---
title: Rarible Protocol Quick Start
description: Quick Start Guide for starting using Rarible Protocol Multichain SDK
---

# Quick Start

It's a Quick Start Guide for starting using Multichain SDK.

We will create ERC-721 Lazy Minting NFT and list it in the Ethereum network to start using Multichain SDK. To get more information, use the links in each section.

## Installation

```shell
npm install -D @rarible/sdk
npm install web3@1.5.0
npm install tslib@2.3.1
```

or using yarn

```shell
yarn add @rarible/sdk -D
yarn add web3
yarn add tslib@2.3.1
```

Check that the SDK is installed correctly:

```shell
npm view @rarible/sdk version
```

## Using SDK

Create a project with the JS framework of your choice (we'll be using NextJS here).

To properly set up the Rarible SDK, we need to follow standard Web3 practices.

1. Grab the Ethereum object out of the global window object.
2. Use it to create a new instance of Web3.
3. Create a new instance of EthereumWallet class.
4. Create Rarible SDK with a new instance of ethereumWallet, created in the previous step.

In code, it looks like that (using TypeScript):

```typescript
--8<-- "docs/snippets/usage-sdk.md"
```

If using Ethers you should use @rarible/ethers-ethereum library for creating an EthereumWallet.
Here is an example of creating all supported providers:

```typescript
--8<-- "docs/snippets/usage-sdk-ethers.md"
```

In `createRaribleSdk`, we have several environment parameters:

* `prod` (mainnet)
* `testnet` (ropsten)

The difference between them is the chain Id and the Rarible API endpoint.

And if you're creating any blockchain application that will interact with users, you'll still need to implement the connect Metamask button to get their wallet connected.

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

See [Reference overview](../reference/reference-overview.md) page for more information about SDK usage.
