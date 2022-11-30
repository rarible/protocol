---
title: Rarible Protocol Search Capabilities
description: The search capabilities for information about NFT, orders, and owners using the Protocol API
---

# Search Capabilities

On the [multichain-api.rarible.org](https://multichain-api.rarible.org) you can find main information about Protocol API.

<span style="color:#541e18">**ATTENTION: Flow blockchain is temporary out of support - no data is provided on API for Flow blockchain, direct API calls with FLOW blockchain specified are ruturning ERROR 400 "Flow is not supported"**</span>

## Controllers

Use the following controllers to search information about NFT with our multichain API:

* [Signature controller](https://multichain-api.rarible.org/testnet/tag/signature-controller) — uses for validation of the order signature
* [Currency controller](https://multichain-api.rarible.org/testnet/tag/currency-controller) — getting currency USD rate
* [Item controller](https://multichain-api.rarible.org/testnet/tag/item-controller) — getting information about NFT items
* [Ownership controller](https://multichain-api.rarible.org/testnet/tag/ownership-controller) — getting information about NFT items ownership
* [Order controller](https://multichain-api.rarible.org/testnet/tag/order-controller) — getting information about NFT orders
* [Auction controller](https://multichain-api.rarible.org/testnet/tag/auction-controller) — getting information about NFT auctions
* [Activity controller](https://multichain-api.rarible.org/testnet/tag/activity-controller) — getting information about activities with NFT
* [Collection controller](https://multichain-api.rarible.org/testnet/tag/collection-controller) — getting information about NFT collections

## API usage Examples

### Items

??? example "get Item by owner"

    Returns Item by owner
    
    [`https://api.rarible.org/v0.1/items/byOwner`](https://api.rarible.org/v0.1/doc#operation/getItemsByOwner)
    
    **Example request (mainnet)**
    
    ```shell
    curl --request GET 'https://api.rarible.org/v0.1/items/byOwner?owner=ETHEREUM:0x2e2d91093341493d4722083e710110163c3be5b9&size=1'
    ```
    
    Request parameters:
    
    * `owner` — address of the item owner, has format `${blockchain}:${address}`. For example, `ETHEREUM:0x2e2d91093341493d4722083e710110163c3be5b9`
    
    **Example response (status 200)**

    ```json
    {
      "continuation": "1645421913958_POLYGON:0x828383b51514873cc937ee83f57fbbff0221700c:13471465447374847834598764369914954310108963722019096037095232973924004254539:0x2e2d91093341493d4722083e710110163c3be5b9",
      "items": [
        {
          "id": "POLYGON:0x828383b51514873cc937ee83f57fbbff0221700c:13471465447374847834598764369914954310108963722019096037095232973924004254539",
          "blockchain": "POLYGON",
          "collection": "POLYGON:0x828383b51514873cc937ee83f57fbbff0221700c",
          "contract": "POLYGON:0x828383b51514873cc937ee83f57fbbff0221700c",
          "tokenId": "13471465447374847834598764369914954310108963722019096037095232973924004254539",
          "creators": [
            {
              "account": "ETHEREUM:0x2e2d91093341493d4722083e710110163c3be5b9",
              "value": 10000
            }
          ],
          "lazySupply": "0",
          "pending": [],
          "mintedAt": "2022-02-21T05:38:22Z",
          "lastUpdatedAt": "2022-02-21T05:38:33.958Z",
          "supply": "1",
          "meta": {
            "name": "Unnamed territory",
            "description": "**NextEarth LAND NFT**\n\nİTÜ Gümüşsuyu Öğrenci Yurdu, İTÜ Gümüşsuyu Yerleşkesi, Beyoglu, Istanbul 34437, Turkey",
            "tags": [],
            "genres": [],
            "attributes": [
              {
                "key": "Type",
                "value": "Land"
              },
              {
                "key": "Has water",
                "value": "No"
              },
              {
                "key": "Has non-urban",
                "value": "No"
              },
              {
                "key": "Has urban",
                "value": "Yes"
              },
              {
                "key": "Pack Purchase",
                "value": "No"
              },
              {
                "key": "Tile count",
                "value": "1"
              },
              {
                "key": "Urban",
                "value": "1"
              },
              {
                "key": "Non Urban",
                "value": "0"
              },
              {
                "key": "Water",
                "value": "0"
              },
              {
                "key": "Country",
                "value": "Turkey"
              }
            ],
            "content": [
              {
                "@type": "IMAGE",
                "url": "https://storage.googleapis.com/cdn-pub-production-nextearth-io/data/ae5db33b-e770-4e5d-81cf-e074a08d57eb/nft-image/57d55696-24dd-49f4-8f31-15102acc9554.png",
                "representation": "ORIGINAL",
                "mimeType": "image/png",
                "size": 812417,
                "width": 1024,
                "height": 1024
              }
            ],
            "restrictions": []
          },
          "deleted": false,
          "originOrders": [],
          "ammOrders": {
            "ids": []
          },
          "auctions": [],
          "totalStock": "0",
          "sellers": 0
        }
      ]
    }
    ```

??? example "get Item by Id"

    Returns Item by Id
    
    [`https://api.rarible.org/v0.1/items/{itemId}`](https://api.rarible.org/v0.1/doc#operation/getItemById)
    
    **Example request (mainnet)**
    
    ```shell
    curl --request GET 'https://api.rarible.org/v0.1/items/ETHEREUM:0xb66a603f4cfe17e3d27b87a8bfcad319856518b8:20886900154002869811386593404403268730099008514936490854803004457464658657286'
    ```
    
    Request parameters:
    
    * `itemId` — Id of your NFT, has format `${blockchain}:${token}:${tokenId}`. For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:12345`
    
    **Example response (status 200)**

    ```json
    {
      "id": "ETHEREUM:0xb66a603f4cfe17e3d27b87a8bfcad319856518b8:20886900154002869811386593404403268730099008514936490854803004457464658657286",
      "blockchain": "ETHEREUM",
      "collection": "ETHEREUM:0xb66a603f4cfe17e3d27b87a8bfcad319856518b8",
      "contract": "ETHEREUM:0xb66a603f4cfe17e3d27b87a8bfcad319856518b8",
      "tokenId": "20886900154002869811386593404403268730099008514936490854803004457464658657286",
      "creators": [
        {
          "account": "ETHEREUM:0x2e2d91093341493d4722083e710110163c3be5b9",
          "value": 10000
        }
      ],
      "lazySupply": "100",
      "pending": [],
      "mintedAt": "2022-01-04T09:30:45.322Z",
      "lastUpdatedAt": "2022-01-04T09:30:45.322Z",
      "supply": "100",
      "meta": {
        "name": "night owl",
        "description": "night owls only survive at night",
        "tags": [],
        "genres": [],
        "attributes": [],
        "content": [
          {
            "@type": "IMAGE",
            "url": "https://ipfs.infura.io/ipfs/QmYUxZSD8yUZk6zLxSZPvRXu1eQduUgS4b3P9UNd4yoHGk/image.jpeg",
            "representation": "ORIGINAL",
            "mimeType": "image/jpeg",
            "size": 1554451,
            "width": 3120,
            "height": 4160
          }
        ],
        "restrictions": []
      },
      "deleted": false,
      "bestSellOrder": {
        "id": "ETHEREUM:0xabf742f5c6959ec1f4cf353c477fd51af8ecb7e080989a4959755197132be68b",
        "fill": "0",
        "platform": "RARIBLE",
        "status": "ACTIVE",
        "makeStock": "100",
        "cancelled": false,
        "optionalRoyalties": false,
        "createdAt": "2022-01-04T09:31:37.405Z",
        "lastUpdatedAt": "2022-01-04T09:31:37.405Z",
        "dbUpdatedAt": "2022-01-04T09:31:37.405Z",
        "makePrice": "0.091",
        "makePriceUsd": "103.4470817788344755",
        "maker": "ETHEREUM:0x2e2d91093341493d4722083e710110163c3be5b9",
        "make": {
          "type": {
            "@type": "ERC1155_Lazy",
            "contract": "ETHEREUM:0xb66a603f4cfe17e3d27b87a8bfcad319856518b8",
            "tokenId": "20886900154002869811386593404403268730099008514936490854803004457464658657286",
            "uri": "/ipfs/QmSy7ca3AWHYiNL8rKaU3JueAXgiD8UEupfGLjnBzxyaMT",
            "supply": "100",
            "creators": [
              {
                "account": "ETHEREUM:0x2e2d91093341493d4722083e710110163c3be5b9",
                "value": 10000
              }
            ],
            "royalties": [
              {
                "account": "ETHEREUM:0x2e2d91093341493d4722083e710110163c3be5b9",
                "value": 2000
              }
            ],
            "signatures": [
              "0xf822e8642be85a526f92c5bbec5af0550741c5d1b9b5b4ff2d83b424d2a47d1514254ec9667ded2fc74697758c013374456c7cd0879750e00097963ca08494481b"
            ]
          },
          "value": "100"
        },
        "take": {
          "type": {
            "@type": "ETH",
            "blockchain": "ETHEREUM"
          },
          "value": "9.1"
        },
        "salt": "0x28000d2f67a3eeed7cf0a2b85b559e71ba36a5837f8e1693f5f2355f1667adb6",
        "signature": "0x51233898413883053f099e5e1ccac1418631a3108696c204aa91eb3024bcd4ed420e42f2fbdcb242a940a0fb0b697bcdb415d1269ed6507e4590cddb723c40d31c",
        "data": {
          "@type": "ETH_RARIBLE_V2",
          "payouts": [],
          "originFees": [
            {
              "account": "ETHEREUM:0x1cf0df2a5a20cd61d68d4489eebbf85b8d39e18a",
              "value": 250
            }
          ]
        }
      },
      "originOrders": [],
      "ammOrders": {
        "ids": []
      },
      "auctions": [],
      "totalStock": "0",
      "sellers": 0
    }
    ```

??? example "get All Items"

    Returns All Items
    
    [`https://api.rarible.org/v0.1/items/all`](https://api.rarible.org/v0.1/doc#operation/getAllItems)
    
    **Example request (mainnet)**
    
    ```shell
    curl --request GET 'https://api.rarible.org/v0.1/items/all?blockchains=POLYGON&size=1'
    ```
    
    **Example response (status 200)**

    ```json
    {
      "continuation": "1669016456510_POLYGON:0x22d5f9b75c524fec1d6619787e582644cd4d7422:208",
      "items": [
        {
          "id": "POLYGON:0x22d5f9b75c524fec1d6619787e582644cd4d7422:208",
          "blockchain": "POLYGON",
          "collection": "POLYGON:0x22d5f9b75c524fec1d6619787e582644cd4d7422",
          "contract": "POLYGON:0x22d5f9b75c524fec1d6619787e582644cd4d7422",
          "tokenId": "208",
          "creators": [
            {
              "account": "ETHEREUM:0x0e06f59f3737e7fe81a25c2332ddb1b164a0933b",
              "value": 10000
            }
          ],
          "lazySupply": "0",
          "pending": [],
          "mintedAt": "2022-02-28T21:05:45Z",
          "lastUpdatedAt": "2022-11-21T07:40:56.510Z",
          "supply": "2641228165888999997013728",
          "meta": {
            "name": "Parsnip",
            "description": "\r\n## Parsnip\r\n\r\nA crop grown at Sunflower Land.\r\n\r\nNot to be mistaken for carrots.\r\n\r\n## Supply\r\n\r\nUnlimited\r\n\r\n[Link](https://docs.sunflower-land.com/player-guides/crop-farming)",
            "tags": [],
            "genres": [],
            "originalMetaUri": "https://sunflower-land.com/play/erc1155/208.json",
            "attributes": [
              {
                "key": "Purpose",
                "value": "Crop"
              }
            ],
            "content": [
              {
                "@type": "IMAGE",
                "url": "https://sunflower-land.com/play/erc1155/images/208.png",
                "representation": "ORIGINAL",
                "mimeType": "image/png",
                "size": 5590,
                "available": true,
                "width": 400,
                "height": 400
              }
            ],
            "restrictions": []
          },
          "deleted": false,
          "bestSellOrder": {
            "id": "POLYGON:0xf808f42f8fc3fb2b75ccc0767504634a5b16aacfd77d35b87314173607c8b70c",
            "fill": "1000001",
            "platform": "RARIBLE",
            "status": "ACTIVE",
            "makeStock": "8999999998999999",
            "cancelled": false,
            "optionalRoyalties": false,
            "createdAt": "2022-10-30T06:43:45.313Z",
            "lastUpdatedAt": "2022-11-20T14:50:37.506Z",
            "dbUpdatedAt": "2022-11-20T15:15:09.753Z",
            "makePrice": "0.00000000000000007",
            "makePriceUsd": "0.000000000000000056967095449175135",
            "maker": "ETHEREUM:0x0e27030eff636cf4f106bdba6a0808b15fec26a8",
            "make": {
              "type": {
                "@type": "ERC1155",
                "contract": "POLYGON:0x22d5f9b75c524fec1d6619787e582644cd4d7422",
                "tokenId": "208"
              },
              "value": "9000000000000000"
            },
            "take": {
              "type": {
                "@type": "ETH",
                "blockchain": "POLYGON"
              },
              "value": "0.63"
            },
            "salt": "0x773848ad047df6e1218da98aeb48af0e7cf3e3a36f20a59d1e0c3dccb0cf712b",
            "signature": "0xf4c5de0cbb1d662148a169d985b57ccdd9a12e172f5f07f4757e2ae2065b26e83bd917785c8f8cb5926eea1eea61eb51281295314da280483874ab48d26073381b",
            "data": {
              "@type": "ETH_RARIBLE_V2",
              "payouts": [],
              "originFees": [
                {
                  "account": "ETHEREUM:0x0f22f838aaca272afb0f268e4f4e655fac3a35ec",
                  "value": 100
                }
              ]
            }
          },
          "originOrders": [],
          "ammOrders": {
            "ids": []
          },
          "auctions": [],
          "totalStock": "13019738007818531",
          "sellers": 25,
          "lastSale": {
            "date": "2022-11-20T22:58:51Z",
            "seller": "ETHEREUM:0x2ed2c862c8a4a08f0aa0eb44457f913a9642d8a8",
            "buyer": "ETHEREUM:0x9c8dd003954c9fad77e5eca97775b1cd808a3af5",
            "value": "1000000000000000000",
            "currency": {
              "@type": "ETH",
              "blockchain": "POLYGON"
            },
            "price": "0"
          }
        }
      ]
    }
    ```

### Orders

??? example "get Order by Id"

    Returns Order by Id

    [`https://api.rarible.org/v0.1/orders/{id}`](https://api.rarible.org/v0.1/doc#operation/getOrderById)

    **Example request (mainnet)**

    ```shell
        curl --request GET 'https://api.rarible.org/v0.1/orders/ETHEREUM:0x48371f4b1656fa02617945936ba701341cbf586ebebfd9a6d188758c5e8baa37'
    ```

    Request parameters:

    * `id` — order Id, has format `${blockchain}:${id}`. For example, `ETHEREUM:0x48371f4b1656fa02617945936ba701341cbf586ebebfd9a6d188758c5e8baa37`

    **Example response (status 200)**

    ```json
    {
      "id": "ETHEREUM:0x48371f4b1656fa02617945936ba701341cbf586ebebfd9a6d188758c5e8baa37",
      "fill": "0",
      "platform": "X2Y2",
      "status": "CANCELLED",
      "startedAt": "2022-11-15T20:41:58Z",
      "endedAt": "2022-12-15T20:40:49Z",
      "makeStock": "0",
      "cancelled": true,
      "optionalRoyalties": false,
      "createdAt": "2022-11-15T20:41:58Z",
      "lastUpdatedAt": "2022-11-15T20:48:47Z",
      "dbUpdatedAt": "2022-11-15T20:49:00.376Z",
      "makePrice": "59.3",
      "makePriceUsd": "64662.5109083251711",
      "maker": "ETHEREUM:0xed2ab4948ba6a909a7751dec4f34f303eb8c7236",
      "make": {
        "type": {
          "@type": "ERC721",
          "contract": "ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d",
          "tokenId": "6582"
        },
        "value": "1"
      },
      "take": {
        "type": {
          "@type": "ETH",
          "blockchain": "ETHEREUM"
        },
        "value": "59.3"
      },
      "salt": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "data": {
        "@type": "ETH_X2Y2_ORDER_DATA_V1",
        "itemHash": "0x48371f4b1656fa02617945936ba701341cbf586ebebfd9a6d188758c5e8baa37",
        "isCollectionOffer": false,
        "isBundle": false,
        "side": 1,
        "orderId": "22856542"
      }
    }
    ```

??? example "get Sell Orders by maker"

    Returns Sell Orders by maker

    [`https://api.rarible.org/v0.1/orders/sell/byMaker`](https://api.rarible.org/v0.1/doc#operation/getSellOrdersByMaker)

    **Example request (mainnet)**

    ```shell
    curl --request GET 'https://api.rarible.org/v0.1/orders/sell/byMaker?maker=ETHEREUM:0xe59072c5084ec2dc16e6bcdc3560802ffbafb5cb&size=1'
    ```

    Request parameters:

    * `maker` — the maker of the order, has format `${blockchain}:${id}`. For example, `ETHEREUM:0xe59072c5084ec2dc16e6bcdc3560802ffbafb5cb`

    **Example response (status 200)**

    ```json
    {
      "continuation": "1650005167000_0xc4ecfd56430005afd1599582d3e176b4d8a899ffe19635c465f1d77a61887394",
      "orders": [
        {
          "id": "ETHEREUM:0xc4ecfd56430005afd1599582d3e176b4d8a899ffe19635c465f1d77a61887394",
          "fill": "0.000001",
          "platform": "OPEN_SEA",
          "status": "FILLED",
          "startedAt": "2022-04-15T06:41:25Z",
          "endedAt": "2022-05-15T06:41:11Z",
          "makeStock": "0",
          "cancelled": false,
          "optionalRoyalties": false,
          "createdAt": "2022-04-15T06:43:13.856Z",
          "lastUpdatedAt": "2022-04-15T06:46:07Z",
          "dbUpdatedAt": "2022-04-15T06:46:07Z",
          "makePrice": "0.000001",
          "makePriceUsd": "0.001090430200814927",
          "maker": "ETHEREUM:0xe59072c5084ec2dc16e6bcdc3560802ffbafb5cb",
          "taker": "ETHEREUM:0xc0dbf125284240a768ad4ac1e2a2f20d77f6cfc8",
          "make": {
            "type": {
              "@type": "ERC1155",
              "contract": "ETHEREUM:0x495f947276749ce646f68ac8c248420045cb7b5e",
              "tokenId": "103834860413964016633619762390589326621035685084276300587330675527037531193345"
            },
            "value": "1"
          },
          "take": {
            "type": {
              "@type": "ETH",
              "blockchain": "ETHEREUM"
            },
            "value": "0.000001"
          },
          "salt": "0xa6cb012bbaeeacb79c4ea9e6670292434b08124ab672b8541f47a970e50bd329",
          "signature": "0xc5418e2c254b7d81f7d429785380a2f0c6cc6e9c0be5e6fc4b2a8a83573c167a7789549f26b7922a4e66a895e2f63f17bafa052d704de592a95baf1a8e9709661c",
          "data": {
            "@type": "ETH_OPEN_SEA_V1",
            "exchange": "ETHEREUM:0x7f268357a8c2552623316e2562d90e642bb538e5",
            "makerRelayerFee": "1250",
            "takerRelayerFee": "0",
            "makerProtocolFee": "0",
            "takerProtocolFee": "0",
            "feeRecipient": "ETHEREUM:0x5b3256965e7c3cf26e11fcaf296dfc8807c01073",
            "feeMethod": "SPLIT_FEE",
            "side": "SELL",
            "saleKind": "FIXED_PRICE",
            "howToCall": "DELEGATE_CALL",
            "callData": "0x96809f90000000000000000000000000e59072c5084ec2dc16e6bcdc3560802ffbafb5cb0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000495f947276749ce646f68ac8c248420045cb7b5ee59072c5084ec2dc16e6bcdc3560802ffbafb5cb0000000000000b00000000010000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000e00000000000000000000000000000000000000000000000000000000000000000",
            "replacementPattern": "0x000000000000000000000000000000000000000000000000000000000000000000000000ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
            "staticTarget": "ETHEREUM:0x0000000000000000000000000000000000000000",
            "staticExtraData": "0x",
            "extra": "0"
          }
        }
      ]
    }
    ```

??? example "get All Orders"

    Returns all Orders

    [`https://api.rarible.org/v0.1/orders/all`](https://api.rarible.org/v0.1/doc#operation/getOrdersAll)

    **Example request (mainnet)**

    ```shell
    curl --request GET 'https://api.rarible.org/v0.1/orders/all?size=1'
    ```

    **Example response (status 200)**

    ```json
    {
        "continuation": "ETHEREUM:1648132257821_0x487cf9fc8c7713dd634e2d0698fde08fba134ce81e515a9c7b75121096ced384",
        "orders": [
            {
                "id": "ETHEREUM:0x487cf9fc8c7713dd634e2d0698fde08fba134ce81e515a9c7b75121096ced384",
                "fill": "0",
                "platform": "RARIBLE",
                "status": "ACTIVE",
                "makeStock": "1",
                "cancelled": false,
                "createdAt": "2022-03-24T14:30:57.821Z",
                "lastUpdatedAt": "2022-03-24T14:30:57.821Z",
                "makePrice": "0.01",
                "makePriceUsd": "30.198384450784797",
                "priceHistory": [
                    {
                        "date": "2022-03-24T14:30:57.821Z",
                        "makeValue": "1",
                        "takeValue": "0.01"
                    }
                ],
                "maker": "ETHEREUM:0x402a19096d7e4d1cbe74fc92b4e21bf33614e1a5",
                "make": {
                    "type": {
                        "@type": "ERC721_Lazy",
                        "contract": "ETHEREUM:0x6110ea0489c929b44152e99c133e17025a684223",
                        "tokenId": "29022402683878927866272288177291204022157824894707812777715415655733163720747",
                        "uri": "/ipfs/Qmb37SGcSV3ELHeZSzcZt5ymERUn9ug5vtqmPQfs7yFQUm",
                        "creators": [
                            {
                                "account": "ETHEREUM:0x402a19096d7e4d1cbe74fc92b4e21bf33614e1a5",
                                "value": 10000
                            }
                        ],
                        "royalties": [
                            {
                                "account": "ETHEREUM:0x402a19096d7e4d1cbe74fc92b4e21bf33614e1a5",
                                "value": 1000
                            }
                        ],
                        "signatures": [
                            "0x60647533cdabee46b8e40b19cfcc588585d306ce061ddaf50e5dc8187ea6e0e955e91ef1d61a4cbf17dc81136bdadccf6052d54791fa3dbad65bd5925932e7191c"
                        ]
                    },
                    "value": "1"
                },
                "take": {
                    "type": {
                        "@type": "ETH",
                        "blockchain": "ETHEREUM"
                    },
                    "value": "0.01"
                },
                "salt": "0x4605d2c0a64793ea84b6b58edf2326356d5562eeeb4e550f2b79bb965f984ac4",
                "signature": "0xd67ffbe94321dce166ff3028546914547a9f6d44ba434db20e0244f83626862e41606a1254f5c7565bce88ae78d7f5f0214553b6dd6d5cd4f9198302d5c1fa781c",
                "pending": [],
                "data": {
                    "@type": "ETH_RARIBLE_V2",
                    "payouts": [],
                    "originFees": [
                        {
                            "account": "ETHEREUM:0x76c5855e93bd498b6331652854c4549d34bc3a30",
                            "value": 250
                        }
                    ]
                }
            }
        ]
    }
    ```

### Collections

??? example "get Collections by owner"

    Returns Collections by owner

    [`https://api.rarible.org/v0.1/collections/byOwner`](https://api.rarible.org/v0.1/doc#operation/getCollectionsByOwner)

    **Example request (mainnet)**

    ```shell
    curl --request GET 'https://api.rarible.org/v0.1/collections/byOwner?owner=ETHEREUM:0x5a019874f4fae314b0eaa4606be746366e661306'
    ```

    Request parameters:

    * `owner` — address of the collection owner, has format `${blockchain}:${address}`. For example, `ETHEREUM:0x8b3e026252ab4299d69779b4f533913e76a40420`

    **Example response (status 200)**

    ```json
    {
      "total": 1,
      "continuation": "1669113675427_3961628903332964660",
      "collections": [
        {
          "id": "ETHEREUM:0x8a90cab2b38dba80c64b7734e58ee1db38b8992e",
          "blockchain": "ETHEREUM",
          "type": "ERC721",
          "status": "CONFIRMED",
          "name": "Doodles",
          "symbol": "DOODLE",
          "owner": "ETHEREUM:0x5a019874f4fae314b0eaa4606be746366e661306",
          "features": [
            "APPROVE_FOR_ALL"
          ],
          "minters": [],
          "meta": {
            "name": "Doodles",
            "description": "A community-driven collectibles project featuring art by Burnt Toast. Doodles come in a joyful range of colors, traits and sizes with a collection size of 10,000. Each Doodle allows its owner to vote for experiences and activations paid for by the Doodles Community Treasury.",
            "tags": [],
            "genres": [],
            "externalUri": "https://doodles.app",
            "content": [
              {
                "@type": "IMAGE",
                "url": "https://i.seadn.io/gae/7B0qai02OdHA8P_EOVK672qUliyjQdQDGNrACxs7WnTgZAkJa_wWURnIFKeOh5VTf8cfTqW3wQpozGedaC9mteKphEOtztls02RlWQ?w=500&auto=format",
                "representation": "ORIGINAL"
              }
            ],
            "externalLink": "https://doodles.app",
            "sellerFeeBasisPoints": 250,
            "feeRecipient": "ETHEREUM:0xd1f124cc900624e1ff2d923180b3924147364380"
          },
          "bestBidOrder": {
            "id": "ETHEREUM:0xd8768764825b1579a7564aa53c2ae6ff35b11264753bb7996d8a3783dd622d6c",
            "fill": "0",
            "platform": "RARIBLE",
            "status": "ACTIVE",
            "endedAt": "2023-02-11T10:14:45Z",
            "makeStock": "1.21",
            "cancelled": false,
            "optionalRoyalties": false,
            "createdAt": "2022-11-13T10:14:56.695Z",
            "lastUpdatedAt": "2022-11-19T20:04:47Z",
            "dbUpdatedAt": "2022-11-19T20:04:54.528Z",
            "takePrice": "1.21",
            "takePriceUsd": "1356.514677472391657",
            "maker": "ETHEREUM:0x77c0c1c3d55a9afad3ad19f231259cf78a203a8d",
            "make": {
              "type": {
                "@type": "ERC20",
                "contract": "ETHEREUM:0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2"
              },
              "value": "1.21"
            },
            "take": {
              "type": {
                "@type": "COLLECTION",
                "contract": "ETHEREUM:0x8a90cab2b38dba80c64b7734e58ee1db38b8992e"
              },
              "value": "1"
            },
            "salt": "0x813278fe4ebd6335b4333a80497738c1f38996e0b315ce812ad421c54d47dd23",
            "signature": "0x4371588e8b5ed0331fe24e72f4a411a6c2eb231728096b15c34b7694ca400e2c1f2c53f6d43a99e56258619d3e7d5342b4ef876d49384c19b005edb851a3a8591c",
            "data": {
              "@type": "ETH_RARIBLE_V2",
              "payouts": [],
              "originFees": [
                {
                  "account": "ETHEREUM:0x1cf0df2a5a20cd61d68d4489eebbf85b8d39e18a",
                  "value": 100
                }
              ]
            }
          },
          "originOrders": [],
          "statistics": {
            "ownerCount": 5582,
            "itemCount": 5582,
            "ownerCountTotal": "10000",
            "itemCountTotal": "5582",
            "highestSale": {
              "value": "296.4807216419148",
              "valueUsd": "1110196.5062220949"
            },
            "totalVolume": {
              "value": "207022.60851323992",
              "valueUsd": "583735118.8325903"
            },
            "volumes": [
              {
                "period": "DAY",
                "value": {
                  "value": "7.8",
                  "valueUsd": "10007.35639766455"
                },
                "changePercent": "-83.04460747884089"
              },
              {
                "period": "WEEK",
                "value": {
                  "value": "293.64456980127034",
                  "valueUsd": "378942.51244305656"
                },
                "changePercent": "-22.766684857781108"
              },
              {
                "period": "MONTH",
                "value": {
                  "value": "1520.5154496508244",
                  "valueUsd": "2029754.9444540597"
                },
                "changePercent": "-54.72143141310838"
              }
            ],
            "floorPrice": {
              "value": "7.69",
              "valueUsd": "10050.134755031484"
            }
          }
        }
      ]
    }
    ```

??? example "get Collection by Id"

    Returns Collection by Id

    [`https://api.rarible.org/v0.1/collections/{collection}`](https://api.rarible.org/v0.1/doc#operation/getCollectionById)

    **Example request (mainnet)**

    ```shell
    curl --request GET 'https://api.rarible.org/v0.1/collections/POLYGON:0x00000000004ba8d1691a4c215fd2bd99771dccc7'
    ```

    Request parameters:

    * `collection` — collection address, has format `${blockchain}:${address}`. For example, `POLYGON:0x00000000004ba8d1691a4c215fd2bd99771dccc7`

    **Example response (status 200)**

    ```json
    {
      "id": "POLYGON:0x00000000004ba8d1691a4c215fd2bd99771dccc7",
      "blockchain": "POLYGON",
      "type": "ERC721",
      "status": "CONFIRMED",
      "name": "LUCA",
      "symbol": "InvoiceNFT",
      "owner": "ETHEREUM:0x00000000007b9543f6fea6a20fd440b050db3ea0",
      "features": [
        "APPROVE_FOR_ALL"
      ],
      "minters": [],
      "meta": {
        "name": "Untitled",
        "tags": [],
        "genres": [],
        "content": []
      },
      "originOrders": []
    }
    ```

??? example "get All Collections"

    Returns all Collections

    [`https://api.rarible.org/v0.1/collections/all`](https://api.rarible.org/v0.1/doc#operation/getAllCollections)

    **Example request (mainnet)**

    ```shell
    curl --request GET 'https://api.rarible.org/v0.1/collections/all?blockchains=ETHEREUM&size=1'
    ```

    **Example response (status 200)**

    ```json
    {
        "total": 1,
        "continuation": "ETHEREUM:0x0000000007dbc95a44e65b0439427de8236c53d3",
        "collections": [
            {
                "id": "ETHEREUM:0x0000000007dbc95a44e65b0439427de8236c53d3",
                "blockchain": "ETHEREUM",
                "type": "ERC721",
                "name": "Test",
                "symbol": "TEST",
                "owner": "ETHEREUM:0x8b3e026252ab4299d69779b4f533913e76a40420",
                "features": [
                    "APPROVE_FOR_ALL"
                ],
                "minters": [],
                "meta": {
                    "name": "Untitled",
                    "content": []
                }
            }
        ]
    }
    ```

### Ownerships

??? example "get Ownerships by Item"

    Returns Ownerships by Item

    [`https://api.rarible.org/v0.1/ownerships/byItem`](https://api.rarible.org/v0.1/doc#operation/getOwnershipsByItem)

    **Example request (mainnet)**

    ```shell
    curl --request GET 'https://api.rarible.org/v0.1/ownerships/byItem?itemId=ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:390'
    ```

    Request parameters:

    * `itemId` — Id of your NFT, has format `${blockchain}:${token}:${tokenId}`. For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:12345`

    **Example response (status 200)**

    ```json
    {
      "continuation": "1668748561355_ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:390:0xba26877c2036e1f2baba63bdd5bfe996b050e13c",
      "ownerships": [
        {
          "id": "ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:390:0xba26877c2036e1f2baba63bdd5bfe996b050e13c",
          "blockchain": "ETHEREUM",
          "itemId": "ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:390",
          "contract": "ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d",
          "collection": "ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d",
          "tokenId": "390",
          "owner": "ETHEREUM:0xba26877c2036e1f2baba63bdd5bfe996b050e13c",
          "value": "1",
          "createdAt": "2022-11-18T05:16:01.355Z",
          "lastUpdatedAt": "2022-11-18T05:16:02.377Z",
          "creators": [],
          "lazyValue": "0",
          "pending": [],
          "bestSellOrder": {
            "id": "ETHEREUM:0x87301d558f0863ddc43f6200d76cb28bcdf2c292691c8ed37b5ae0c29842d2fd",
            "fill": "0",
            "platform": "LOOKSRARE",
            "status": "ACTIVE",
            "startedAt": "2022-11-22T01:13:35Z",
            "endedAt": "2022-11-23T01:13:35Z",
            "makeStock": "1",
            "cancelled": false,
            "optionalRoyalties": false,
            "createdAt": "2022-11-22T01:13:35Z",
            "lastUpdatedAt": "2022-11-22T01:13:35Z",
            "dbUpdatedAt": "2022-11-22T01:15:36.700Z",
            "makePrice": "61.2",
            "makePriceUsd": "68454.63864745771392",
            "maker": "ETHEREUM:0xba26877c2036e1f2baba63bdd5bfe996b050e13c",
            "make": {
              "type": {
                "@type": "ERC721",
                "contract": "ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d",
                "tokenId": "390"
              },
              "value": "1"
            },
            "take": {
              "type": {
                "@type": "ETH",
                "blockchain": "ETHEREUM"
              },
              "value": "61.2"
            },
            "salt": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "signature": "0x4774e21e5a4117c26f7d47bdf8d2e860291ae72856fca7953e24ee413a0c3d556a6c0ce7ff22ea4c344b45bfcafc29bf5c7bff9641f5c7ff672566ed56dd11821b",
            "data": {
              "@type": "ETH_LOOKSRARE_ORDER_DATA_V1",
              "minPercentageToAsk": 9800,
              "strategy": "ETHEREUM:0x579af6fd30bf83a5ac0d636bc619f98dbdeb930c",
              "nonce": 169
            }
          },
          "originOrders": []
        }
      ]
    }
    ```

??? example "get Ownerships by Id"

    Returns Ownerships by Id

    [`https://api.rarible.org/v0.1/ownerships/{ownershipId}`](https://api.rarible.org/v0.1/doc#operation/getOwnershipById)

    **Example request (mainnet)**

    ```shell
    curl --request GET 'https://api.rarible.org/v0.1/ownerships/ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:390:0xba26877c2036e1f2baba63bdd5bfe996b050e13c'
    ```

    Request parameters:

    * `ownershipId` — ownership Id in format `${blockchain}:${token}:${tokenId}:${owner}`. For example, `ETHEREUM:0x63ad270fc18f6f9435c3e205f06e003d3b861d33:765:0xe64ebc77ef72df8a7689d8928bc004b9e7ff43b3`

    **Example response (status 200)**

    ```json
    {
      "id": "ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:390:0xba26877c2036e1f2baba63bdd5bfe996b050e13c",
      "blockchain": "ETHEREUM",
      "itemId": "ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:390",
      "contract": "ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d",
      "collection": "ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d",
      "tokenId": "390",
      "owner": "ETHEREUM:0xba26877c2036e1f2baba63bdd5bfe996b050e13c",
      "value": "1",
      "createdAt": "2022-11-18T05:16:01.355Z",
      "lastUpdatedAt": "2022-11-18T05:16:02.377Z",
      "creators": [],
      "lazyValue": "0",
      "pending": [],
      "bestSellOrder": {
        "id": "ETHEREUM:0x87301d558f0863ddc43f6200d76cb28bcdf2c292691c8ed37b5ae0c29842d2fd",
        "fill": "0",
        "platform": "LOOKSRARE",
        "status": "ACTIVE",
        "startedAt": "2022-11-22T01:13:35Z",
        "endedAt": "2022-11-23T01:13:35Z",
        "makeStock": "1",
        "cancelled": false,
        "optionalRoyalties": false,
        "createdAt": "2022-11-22T01:13:35Z",
        "lastUpdatedAt": "2022-11-22T01:13:35Z",
        "dbUpdatedAt": "2022-11-22T01:15:36.700Z",
        "makePrice": "61.2",
        "makePriceUsd": "68454.63864745771392",
        "maker": "ETHEREUM:0xba26877c2036e1f2baba63bdd5bfe996b050e13c",
        "make": {
          "type": {
            "@type": "ERC721",
            "contract": "ETHEREUM:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d",
            "tokenId": "390"
          },
          "value": "1"
        },
        "take": {
          "type": {
            "@type": "ETH",
            "blockchain": "ETHEREUM"
          },
          "value": "61.2"
        },
        "salt": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "signature": "0x4774e21e5a4117c26f7d47bdf8d2e860291ae72856fca7953e24ee413a0c3d556a6c0ce7ff22ea4c344b45bfcafc29bf5c7bff9641f5c7ff672566ed56dd11821b",
        "data": {
          "@type": "ETH_LOOKSRARE_ORDER_DATA_V1",
          "minPercentageToAsk": 9800,
          "strategy": "ETHEREUM:0x579af6fd30bf83a5ac0d636bc619f98dbdeb930c",
          "nonce": 169
        }
      },
      "originOrders": []
    }
    ```

### Activity

We have several query parameters for paging and continuation in the Activity controller methods:

* `size` — the maximum number of results per page to return
* `continuation` — deprecated parameter
* `cursor` — combined continuation token from the previous response, type of page token. Can be used to get the next page of results in a subsequent list request. Has format `${BLOCKCHAIN}:${TS_MS}_{ENTITY_ID};...`, where:
    * `BLOCKCHAIN` — blockchain name: `ETHEREUM`, `FLOW`, `TEZOS`, `POLYGON` or `SOLANA`
    * `TS_MS` — timestamp of the `data` in ms
    * `ENTITY_ID` — entity identifier, different blockchains have different identifier formats

For example:

```shell
POLYGON:1649395092000_624fc5956f6dc654e6095b90;ETHEREUM:1649395762000_624fc83a63c052298d2e2b61;SOLANA:1649395777000_000126563148:EjGVpJkNpjCakf5WcN13b8rZzxvDAnjVm7mgLam812xm:000185:4fGmEP5Cm3MURsGJ8mx1uEC7c2sWsVrAGdjC2PfCbamj5ZKZwwCRYTUWyoY3Yzo3JYr5TGqJEUnmB6ejFPChTNKJ:000000:000001;TEZOS:1649260825000_BMQpZgFjvunjfqe7JPbRihLxrAv89vR9wtaHBpf8H6FULqXQM6o_243;FLOW:1649159220612_a4a4ad0e64aa0a3e6820f8a546d9355045eb1ca2f4818b85f5c0085f8cae04b9.64
```

If the blockchain is not specified in the `cursor`, then no entries have been found for it according to the sorting results.

To get the next page of results, set `cursor` returned by a previous list request. But we recommend using the cursor in automated mode, because it is not designed to be built by hand.

If you still want to use it manually, use the following example to get the correct data.

??? example "getAllActivities example"

    [`https://api.rarible.org/v0.1/activities/all`](https://multichain-api.rarible.org/testnet/tag/activity-controller#operation/getAllActivities)
    
    1. Specify the query parameters: `blockchains`, activity `type`, and `size`:

        ```shell
        curl --request GET 'https://api.rarible.org/v0.1/activities/all?blockchains=ETHEREUM&type=MINT&size=3'
        ```
        
        Example response (status 200)
        
        ```json
        {
            "continuation": "1649398291000_624fd21b63c052298d2e43f9",
            "cursor": "ETHEREUM:1649398291000_624fd21b63c052298d2e43f9",
            "activities": [
                {
                    "@type": "MINT",
                    "id": "ETHEREUM:624fd23963c052298d2e4407",
                    "date": "2022-04-08T06:12:02Z",
                    "reverted": false,
                    "owner": "ETHEREUM:0x33b5606763150120076308076c91f01132a799da",
                    "contract": "ETHEREUM:0x2703b3753930fe36b5af2b9b6cba1615fdf31310",
                    "tokenId": "2",
                    "itemId": "ETHEREUM:0x2703b3753930fe36b5af2b9b6cba1615fdf31310:2",
                    "value": "1",
                    "transactionHash": "0x74fd40687d29f2ac584c14b46ad871d82e0fbe3332a2679370b1117c4fac0e57",
                    "blockchainInfo": {
                        "transactionHash": "0x74fd40687d29f2ac584c14b46ad871d82e0fbe3332a2679370b1117c4fac0e57",
                        "blockHash": "0xbd49cf6e7aad7c7e693ea675048033bfdfdea9665374de27283ee045ba7c9b91",
                        "blockNumber": 10467061,
                        "logIndex": 21
                    }
                },
                {
                    "@type": "MINT",
                    "id": "ETHEREUM:624fd23963c052298d2e4406",
                    "date": "2022-04-08T06:12:02Z",
                    "reverted": false,
                    "owner": "ETHEREUM:0xd4f6cb0c1fe07407b7098ac7fe4265f3b2ae61f2",
                    "contract": "ETHEREUM:0x1e1e3fed3e83dfe729a29ace3b588169a586fd18",
                    "tokenId": "1",
                    "itemId": "ETHEREUM:0x1e1e3fed3e83dfe729a29ace3b588169a586fd18:1",
                    "value": "1",
                    "transactionHash": "0xa47279f35076d084a5bfa5abd4de71a3226d5b5f7424ceaa52fa81d179a2b8d6",
                    "blockchainInfo": {
                        "transactionHash": "0xa47279f35076d084a5bfa5abd4de71a3226d5b5f7424ceaa52fa81d179a2b8d6",
                        "blockHash": "0xbd49cf6e7aad7c7e693ea675048033bfdfdea9665374de27283ee045ba7c9b91",
                        "blockNumber": 10467061,
                        "logIndex": 0
                    }
                },
                {
                    "@type": "MINT",
                    "id": "ETHEREUM:624fd21b63c052298d2e43f9",
                    "date": "2022-04-08T06:11:31Z",
                    "reverted": false,
                    "owner": "ETHEREUM:0x739cc4746e106d050f757bcece2aafc9f2eaaa28",
                    "contract": "ETHEREUM:0x25b284f96106bb046b9bd99ab167f060bcf18982",
                    "tokenId": "10",
                    "itemId": "ETHEREUM:0x25b284f96106bb046b9bd99ab167f060bcf18982:10",
                    "value": "1",
                    "transactionHash": "0x990b3b2157dad093de018da254fc52adbd89737c72cbd1a443253897a74a4161",
                    "blockchainInfo": {
                        "transactionHash": "0x990b3b2157dad093de018da254fc52adbd89737c72cbd1a443253897a74a4161",
                        "blockHash": "0xe5b01f69dba978cb52907a6d12938550fcab5bac1572c9d7ca5c7fab30d32c84",
                        "blockNumber": 10467059,
                        "logIndex": 6
                    }
                }
            ]
        }
        ```
        
        As we see, `ENTITY_ID` part in the `cursor` is the same as `id` of the last element in the response:
        
        ```json
        {
            ...
            "cursor": "ETHEREUM:1649398291000_624fd21b63c052298d2e43f9",
            "activities": [
                {
                ...
                {
                    ...
                    "id": "ETHEREUM:624fd21b63c052298d2e43f9",
                    ...
                    }
                }
            ]
        }
        ```

    2. Take the resulting `cursor` and add it to the new query:

        ```shell
        curl --request GET 'https://api.rarible.org/v0.1/activities/all?blockchains=ETHEREUM&type=MINT&cursor=ETHEREUM:1649398291000_624fd21b63c052298d2e43f9&size=3'
        ```
        
        Example response (status 200)
        
        ```json
        {
            "cursor": "ETHEREUM:1649398276000_624fd20e63c052298d2e42f6",
            "activities": [
                {
                    "@type": "MINT",
                    "id": "ETHEREUM:624fd20f63c052298d2e43e3",
                    "date": "2022-04-08T06:11:16Z",
                    "reverted": false,
                    "owner": "ETHEREUM:0x77054b00ddbbe9c597d93156b964fc115dbc1685",
                    "contract": "ETHEREUM:0xce92876be6f0e6c795d55aca4eec1986c6db35eb",
                    "tokenId": "1011",
                    "itemId": "ETHEREUM:0xce92876be6f0e6c795d55aca4eec1986c6db35eb:1011",
                    "value": "1",
                    "transactionHash": "0xf6cd37b1ce91f16b0f4a1dce86e78d59b4cba6ad7352eaa15cb6fc32c853362a",
                    "blockchainInfo": {
                        "transactionHash": "0xf6cd37b1ce91f16b0f4a1dce86e78d59b4cba6ad7352eaa15cb6fc32c853362a",
                        "blockHash": "0xc5a24c1dc49b5551b06f805edb4dd782cd46b3f21de71d3b250de6d767a625d9",
                        "blockNumber": 10467058,
                        "logIndex": 508
                    }
                },
                {
                    "@type": "MINT",
                    "id": "ETHEREUM:624fd20f63c052298d2e43e2",
                    "date": "2022-04-08T06:11:16Z",
                    "reverted": false,
                    "owner": "ETHEREUM:0x77054b00ddbbe9c597d93156b964fc115dbc1685",
                    "contract": "ETHEREUM:0xce92876be6f0e6c795d55aca4eec1986c6db35eb",
                    "tokenId": "1012",
                    "itemId": "ETHEREUM:0xce92876be6f0e6c795d55aca4eec1986c6db35eb:1012",
                    "value": "1",
                    "transactionHash": "0xf6cd37b1ce91f16b0f4a1dce86e78d59b4cba6ad7352eaa15cb6fc32c853362a",
                    "blockchainInfo": {
                        "transactionHash": "0xf6cd37b1ce91f16b0f4a1dce86e78d59b4cba6ad7352eaa15cb6fc32c853362a",
                        "blockHash": "0xc5a24c1dc49b5551b06f805edb4dd782cd46b3f21de71d3b250de6d767a625d9",
                        "blockNumber": 10467058,
                        "logIndex": 507
                    }
                },
                {
                    "@type": "MINT",
                    "id": "ETHEREUM:624fd20e63c052298d2e42f6",
                    "date": "2022-04-08T06:11:16Z",
                    "reverted": false,
                    "owner": "ETHEREUM:0x0ade6d84cb1b8fe9ab8c8145f53b202c426a34f3",
                    "contract": "ETHEREUM:0x4fc8df260a04683421d3949baf182f9556f3a9f9",
                    "tokenId": "2",
                    "itemId": "ETHEREUM:0x4fc8df260a04683421d3949baf182f9556f3a9f9:2",
                    "value": "1",
                    "transactionHash": "0xbf231cf9a46ff83484eb39ac73c1d4a806e8376a19fc3c6549d7777c186cd2b3",
                    "blockchainInfo": {
                        "transactionHash": "0xbf231cf9a46ff83484eb39ac73c1d4a806e8376a19fc3c6549d7777c186cd2b3",
                        "blockHash": "0xc5a24c1dc49b5551b06f805edb4dd782cd46b3f21de71d3b250de6d767a625d9",
                        "blockNumber": 10467058,
                        "logIndex": 17
                    }
                }
            ]
        }
        ```    

    Repeat this step with the newly obtained `cursor`, if necessary.

On the [multichain-api.rarible.org](https://multichain-api.rarible.org) you can find more information about Protocol Multichain API.
