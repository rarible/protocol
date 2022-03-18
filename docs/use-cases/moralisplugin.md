---
title: Moralis Rarible Plugin
description: Plugin enables interaction with Rarible, allowing anyone to lazy-mint an NFT and sell it
---

# Moralis Rarible Plugin

This plugin has been developed by the [Moralis](https://moralis.io) team.

* [For support, open a github issue](https://github.com/MoralisWeb3/plugindocs/issues)
* [Link to the plugin](https://moralis.io/plugins/rarible-nft-tools/)
* [Link to documentation](https://github.com/MoralisWeb3/plugindocs/tree/main/rarible%20plugin)

This plugin enables interaction with Rarible, allowing anyone to lazy-mint an NFT and sell it.

### Supported chains

This plugins works with 2 different blockchains:

* Ethereum Mainnet (‘eth’)
* Ethereum Rinkeby (‘rinkeby’)

### Supported tokens

* ERC721
* ERC1155

### SDK

Import the Moralis SDK in your project.

```html
<script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
<script src="https://npmcdn.com/moralis@latest/dist/moralis.js"></script>
```

### Lazy mint

You can lazy mint a token by calling the lazyMint endpoint. This endpoint returns an object that contains the tokenId and tokenAddress of the lazy minted token.

```js
await Moralis.Plugins.rarible.lazyMint({
  chain: 'rinkeby',
  userAddress: '0x7f64041298CC2C045FE5eb0e897ab7b5D4BdB4F3',
  tokenType: 'ERC1155',
  tokenUri: '/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp',
  supply: 100,
  royaltiesAmount: 5, // 0.05% royalty. Optional
})
```

You can also lazy mint a token and sell immediately. Below we are goin to lazy mint a token and create a sell order for it. In this example, we are selling 3 out of the 100 tokens created for 1 ETH (10 ** 18) each.

```js
await Moralis.Plugins.rarible.lazyMint({
  chain: 'rinkeby',
  userAddress: '0x7f64041298CC2C045FE5eb0e897ab7b5D4BdB4F3',
  tokenType: 'ERC1155',
  tokenUri: '/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp',
  supply: 100,
  royaltiesAmount: 5, // 0.05% royalty. Optional
  list: true, // Only if lazy listing
  listTokenAmount: 3, // Only if lazy listing
  listTokenValue: 10 ** 18, // Only if lazy listing
  listAssetClass: 'ETH', // only if lazy listing  || optional
})
```

### Sell order

You can create a sell order for a lazy minted token by calling the createSellOrder endpoint. In this example, we are selling 4 tokens created for 1 ETH (10 ** 18) each.

```js
await Moralis.Plugins.rarible.createSellOrder({
  chain: 'rinkeby',
  userAddress: '0xE78dC206875373B351EEF2D182025bb9a64d67B3',
  makeTokenId: '104734732573670734795292663651146618103387426131809974624560761860320187646009',
  makeTokenAddress: '0x1AF7A7555263F275433c6Bb0b8FdCD231F89B1D7',
  makeAssetClass: 'ERC1155',
  makeValue: '4',
  takeAssetClass: 'ETH',
  takeValue: 10 ** 18,
});
```

### ERC20

You can sell a lazy minted token for ERC20 instead of ETH. Make sure to specify the following parameters:

```js
takeAssetClass: 'ERC20',
takeTokenAddress: '0x5592ec0cfb4dbc12d3ab100b257153436a1f0fea', // DAI
```

Example:

```js
await Moralis.Plugins.rarible.createSellOrder({
  chain: 'rinkeby',
  userAddress: '0xE78dC206875373B351EEF2D182025bb9a64d67B3',
  makeTokenId: '104734732573670734795292663651146618103387426131809974624560761860320187646009',
  makeTokenAddress: '0x1AF7A7555263F275433c6Bb0b8FdCD231F89B1D7',
  makeAssetClass: 'ERC1155',
  makeValue: '4',
  takeAssetClass: 'ERC20',
  takeTokenAddress: '0x5592ec0cfb4dbc12d3ab100b257153436a1f0fea', // DAI
  takeValue: 10 ** 18,
});
```
