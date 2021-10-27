# Order Discovery

## Search orders

Example of how to query orders for all NFTs in a collection

```
curl --location --request GET 'https://ethereum-api-staging.rarible.org/v0.1/order/orders/sell/byCollection?collection=0xcfa14f6DC737b8f9e0fC39f05Bf3d903aC5D4575&sort=LAST_UPDATE'
```

Response

```
{
    "orders": [
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
            "salt": "0x00000000000000000000000000000000000000000000000000000000000002b3",
            "data": {
                "dataType": "RARIBLE_V2_DATA_V1",
                "payouts": [],
                "originFees": []
            },
            "signature": "0xf45a9adfb58fdd9da808b5f80302ebdb7d75f032d6aaee9700ee93f567fff3b148116a93ad2bd908a2d8e9576295650460a653d442f7c3472cb8f1275739075e1c",
            "createdAt": "2021-05-25T01:33:43.358+00:00",
            "lastUpdateAt": "2021-05-25T01:33:43.532+00:00",
            "pending": [],
            "hash": "0x0b3007a2a4cd8701f98b8fd02f2a9bc09320d11d5e4fa8134f884904d8bfdf3b",
            "makeBalance": "1",
            "takePriceUsd": 2735.136582605625300000000000000000
        }
    ],
    "continuation": "1621906423532_0b3007a2a4cd8701f98b8fd02f2a9bc09320d11d5e4fa8134f884904d8bfdf3b"
}
```

For more information on the order indexer and options for discoring orders, see the [API Reference](https://api-reference.rarible.com/#tag/order-controller)
