

# Search Capabilities

## Controllers

signature-controller

currency-controller

item-controller

ownership-controller

order-controller

auction-controller

activity-controller

collection-controller

## API usage Examples

### Items

??? example "get Item by owner"

    Returns Item by owner
    
    [`https://api.rarible.org/v0.1/items/byOwner`](https://api.rarible.org/v0.1/doc#operation/getItemsByOwner)
    
    **Example request (staging)**
    
    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/items/byOwner?owner=ETHEREUM:0x66606fe12f319a8f781a9af35c3d061617ea642a&size=1'
    ```
    
    Request parameters:
    
    * `owner` — address of the item owner, has format `${blockchain}:${address}`. For example, `ETHEREUM:0x66606fe12f319a8f781a9af35c3d061617ea642a`
    
    **Example response (status 200)**

    ```json
    {
        "total": 1,
        "continuation": "1648125753039_0x08295565739cf720f2a61e5237815eacfad98c6a:2102",
        "items": [
            {
                "id": "ETHEREUM:0x08295565739cf720f2a61e5237815eacfad98c6a:2102",
                "blockchain": "ETHEREUM",
                "collection": "ETHEREUM:0x08295565739cf720f2a61e5237815eacfad98c6a",
                "contract": "ETHEREUM:0x08295565739cf720f2a61e5237815eacfad98c6a",
                "tokenId": "2102",
                "creators": [
                    {
                        "account": "ETHEREUM:0x66606fe12f319a8f781a9af35c3d061617ea642a",
                        "value": 10000
                    }
                ],
                "owners": [],
                "royalties": [],
                "lazySupply": "0",
                "pending": [],
                "mintedAt": "2022-03-24T12:42:33Z",
                "lastUpdatedAt": "2022-03-24T12:42:33.039Z",
                "supply": "1",
                "meta": {
                    "name": "捌：人海茫茫 #\n2102",
                    "description": "人海啊茫茫啊-《海草舞》NFT \n\n人海啊 茫茫啊 随波逐流 浮浮沉沉",
                    "attributes": [
                        {
                            "key": "演唱",
                            "value": "萧全"
                        },
                        {
                            "key": "作词",
                            "value": "萧全"
                        },
                        {
                            "key": "作曲",
                            "value": "萧全"
                        },
                        {
                            "key": "稀有度",
                            "value": "罕见"
                        }
                    ],
                    "content": [
                        {
                            "@type": "IMAGE",
                            "url": "https://rarible.mypinata.cloud/ipfs/QmbyFuDKZc9UkxMNJ7t25cZk7mm8u77c3FENFsatxN4VNk/8.png",
                            "representation": "ORIGINAL"
                        },
                        {
                            "@type": "IMAGE",
                            "url": "https://lh3.googleusercontent.com/t55AtJJ9szplBUbEchUAE_tyZuYTeSenjd7iHfVPfwsvIX3lof2kcI9jzGcpZ1Prf3oFiYLdcVsO0aFNCo-j6sgYUY0x32IEngz9s8I",
                            "representation": "BIG"
                        },
                        {
                            "@type": "IMAGE",
                            "url": "https://lh3.googleusercontent.com/t55AtJJ9szplBUbEchUAE_tyZuYTeSenjd7iHfVPfwsvIX3lof2kcI9jzGcpZ1Prf3oFiYLdcVsO0aFNCo-j6sgYUY0x32IEngz9s8I=s250",
                            "representation": "PREVIEW"
                        },
                        {
                            "@type": "VIDEO",
                            "url": "https://storage.opensea.io/files/cec338c0f5685f3037096b7bed283e15.wav",
                            "representation": "ORIGINAL"
                        }
                    ],
                    "restrictions": []
                },
                "deleted": false,
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
    
    **Example request (staging)**
    
    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/items/ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:19661880631107248865491477079747186145992059189823053172927066273904580362243'
    ```
    
    Request parameters:
    
    * `itemId` — Id of your NFT, has format `${blockchain}:${token}:${tokenId}`. For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:12345`
    
    **Example response (status 200)**

    ```json
    {
       "id": "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:19661880631107248865491477079747186145992059189823053172927066273904580362243",
       "blockchain": "ETHEREUM",
       "collection": "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82",
       "contract": "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82",
       "tokenId": "19661880631107248865491477079747186145992059189823053172927066273904580362243",
       "creators": [
          {
             "account": "ETHEREUM:0x2b783ae5b5b8a7a822449c7d8b6f35f9abc827f5",
             "value": 10000
          }
       ],
       "owners": [],
       "royalties": [],
       "lazySupply": "0",
       "pending": [],
       "mintedAt": "2022-03-09T22:48:33Z",
       "lastUpdatedAt": "2022-03-09T22:50:03.530Z",
       "supply": "1",
       "meta": {
          "name": "gbgbgbgbgbgb",
          "description": "",
          "attributes": [],
          "content": [
             {
                "@type": "IMAGE",
                "url": "https://rarible.mypinata.cloud/ipfs/QmQCp8bhbaPwGEuHeeR8pme2q3zuSjam2JEuFgAvp4DZsU/image.jpeg",
                "representation": "ORIGINAL",
                "mimeType": "image/jpeg",
                "size": 13311,
                "width": 640,
                "height": 640
             }
          ],
          "restrictions": []
       },
       "deleted": false,
       "auctions": [],
       "totalStock": "0",
       "sellers": 0
    }
    ```

??? example "get All Items"

    Returns All Items
    
    [`https://api.rarible.org/v0.1/items/all`](https://api.rarible.org/v0.1/doc#operation/getAllItems)
    
    **Example request (staging)**
    
    ```shell
    curl --request GET 'https://api.rarible.org/v0.1/items/all?blockchains=POLYGON&size=1'
    ```
    
    **Example response (status 200)**

    ```json
    {
        "total": 1,
        "continuation": "POLYGON:1648131545251_0x4d544035500d7ac1b42329c70eb58e77f8249f0f:3874767738",
        "items": [
            {
                "id": "POLYGON:0x4d544035500d7ac1b42329c70eb58e77f8249f0f:3874767738",
                "blockchain": "POLYGON",
                "collection": "POLYGON:0x4d544035500d7ac1b42329c70eb58e77f8249f0f",
                "contract": "POLYGON:0x4d544035500d7ac1b42329c70eb58e77f8249f0f",
                "tokenId": "3874767738",
                "creators": [
                    {
                        "account": "ETHEREUM:0x517c295d34137a2f4b3026656c09dd62e668fc72",
                        "value": 10000
                    }
                ],
                "owners": [],
                "royalties": [],
                "lazySupply": "0",
                "pending": [],
                "mintedAt": "2022-03-24T14:18:11Z",
                "lastUpdatedAt": "2022-03-24T14:19:05.251Z",
                "supply": "1",
                "meta": {
                    "name": "LOK Food 5M",
                    "description": "League of Kingdoms Resource",
                    "attributes": [],
                    "content": [
                        {
                            "@type": "IMAGE",
                            "url": "https://lok-nft.leagueofkingdoms.com/resource/10101020.png",
                            "representation": "ORIGINAL",
                            "mimeType": "image/png",
                            "width": 200,
                            "height": 200
                        }
                    ],
                    "restrictions": []
                },
                "deleted": false,
                "auctions": [],
                "totalStock": "0",
                "sellers": 0
            }
        ]
    }
    ```

### Orders

??? example "get Order by Id"

    Returns Order by Id

    [`https://api.rarible.org/v0.1/orders/{id}`](https://api.rarible.org/v0.1/doc#operation/getOrderById)

    **Example request (staging)**

    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/orders/ETHEREUM:0x1641f3a030a1e810abe15c70320ab0e4cf1ee59c0baa3a77cf8b409aa0a0d320'
    ```

    Request parameters:

    * `id` — order Id, has format `${blockchain}:${id}`. For example, `ETHEREUM:0x1641f3a030a1e810abe15c70320ab0e4cf1ee59c0baa3a77cf8b409aa0a0d320`

    **Example response (status 200)**

    ```json
    {
        "id": "ETHEREUM:0x1641f3a030a1e810abe15c70320ab0e4cf1ee59c0baa3a77cf8b409aa0a0d320",
        "fill": "0",
        "platform": "OPEN_SEA",
        "status": "INACTIVE",
        "startedAt": "2022-03-24T14:27:33Z",
        "endedAt": "2022-09-20T14:29:08Z",
        "makeStock": "0",
        "cancelled": false,
        "createdAt": "2022-03-24T14:29:15.790Z",
        "lastUpdatedAt": "2022-03-24T14:29:15.790Z",
        "makePrice": "0.01",
        "makePriceUsd": "30.198384450784797",
        "priceHistory": [
            {
                "date": "2022-03-24T14:29:15.790Z",
                "makeValue": "1",
                "takeValue": "0.01"
            }
        ],
        "maker": "ETHEREUM:0xe59072c5084ec2dc16e6bcdc3560802ffbafb5cb",
        "make": {
            "type": {
                "@type": "ERC1155",
                "contract": "ETHEREUM:0x88b48f654c30e99bc2e4a1559b4dcf1ad93fa656",
                "tokenId": "103834860413964016633619762390589326621035685084276300587330678503415507582977"
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
        "salt": "0xd49cbf21e348826dff4760cf9c22af9bd877809341ad0e5d0e899d60d8d59553",
        "signature": "0x45face93c43bdb3375e02b5140c4ec380a112b82c81fa78a5f6e7d15206d997629e5427476302f66cfae79488ca5591bc667de4c8847b56c81d90e2a76a9f8021c",
        "pending": [],
        "data": {
            "@type": "ETH_OPEN_SEA_V1",
            "exchange": "ETHEREUM:0xdd54d660178b28f6033a953b0e55073cfa7e3744",
            "makerRelayerFee": "1250",
            "takerRelayerFee": "0",
            "makerProtocolFee": "0",
            "takerProtocolFee": "0",
            "feeRecipient": "ETHEREUM:0x5b3256965e7c3cf26e11fcaf296dfc8807c01073",
            "feeMethod": "SPLIT_FEE",
            "side": "SELL",
            "saleKind": "FIXED_PRICE",
            "howToCall": "DELEGATE_CALL",
            "callData": "0x96809f90000000000000000000000000e59072c5084ec2dc16e6bcdc3560802ffbafb5cb000000000000000000000000000000000000000000000000000000000000000000000000000000000000000088b48f654c30e99bc2e4a1559b4dcf1ad93fa656e59072c5084ec2dc16e6bcdc3560802ffbafb5cb00000000000a9e00000000010000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000e00000000000000000000000000000000000000000000000000000000000000000",
            "replacementPattern": "0x000000000000000000000000000000000000000000000000000000000000000000000000ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
            "staticTarget": "ETHEREUM:0x0000000000000000000000000000000000000000",
            "staticExtraData": "0x",
            "extra": "0"
        }
    }
    ```

??? example "get Sell Orders by maker"

    Returns Sell Orders by maker

    [`https://api.rarible.org/v0.1/orders/sell/byMaker`](https://api.rarible.org/v0.1/doc#operation/getSellOrdersByMaker)

    **Example request (staging)**

    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/orders/sell/byMaker?maker=ETHEREUM:0xe59072c5084ec2dc16e6bcdc3560802ffbafb5cb&size=1'
    ```

    Request parameters:

    * `maker` — the maker of the order, has format `${blockchain}:${id}`. For example, `ETHEREUM:0xe59072c5084ec2dc16e6bcdc3560802ffbafb5cb`

    **Example response (status 200)**

    ```json
    {
        "continuation": "1648132919811_0xf8e3f895591ac3f6ff4a516ea17ac1c12b21c3d93acfa3e808e16f1467bb7c52",
        "orders": [
            {
                "id": "ETHEREUM:0xf8e3f895591ac3f6ff4a516ea17ac1c12b21c3d93acfa3e808e16f1467bb7c52",
                "fill": "0",
                "platform": "OPEN_SEA",
                "status": "INACTIVE",
                "startedAt": "2022-03-24T14:40:16Z",
                "endedAt": "2022-09-20T14:41:52Z",
                "makeStock": "0",
                "cancelled": false,
                "createdAt": "2022-03-24T14:41:59.811Z",
                "lastUpdatedAt": "2022-03-24T14:41:59.811Z",
                "makePrice": "0.01",
                "makePriceUsd": "30.198384450784797",
                "priceHistory": [
                    {
                        "date": "2022-03-24T14:41:59.811Z",
                        "makeValue": "1",
                        "takeValue": "0.01"
                    }
                ],
                "maker": "ETHEREUM:0xe59072c5084ec2dc16e6bcdc3560802ffbafb5cb",
                "make": {
                    "type": {
                        "@type": "ERC1155",
                        "contract": "ETHEREUM:0x88b48f654c30e99bc2e4a1559b4dcf1ad93fa656",
                        "tokenId": "103834860413964016633619762390589326621035685084276300587330678545196949438465"
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
                "salt": "0x0b06c99560930d99286981d16bdee68a8a10e872bc7718e662a144ab63eb854b",
                "signature": "0xee243d7bdb69518ea6c9c9cbfb4163e49111ec476b870f07c61c549b72927d332321ba1fceb1b2db7e26e4994a25fc18e0da2e729737deb8ae84f0c54c7f3d7c1c",
                "pending": [],
                "data": {
                    "@type": "ETH_OPEN_SEA_V1",
                    "exchange": "ETHEREUM:0xdd54d660178b28f6033a953b0e55073cfa7e3744",
                    "makerRelayerFee": "1250",
                    "takerRelayerFee": "0",
                    "makerProtocolFee": "0",
                    "takerProtocolFee": "0",
                    "feeRecipient": "ETHEREUM:0x5b3256965e7c3cf26e11fcaf296dfc8807c01073",
                    "feeMethod": "SPLIT_FEE",
                    "side": "SELL",
                    "saleKind": "FIXED_PRICE",
                    "howToCall": "DELEGATE_CALL",
                    "callData": "0x96809f90000000000000000000000000e59072c5084ec2dc16e6bcdc3560802ffbafb5cb000000000000000000000000000000000000000000000000000000000000000000000000000000000000000088b48f654c30e99bc2e4a1559b4dcf1ad93fa656e59072c5084ec2dc16e6bcdc3560802ffbafb5cb00000000000ac400000000010000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000e00000000000000000000000000000000000000000000000000000000000000000",
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

    **Example request (staging)**

    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/orders/all?size=1'
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

    **Example request (staging)**

    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/collections/byOwner?owner=ETHEREUM:0x8b3e026252ab4299d69779b4f533913e76a40420'
    ```

    Request parameters:

    * `owner` — address of the collection owner, has format `${blockchain}:${address}`. For example, `ETHEREUM:0x8b3e026252ab4299d69779b4f533913e76a40420`

    **Example response (status 200)**

    ```json
    {
        "total": 1,
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

??? example "get Collection by Id"

    Returns Collection by Id

    [`https://api.rarible.org/v0.1/collections/{collection}`](https://api.rarible.org/v0.1/doc#operation/getCollectionById)

    **Example request (staging)**

    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/collections/POLYGON:0x00000000004ba8d1691a4c215fd2bd99771dccc7'
    ```

    Request parameters:

    * `collection` — collection address, has format `${blockchain}:${address}`. For example, `POLYGON:0x00000000004ba8d1691a4c215fd2bd99771dccc7`

    **Example response (status 200)**

    ```json
    {
        "id": "POLYGON:0x00000000004ba8d1691a4c215fd2bd99771dccc7",
        "blockchain": "POLYGON",
        "type": "ERC721",
        "name": "LUCA",
        "symbol": "InvoiceNFT",
        "features": [
            "APPROVE_FOR_ALL"
        ],
        "minters": [],
        "meta": {
            "name": "Untitled",
            "content": []
        }
    }
    ```

??? example "get All Collections"

    Returns all Collections

    [`https://api.rarible.org/v0.1/collections/all`](https://api.rarible.org/v0.1/doc#operation/getAllCollections)

    **Example request (staging)**

    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/collections/all?blockchains=ETHEREUM&size=1'
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

    **Example request (staging)**

    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/ownerships/byItem?itemId=ETHEREUM:0x63ad270fc18f6f9435c3e205f06e003d3b861d33:765'
    ```

    Request parameters:

    * `itemId` — Id of your NFT, has format `${blockchain}:${token}:${tokenId}`. For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:12345`

    **Example response (status 200)**

    ```json
    {
        "total": 1,
        "ownerships": [
            {
                "id": "ETHEREUM:0x63ad270fc18f6f9435c3e205f06e003d3b861d33:765:0xe64ebc77ef72df8a7689d8928bc004b9e7ff43b3",
                "blockchain": "ETHEREUM",
                "itemId": "ETHEREUM:0x63ad270fc18f6f9435c3e205f06e003d3b861d33:765",
                "contract": "ETHEREUM:0x63ad270fc18f6f9435c3e205f06e003d3b861d33",
                "collection": "ETHEREUM:0x63ad270fc18f6f9435c3e205f06e003d3b861d33",
                "tokenId": "765",
                "owner": "ETHEREUM:0xe64ebc77ef72df8a7689d8928bc004b9e7ff43b3",
                "value": "1",
                "createdAt": "2022-03-24T16:20:05.015Z",
                "creators": [],
                "lazyValue": "0",
                "pending": []
            }
        ]
    }
    ```

??? example "get Ownerships by Id"

    Returns Ownerships by Id

    [`https://api.rarible.org/v0.1/ownerships/{ownershipId}`](https://api.rarible.org/v0.1/doc#operation/getOwnershipById)

    **Example request (staging)**

    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/ownerships/ETHEREUM:0x63ad270fc18f6f9435c3e205f06e003d3b861d33:765:0xe64ebc77ef72df8a7689d8928bc004b9e7ff43b3'
    ```

    Request parameters:

    * `ownershipId` — ownership Id in format `${blockchain}:${token}:${tokenId}:${owner}`. For example, `ETHEREUM:0x63ad270fc18f6f9435c3e205f06e003d3b861d33:765:0xe64ebc77ef72df8a7689d8928bc004b9e7ff43b3`

    **Example response (status 200)**

    ```json
    {
        "id": "ETHEREUM:0x63ad270fc18f6f9435c3e205f06e003d3b861d33:765:0xe64ebc77ef72df8a7689d8928bc004b9e7ff43b3",
        "blockchain": "ETHEREUM",
        "itemId": "ETHEREUM:0x63ad270fc18f6f9435c3e205f06e003d3b861d33:765",
        "contract": "ETHEREUM:0x63ad270fc18f6f9435c3e205f06e003d3b861d33",
        "collection": "ETHEREUM:0x63ad270fc18f6f9435c3e205f06e003d3b861d33",
        "tokenId": "765",
        "owner": "ETHEREUM:0xe64ebc77ef72df8a7689d8928bc004b9e7ff43b3",
        "value": "1",
        "createdAt": "2022-03-24T16:20:05.015Z",
        "creators": [],
        "lazyValue": "0",
        "pending": []
    }
    ```

For more information and examples, please check API documentation: [production](https://api.rarible.org/v0.1/doc), [staging](https://api-staging.rarible.org/v0.1/doc) and [development](https://api-dev.rarible.org/v0.1/doc).
