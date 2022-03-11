---
title: Deploy NFT Collection in Rarible Protocol
description: How to deploy NFT collection in Rarible Multichain Protocol
---

# Deploy Collection

You can Deploy NFT Collection with Rarible Multichain Protocol in different blockchains.

## Preparation

1. [Install and configure](https://docs.rarible.org/union-sdk/#installation) Protocol SDK.
2. [Connect the required wallet](https://docs.rarible.org/union-sdk/#metamask-integration-with-rarible).

## Deploy

To deploy collection get `sdk.nft.deploy()`:

```typescript
const deploy = await sdk.nft.deploy({
  blockchain: Blockchain.ETHEREUM,
  asset: {
    assetType: "ERC721",
    arguments: {
      name: "My Collection",
      symbol: "MYCOL",
      baseURI: "https://example.com",
      contractURI: "https://example.com",
      isUserToken: false
    }
  }
})  
```

* `blockchain` — blockchain type: `ETHEREUM`, `POLYGON`, `TEZOS`, `FLOW`
* `assetType` — NFT collection type: `ERC721` or `ERC1155`
* `name` — name of the collection
* `symbol` — symbol of the collection
* `baseURI` — prefix of the result of the tokenURI call
* `contractURI` — URI meta of the entire collection
* `isUserToken` — privat (true) or public (false) collection

## Checking created collection

To check the created collection:

* Use the `getCollectionById` [API method](https://api.rarible.org/v0.1/doc#operation/getCollectionById)

    ??? note "getCollectionById"

        Returns collection by address.
        
        `https://api.rarible.org/v0.1/collections/{collection}`
        
        **Example request (staging)**
        
        ```shell
        curl --request GET 'https://api-staging.rarible.org/v0.1/collections/all?blockchains=ETHEREUM&size=3'
        ```
        
        **Example response (status 200)**
    
        ```json
        {
            "total": 3,
            "continuation": "ETHEREUM:0x6ea0adbc173c7e8ca64c1ce881c1cfc161927876",
            "collections": [
                {
                    "id": "ETHEREUM:0x6ea0adbc173c7e8ca64c1ce881c1cfc161927876",
                    "blockchain": "ETHEREUM",
                    "type": "ERC721",
                    "name": "CryptoKitties",
                    "symbol": "CK",
                    "features": [],
                    "minters": []
                },
                {
                    "id": "ETHEREUM:0xaf2584a8b198f5d0b360b95d92aec852f7902e52",
                    "blockchain": "ETHEREUM",
                    "type": "CRYPTO_PUNKS",
                    "name": "CRYPTOPUNKS",
                    "symbol": "(Ͼ)",
                    "owner": "ETHEREUM:0xfb571f9da71d1ac33e069571bf5c67fadcff18e4",
                    "features": [],
                    "minters": []
                },
                {
                    "id": "ETHEREUM:0xd0200fa0a9c94484c7152813313b122e31bed99d",
                    "blockchain": "ETHEREUM",
                    "type": "ERC721",
                    "name": "CryptoKitties",
                    "symbol": "CK",
                    "features": [],
                    "minters": []
                }
            ]
        }
        ```

* Or check [Etherscan](https://etherscan.io/) for Ethereum and Polygon, [Flowscan](https://flowscan.org/) for Flow, or [tezblock](https://tezblock.io/) for Tezos.

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
