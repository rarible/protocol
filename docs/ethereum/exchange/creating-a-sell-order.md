# Creating A Sell Order

## Creating an order

**Step 1. Approval**

We need to call approval on the transfer proxy contract.

{% hint style="danger" %}
The approval on the transfer proxy only needs to be called if a previous approval does not exist.
{% endhint %}

**Step 2. Creating signature**

### Sell ERC721 for ETH

**You can only fill an ETH order if your side of the order is providing the ETH**. Otherwise you would have to use WETH which has the transferFrom capability.

**First** Encode the order for signing

POST to `https://ethereum-api-staging.rarible.org/v0.1/order/encoder/order`

```
{
    "type": "RARIBLE_V2",
    "maker": "0x744222844bFeCC77156297a6427B5876A6769e19",
    "make": {
        "assetType": {
            "assetClass": "ERC721",
            "contract": "0xcfa14f6DC737b8f9e0fC39f05Bf3d903aC5D4575",
            "tokenId": 1
        },
        "value": "1"
    },
    "take": {
        "assetType": {
            "assetClass": "ETH"
        },
        "value": "1000000000000000000"
    },
    "data": {
        "dataType": "RARIBLE_V2_DATA_V1",
        "payouts": [],
        "originFees": []
    },
    "salt": "3621"
}
```

Response:

```
{
    "maker": "0x744222844bfecc77156297a6427b5876a6769e19",
    "makeAsset": {
        "assetType": {
            "assetClass": "0x73ad2146",
            "data": "0x000000000000000000000000cfa14f6dc737b8f9e0fc39f05bf3d903ac5d45750000000000000000000000000000000000000000000000000000000000000001"
        },
        "value": "1"
    },
    "taker": "0x0000000000000000000000000000000000000000",
    "takeAsset": {
        "assetType": {
            "assetClass": "0xaaaebeba",
            "data": "0x"
        },
        "value": "1000000000000000000"
    },
    "salt": "3621",
    "start": "0",
    "end": "0",
    "dataType": "0x4c234266",
    "data": "0x0000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"
}
```

**Then** Sign the order

```
async function sign(provider, order, account, verifyingContract) {
    const chainId = Number(provider._network.chainId);
    const data = EIP712.createTypeData({
        name: "Exchange",
        version: "2",
        chainId,
        verifyingContract
    }, 'Order', order, Types);
  console.log({data})
    return (await EIP712.signTypedData(provider, account, data)).sig;
}
```

**Step 3. Send order with signature to our API**

POST to `https://ethereum-api-staging.rarible.org/v0.1/order/orders`

Payload

```
{
    "type": "RARIBLE_V2",
    "maker": "0x744222844bFeCC77156297a6427B5876A6769e19",
    "make": {
        "assetType": {
            "assetClass": "ERC721",
            "contract": "0xcfa14f6DC737b8f9e0fC39f05Bf3d903aC5D4575",
            "tokenId": 1
        },
        "value": "1"
    },
    "take": {
        "assetType": {
            "assetClass": "ETH"
        },
        "value": "1000000000000000000"
    },
    "data": {
        "dataType": "RARIBLE_V2_DATA_V1",
        "payouts": [],
        "originFees": []
    },
    "salt": "5422",
    "signature": "0x45461654b86e856686e7a2e9a9213b29f8dc32a731046e0c2f1aa01e4eaa991e41ebc67535fac14c333ad5b0d0d821ef518edc9ed08ad7efc0af572620c045ce1c"
}
```

Response

```
{
    "maker": "0x744222844bfecc77156297a6427b5876a6769e19",
    "make": {
        "assetType": {
            "assetClass": "ERC721",
            "contract": "0xcfa14f6dc737b8f9e0fc39f05bf3d903ac5d4575",
            "tokenId": "1"
        },
        "value": "1"
    },
    "take": {
        "assetType": {
            "assetClass": "ETH"
        },
        "value": "1000000000000000000"
    },
    "type": "RARIBLE_V2",
    "fill": "0",
    "makeStock": "1",
    "cancelled": false,
    "salt": "0x000000000000000000000000000000000000000000000000000000000000152e",
    "data": {
        "dataType": "RARIBLE_V2_DATA_V1",
        "payouts": [],
        "originFees": []
    },
    "signature": "0x45461654b86e856686e7a2e9a9213b29f8dc32a731046e0c2f1aa01e4eaa991e41ebc67535fac14c333ad5b0d0d821ef518edc9ed08ad7efc0af572620c045ce1c",
    "createdAt": "2021-05-25T02:04:28.836+00:00",
    "lastUpdateAt": "2021-05-25T02:04:28.983+00:00",
    "pending": [],
    "hash": "0xc9cb92588fc1434a417f4cacb9e1267750e6f1cbe650988a6fdc1d0be8a310a9",
    "makeBalance": "1",
    "takePriceUsd": 2735.1365826056253000000000000000000
}
```

{% hint style="info" %}
In order to get latest information about API, please follow [OpenAPI doc](https://api-reference.rarible.com/#operation/createOrUpdateOrder) for createOrUpdateOrder
{% endhint %}
