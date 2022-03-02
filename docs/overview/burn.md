---
title: Burn NFTs in Rarible Protocol
description: The main information about burning NFTs in Rarible Multichain Protocol
---

# Burn

You can burn NFTs with Rarible Multichain Protocol in different blockchains.

## Preparation

1. [Install and configure](https://docs.rarible.org/union-sdk/#installation) Protocol SDK.
2. [Connect the required wallet](https://docs.rarible.org/union-sdk/#metamask-integration-with-rarible).

## Burn NFTs

Burning tokens is equivalent to sending them to address 0x0 because nobody has a private key for that.

To burn NFTs create `PrepareBurnRequest` and get `sdk.nft.burn()`:

```typescript
const itemId =
  "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382052";

const burnRequest: PrepareBurnRequest = {
  itemId: toItemId(itemId),
};

const burnResponse = await sdk.nft.burn(burnRequest);

const response = await burnResponse.submit();
```

* `itemId` — ItemID of your NFT in format `${blockchain}:${token}:${tokenId}`. Supported blockchains: `ETHEREUM`, `POLYGON`, `TEZOS`, `FLOW`.

    For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:1`
