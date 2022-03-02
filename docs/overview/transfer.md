---
title: Transfer NFTs in Rarible Protocol
description: The main information about transferring NFTs in Rarible Multichain Protocol
---

# Transfer

You can transfer NFTs with Rarible Multichain Protocol in different blockchains.

## Preparation

1. [Install and configure](https://docs.rarible.org/union-sdk/#installation) Protocol SDK.
2. [Connect the required wallet](https://docs.rarible.org/union-sdk/#metamask-integration-with-rarible).
3. [Mint NFT](mint.md).

## Transfer NFTs

To transfer NFTs create `PrepareTransferRequest` and get `sdk.nft.transfer()`:

```typescript
const itemId =
  "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382052";

const transferRequest: PrepareTransferRequest = {
  itemId: toItemId(itemId),
};

const transferResponse = await sdk.nft.transfer(transferRequest);

const response = await transferResponse.submit({
  to: toMultichianAddress("ETHEREUM:0x79Ea2d536b5b7144A3EabdC6A7E43130199291c0"),
});
```

* `itemId` — ItemID of your NFT in format `${blockchain}:${token}:${tokenId}`. Supported blockchains: `ETHEREUM`, `POLYGON`, `TEZOS`, `FLOW`. 

    For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:1`
