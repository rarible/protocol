---
title: Rarible Protocol Quick Start
description: Quick Start Guide for starting using Rarible Union Protocol SDK
---

# Quick Start

It's a Quick Start Guide for starting using Union SDK.

We will create ERC-721 Lazy Minting NFT and list it in the Ethereum network to start using Union SDK. To get more information, use the links in each section.

_WIP. It's the first Quick Start version._

## Installation

```shell
npm install -D @rarible/sdk
npm install web3
```

or using yarn

```shell
yarn add @rarible/sdk -D
yarn add web3
```

## Usage SDK

Create a project with the JS framework of your choice (we'll be using NextJS here).

To properly set up the Rarible SDK, we need to follow standard Web3 practices.

1. Grab the Ethereum object out of the global window object.
2. Use it to create a new instance of Web3.
3. Create a new instance of EthereumWallet class.
4. Create Rarible SDK with a new instance of ethereumWallet, created in the previous step.

In code, it looks like that (using TypeScript):

```typescript
// Imports
import Web3 from "web3";
import { createRaribleSdk } from "@rarible/sdk";
import { EthereumWallet } from "@rarible/sdk-wallet";

// Code
const { ethereum } = window as any;

const web3 = new Web3(ethereum);
const ethWallet = new EthereumWallet(ethereum);

const raribleSdk = createRaribleSdk(ethWallet, "staging");
```

In `createRaribleSdk`, we have several environment parameters:

* prod (mainnet)
* dev (ropsten)
* staging (rinkeby)
* e2e (you probably won't use this)

The difference between them is the chain Id and the Rarible API endpoint.

And if you're creating any blockchain application that will interact with users, you'll still need to implement the connect Metamask button to get their wallet connected.

See [Rarible Protocol Software Development Kit](https://github.com/rarible/sdk) repo on GitHub for more information about using SDK.

## Preprocessing Metadata

Let's use the preprocess function to prepare metadata for different blockchains.

```typescript
const blockchain = Blockchain.ETHEREUM;
const metadata: CommonTokenMetadata = {
  name: "Hey",
  description: undefined,
  image: undefined,
  animationUrl: undefined,
  externalUrl: undefined,
  attributes: [],
};
const request: PreprocessMetaRequest = {
  blockchain,
  ...metadata,
};
const response = sdk.nft.preprocessMeta(request);
```

See [Example of uploading & using Metadata with IPFS](../ethereum/metadata/ipfs-example.md) for more information about IPFS.

## Create Collection

There are several collection types:

* collection — can mint anyone
* user collection — can mint only owner, need `isUserToken: true`

You can use any public collection to mint and sell NFTs.

If you want to create your collection, you have to use the deploy function in Ethereum blockchain through the Union SDK. ERC-1155 and ERC-721 collections look the same.

```typescript
const ethereum = new Web3Ethereum({ web3: web3 }) //user web3 instance
const ethereumWallet = new EthereumWallet(ethereum)
const sdk = createRaribleSdk(ethereumWallet, "staging")
 await sdk.nft.deploy({
  blockchain: Blockchain.ETHEREUM,
  asset: {
   assetType: "ERC721",
   arguments: {
    name: "My own NFT collection",
    symbol: "RARI",
    baseURI: "https://ipfs.rarible.com",
    contractURI: "https://ipfs.rarible.com",
    isUserToken: false, // public collection
   },
  },
 })
```

## ERC-721 NFT Lazy Minting & Sell

Often users want to list their NFTs on the sale right after creation. For this case, use `mintAndSell` function, which allows you to do exactly that.

```typescript
const currentWallet = wallet as EthereumWallet;
const makerAccount = await currentWallet.ethereum.getFrom();
// Price in ETH
const price: number = 1;
const mintRequest: PrepareMintRequest = {
  collectionId: toContractAddress(
    "ETHEREUM:CONTRACT_ADDRESS"
  ),
};
const ethCurrency: EthErc20AssetType = {
  "@type": "ERC20",
  contract: toContractAddress(
    "ETHEREUM:CONTRACT_ADDRESS"
  ),
};
const mintResponse = await sdk.nft.mintAndSell(mintRequest);
const response = await mintResponse.submit({
  uri,
  supply: 1,
  lazyMint: true,
  price,
  creators: [
    {
      account: toUnionAddress(`ETHEREUM:${makerAccount}`),
      value: 10000,
    },
  ],
  currency: ethCurrency,
});
// Response:
// ItemId
// OrderId
```

See [ERC721-NFT Lazy Minting](../union-sdk/nft.md#erc721-nft-lazy-minting) and [List NFT on sell](../union-sdk/order.md#list-nft-on-sell) for more information.
