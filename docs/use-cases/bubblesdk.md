---
title: Rarible SDK No-Code plugin for Bubble
description: You can now use the Rarible Protocol SDK and build your own NFT Marketplace without deep knowledge on how to code
---

# Rarible SDK No-Code plugin for Bubble

This plugin has been developed by [NovaBloq](https://novabloq.com/).

You can now use the Rarible Protocol SDK and build your own NFT Marketplace without deep knowledge on how to code. We have integrated the SDK in a no-code plugin for Bubble.io

You can use the SDK without any programming skills and build your own NFT Marketplace entirely without code.
We have integrated SDK into a no-code plugin for the biggest no-code platform [Bubble.io](https://bubble.io/).

[Link to the plugin](https://bubble.io/plugin/rarible-sdk---nft-marketplace-1627909974342x941739732723564500)

[Link to documentation](https://rarible.docs.ezcodeplugins.com)

[Demo page with available features](https://rarible-demo.bubbleapps.io/version-test)

`All examples are open source, you can see how it works from the inside.`

###  SDK supported features:

- ERC721 and ERC1155 supported
- Mint
- Lazy Mint (Buyer pays the fee)
- Custom Royalties
- Custom Origin Fees
- Create Order (Sell, Bid)
- Buy item
- Accept Bid
- Transfer an NFT to other wallet
- Cancel Order
- Burn
- Create Collection

### API supported features:

- Get Item Metadata
- Get Item Data
- Get Orders By Wallet
- Get Order By Hash
- Get NFT Ownership
- Get NFT Order Activities
- Get Order Activities By Item
- Get All NFT Items By Owner, Creator, Collection


### Supported chains: 
 - Ethereum: Mainnet, Rinkeby, Ropsten
 - Polygon: Mainnet,  Mumbai
 - Tezos: Mainnet/Hangzhounet

For any plugin/bubble related questions we have a separate thread on Bubble’s forum [here](https://forum.bubble.io/t/free-plugin-rarible-sdk-nft-marketplace-by-ezcode/172519).

Also, you can join our Web3 NoCode community on [Discord](https://discord.gg/GHSTa8H8Cb) where you can get help with the plugin and Bubble overall.


### How to use:

# Installation
1. Place the element Rarible SDK on the page
2. Make sure it is visible (not in a popup or a hidden group)
3. Select preferred network from the Environment Dropdown

Ready to go, see examples on how to integrate it in demo pages.

We are working on documentation and more demo pages.

# Wallet Type
This dropdown from the plugin element is used for indicating the type of wallet used to connect to your app. (Select the one that the user connected with).
The dropdown contains only the wallets that are supported by the plugin.

# How to use Tezos
- Select Tezos Environment from the dropdown (mainnet or testnet)
- Select Tezos for Wallet type
- Use actions Connect/Disconnect Tezos Wallet
- After connection, an event called "Tezos wallet Connected" will be triggered. The plugin will be ready to be used after that.

NFT Marketplaces being built with this plugin: 
- [one2all](https://one2all.io/)
