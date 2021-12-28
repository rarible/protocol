---
title: Search Orders with Ethereum API
description: The main requests for search orders in Rarible Protocol Ethereum API
---

# Search Orders

The main requests for working with Orders refer to [order-controller](https://ethereum-api.rarible.org/v0.1/doc#tag/order-controller ). Let's look at the example of getOrdersAllByStatus.

## [getOrdersAllByStatus](https://ethereum-api.rarible.org/v0.1/doc#operation/getOrdersAllByStatus)

Returns all orders sorted by status.

Example request:

```shell
curl --request GET 'https://ethereum-api.rarible.org/v0.1/order/orders/all/byStatus?sort=LAST_UPDATE_DESC&size=1&status=ACTIVE'
```

Request parameters:

* **sort ** — sort by last updated orders `LAST_UPDATE_ASC`, `LAST_UPDATE_DESC`
* **size** — number of orders to be returned
* **continuation** — continuation token from the previous response
* **status** — order status `ACTIVE`, `FILLED`, `HISTORICAL`, `INACTIVE`, `CANCELLED`

Response example (status 200):

```json
{
    "orders": [
        {
            "type": "RARIBLE_V2",
            "maker": "0x1a68bab3ebe18ffe95508b2d4e1362addc2cbdd6",
            "make": {
                "assetType": {
                    "assetClass": "ERC20",
                    "contract": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2"
                },
                "value": "260000000000000000",
                "valueDecimal": 0.260000000000000000
            },
            "take": {
                "assetType": {
                    "assetClass": "ERC721",
                    "contract": "0x918f677b3ab4b9290ca96a95430fd228b2d84817",
                    "tokenId": "260"
                },
                "value": "1",
                "valueDecimal": 1
            },
            "fill": "0",
            "fillValue": 0,
            "makeStock": "260000000000000000",
            "makeStockValue": 0.260000000000000000,
            "cancelled": false,
            "salt": "0xf7f9ca62eceb7ee9021a89ac2a77976287721cc56a28f9d8d12c1332898e12e4",
            "signature": "0x382bd104f4497119c75b36e5f0954a03692ab1c3b995266b20623bc718a58f423ff68e2caacb93668811e52b6a099260b3147ded35dc3ad5d65970efde9587761c",
            "createdAt": "2021-11-23T15:08:20.925Z",
            "lastUpdateAt": "2021-11-23T15:08:20.925Z",
            "pending": [],
            "hash": "0x3e23919b0ad64895792c49bb40a551a8e60d70081eb940fa3d1a56c17436eedf",
            "makeBalance": "0",
            "takePrice": 0.260000000000000000,
            "takePriceUsd": 1089.887807206807960000000000000000,
            "priceHistory": [
                {
                    "date": "2021-11-23T15:08:20.925Z",
                    "makeValue": 0.260000000000000000,
                    "takeValue": 1
                }
            ],
            "status": "ACTIVE",
            "data": {
                "dataType": "RARIBLE_V2_DATA_V1",
                "payouts": [],
                "originFees": [
                    {
                        "account": "0x1cf0df2a5a20cd61d68d4489eebbf85b8d39e18a",
                        "value": 250
                    }
                ]
            }
        }
    ],
    "continuation": "1637680100925_3e23919b0ad64895792c49bb40a551a8e60d70081eb940fa3d1a56c17436eedf"
}
```

Response parameters:

* **orders** — list of found orders with basic information on them
* **continuation** — continuation token from the previous response
