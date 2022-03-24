---
title: Create NFT Collection in Rarible Protocol
description: How to create NFT collection in Rarible Multichain Protocol
---

# Collection

You can Create NFT Collection with Rarible Multichain Protocol in different blockchains.

--8<-- "docs/snippets/preparation-sdk.md"

## Create collection

Use `createCollection` function:

```typescript
import { createRaribleSdk } from "@rarible/sdk"
import type { BlockchainWallet } from "@rarible/sdk-wallet/src"
import type { CreateCollectionRequest } from "@rarible/sdk/src/types/nft/deploy/domain"

async function createCollection(wallet: BlockchainWallet, collectionRequest: CreateCollectionRequest) {
	const sdk = createRaribleSdk(wallet, "dev")
	const result = await sdk.nft.createCollection(collectionRequest)
	await result.tx.wait()
	return result.address
}
```

Depending on blockchain type, in `collectionRequest` should pass the following parameters:

**Ethereum**

```typescript
const ethereumRequest: CreateCollectionRequest = {
  blockchain: Blockchain.ETHEREUM,
  asset: {
    assetType: "ERC721",
    arguments: {
      name: "name",
      symbol: "RARI",
      baseURI: "https://ipfs.rarible.com",
      contractURI: "https://ipfs.rarible.com",
      isUserToken: false,
    },
  },
}
```

**Tezos**

```typescript
const tezosRequest: CreateCollectionRequest = {
  blockchain: Blockchain.TEZOS,
  asset: {
    assetType: "NFT",
    arguments: {
      name: "My NFT collection",
      symbol: "MYNFT",
      contractURI: "https://ipfs.io/ipfs/QmTKxwnqqxTxH4HE3UVM9yoJFZgbsZ8CuqqRFZCSWBF53m",
      isUserToken: false,
    },
  },
}
```

* `blockchain` — blockchain type: `ETHEREUM` or `TEZOS`
* `assetType` — NFT collection type: `ERC721` or `ERC1155` for `ETHEREUM`, `NFT` or `MT` for `TEZOS`
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
