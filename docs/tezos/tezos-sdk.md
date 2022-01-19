---
title: Rarible Protocol Tezos SDK
description: Tezos SDK enables applications to interact with Protocol easily in the Tezos blockchain
---

# Tezos SDK

[Tezos SDK](https://github.com/rarible/tezos-sdk) enables applications to interact with Protocol easily in the Tezos blockchain and was built by [Functori](https://www.functori.com/).

SDK documentation can be found [here](https://tezos-paris-hub.gitlab.io/rarible/rarible-backend/)

## Installation

```
yarn
yarn build-all
```

## Usage

### Configure

In code it looks like that (using TypeScript):

```ts
const config = {
  exchange: "KT1ULGjK8FtaJ9QqCgJVN14B6tY76Ykaz6M8",
  transfer_proxy: "KT1Qypf9A7DHoAeesu5hj8v6iKwHsJb1RUR2",
  fees: new BigNumber(0),
  nft_public: "",
  mt_public: "",
  api: "https://tezos-hangzhou-api.rarible.org/v0.1",
  api_permit: "https://tezos-hangzhou-api.rarible.org/v0.1/",
  permit_whitelist: [],
  wrapper: 'KT1LkKaeLBvTBo6knGeN5RsEunERCaqVcLr9',
}

const tezos = in_memory_provider(
  'edskS4QxJFDSkHaf6Ax3ByfrZj5cKvLUR813uqwE94baan31c1cPPTMvoAvUKbEv2xM9mvtwoLANNTBSdyZf3CCyN2re7qZyi3',
  'https://tezos-hangzhou-node.rarible.org')
const provider = {
  tezos: tezos,
  config
}
```

### Deploy

```ts
const op = await deploy_nft_public(
  provider,
  await provider.tezos.address()
  )
await op.confirmation()
```

### Minting

```ts
const result = await mint(
  provider: Provider,
  contract: string,
  royalties : { [key: string]: BigNumber },
  supply?: BigNumber,
  token_id?: BigNumber,
  metadata?: { [key: string]: string },
  owner?: string,
)
```

### Burn

```ts
const arg = await burn(
  provider: Provider,
  asset_type: ExtendedAssetType,
  amount?: BigNumber
)
```

### Transfer

```ts
const arg = await transfer(
  provider: Provider,
  asset_type: ExtendedAssetType,
  to: string,
  amount?: BigNumber
)
```

### Sell

```ts
const sellOp = await sell(
  provider_seller,
  {
    maker: string,
    maker_edpk: string,
    make_asset_type: ExtendedAssetType
    amount: BigNumber
    take_asset_type: XTZAssetType | FTAssetType
    price: BigNumber
    payouts: Array<Part>
    origin_fees: Array<Part>
  }
)
```

### Bid

```ts
const bid = await bid(
  provider: Provider,
  {
    maker: string
    maker_edpk: string
    make_asset_type: XTZAssetType | FTAssetType
    amount: BigNumber
    take_asset_type: ExtendedAssetType
    price: BigNumber
    payouts: Array<Part>
    origin_fees: Array<Part>
  }
)
```
