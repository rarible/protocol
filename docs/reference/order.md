---
title: Sell NFTs with Rarible Protocol
description: The main information about selling NFTs in Rarible Multichain Protocol
---

# Sell NFTs

When you have your NFT created, there is a high chance that you will want to sell it. Or try at least. You can Sell NFTs with Rarible Multichain Protocol in different blockchains.

## Preparation

1. [Install and configure](https://docs.rarible.org/union-sdk/#installation) Protocol SDK.
2. [Connect the required wallet](https://docs.rarible.org/union-sdk/#metamask-integration-with-rarible).
3. [Mint NFT](mint.md).

## List NFT for sale

To list your NFT for sale, you'll need a token address, the one you get back from

```typescript
await mintResponse.submit();
```

If you want to create a sell order immediately after lazy minting your token, you can use the `mintAndSell` function.

It's pretty straightforward. All we need is:

* `tokenMultichainAddress:` — string in `BLOCKCHAIN:CONTRACT_ADDRESS:TOKEN_ID` format, see code for example
* `price: number` — price in ETH for which we want to list the token (disclaimer: it's not in wei, it's in ETH, so 0.5 equals 0.5 ETH)
* `amount: number` — quantity of NFT we want to list. In case of ERC721 it's 1
* `currency` — type of currency: `FlowAssetTypeNft | TezosXTZAssetType | EthErc20AssetType` etc. you can find all supported currencies `@rarible/api-client/build/models/AssetType` in node modules

```typescript
// 1. Examplary values
const tokenMultichainAddress: string =
  "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382052";
const ethCurrency: EthEthereumAssetType = {
  "@type": "ETH",
};
const price: number = 1;
const amount: number = 1;

// 2. Create PreapreOrderRequest type object and pass it to sdk.order.sell
const orderRequest: PrepareOrderRequest = {
  itemId: toItemId(tokenMultichainAddress),
};

// You can extract info about properties from orderResponse e.g.
// 1. Base fee
// 2. Max Amount
// etc.
const orderResponse = await sdk.order.sell(orderRequest);

// 3. Submit the transaction -> it will pop up the metamask asking you to sign a transaction
const response = await orderResponse.submit({
  price,
  amount,
  currency: ethCurrency,
});
// We get order id from the response. It can be useful when we want to update sell order
```

## Update listed token price

To update the listed token price, you need a sell order id.

Due to security circumstances, you can't update the token price to higher than the one created in the original sell order. If you want to boost the price, you need to cancel the sell order and create a new one.

```typescript
const price: number = 0.8;
const ethCurrency: EthEthereumAssetType = {
  "@type": "ETH",
};

const orderId =
  "ETHEREUM:0x6e794fd04bcf21ee7f347874aefdf36ec1a7b73b5694760b367a7644765a6368";

const updateOrderRequest: PrepareOrderUpdateRequest = {
  orderId: toOrderId(orderId),
};

const updateResponse = await sdk.order.sellUpdate(updateOrderRequest);

const response = await updateResponse.submit({
  price,
});
```

## Fill sell order

Filling a sell order can be compared to paying for an object in a physical store. The sell order is the object being displayed, and filling would represent taking it to the cash register and paying for it.

In order to fill up a sell order, the only required data is orderId.

```typescript
const orderId: string = "ETHEREUM:0x6e794fd04bcf21ee7f347874aefdf36ec1a7b73b5694760b367a7644765a6368";

const fillRequest: PrepareFillRequest = {
  orderId: toOrderId(orderId);
};

const fillResponse = await sdk.order.fill(fillRequest);

const response = await fillResponse.submit({
  amount: 1 // Number of NFTs to buy
})

```

## Checking created order

To check the created order use the `getOrderById` [API method](https://api.rarible.org/v0.1/doc#operation/getOrderById)

??? note "getOrderById"

    Returns Order by ID.
    
    `https://api.rarible.org/v0.1/orders/{id}`
    
    **Example request (staging)**
    
    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/orders/ETHEREUM:0x0293c5918e9f7fb5eec101a656e5ba73fcfd61072ad211a9e80972cc487232ed'
    ```
    
    Request parameters:
    
    * `id` —  ID of your order, has format `${blockchain}:${id}`
    
        For example, `ETHEREUM:0x0293c5918e9f7fb5eec101a656e5ba73fcfd61072ad211a9e80972cc487232ed`
    
    **Example response (status 200)**

    ```json
    {
      "id": "ETHEREUM:0x0293c5918e9f7fb5eec101a656e5ba73fcfd61072ad211a9e80972cc487232ed",
      "fill": "0.00001",
      "platform": "RARIBLE",
      "status": "FILLED",
      "makeStock": "0",
      "cancelled": false,
      "createdAt": "2022-03-11T12:09:14.904Z",
      "lastUpdatedAt": "2022-03-11T12:17:21Z",
      "makePrice": "0.00001",
      "makePriceUsd": "0.026062773565248403",
      "priceHistory": [
        {
          "date": "2022-03-11T12:09:14.904Z",
          "makeValue": "1",
          "takeValue": "0.00001"
        }
      ],
      "maker": "ETHEREUM:0x2c02f0563eaf96dc3ddcb514f4d1832e7cbc801f",
      "make": {
        "type": {
          "@type": "ERC1155_Lazy",
          "contract": "ETHEREUM:0x4ff5fedb430f7393c8c5675e753782b595feb471",
          "tokenId": "19906957776073516298368660511705840565672843874722253325423575352615771308035",
          "uri": "https://shopdefi.gq/api/metadata/c13249c9-e99b-43cd-8a2f-9da5cd26881c",
          "supply": "1",
          "creators": [
            {
              "account": "ETHEREUM:0x2c02f0563eaf96dc3ddcb514f4d1832e7cbc801f",
              "value": 10000
            }
          ],
          "royalties": [
            {
              "account": "ETHEREUM:0x2c02f0563eaf96dc3ddcb514f4d1832e7cbc801f",
              "value": 1000
            }
          ],
          "signatures": [
              "0xee347802d66c1231e3b799dd35768d52df1cd0b8fac88675836c0b8c9394077302d45f29a1e1be7afcf7bd2a9e54cd235a8b632772228fb4cbd0ce013ac3cef71b"
          ]
        },
        "value": "1"
      },
      "take": {
        "type": {
          "@type": "ETH",
          "blockchain": "ETHEREUM"
        },
        "value": "0.00001"
      },
      "salt": "0xaea6697bb08038f1ee23254fef19181bab3694464b612fb6e527ecf85f4cb830",
      "signature": "0xa80eb9c4cbea283976ba4b0db925dae0aefb2d5d4dfedbaa4214ae99a2e5832552e41634ff998b558c258f8b8bd803681534c340029cd1478292ea3838d069791c",
      "pending": [],
      "data": {
        "@type": "ETH_RARIBLE_V2",
        "payouts": [],
        "originFees": []
      }
    }
    ```

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
