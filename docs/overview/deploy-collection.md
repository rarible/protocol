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

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
