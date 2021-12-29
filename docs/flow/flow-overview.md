---
title: Rarible Protocol Flow
description: Rarible Protocol integrated with Flow - fast, decentralized, and developer-friendly blockchain
---

# Rarible Protocol Flow

## Overview

Rarible Protocol Flow combines smart contracts for minting, exchanging tokens, APIs for order creation, discovery, standards used in smart contracts.

Rarible pursues the goal of creating a highly liquid environment for all NFTs out there: a robust on-chain protocol designed for NFTs to exist in a connected space. A separate initiative with a dedicated team will enable direct interactions with the protocol from multiple front ends like storefronts or wallets, offering additional distribution channels and enhancing liquidity. It will also fuel the discovery of new NFT trading mechanics.

Main features:

* Minting:
* Exchange (List, Sell/Buy):
    * On-chain mechanics of listing and buying items.
    * Safe removal of an item from the sale if the item has been moved or burned after being put up for sale.
    * Multiple asset types are supported to fill orders: [FT](https://docs.onflow.org/core-contracts/flow-token/) and [NFT](https://docs.onflow.org/core-contracts/fungible-token/).
    * Supported FT:
        * [FLOW](https://docs.onflow.org/core-contracts/flow-token/)
        * [FUSD](https://docs.onflow.org/fusd/transactions/)
        * [FT](https://docs.onflow.org/core-contracts/fungible-token/)
* Indexer:
    - Provides ways to query NFT for contracts that you want to monitor.
    - Exposes ways to create orders.

## Smart Contracts

Here you can find Rarible Smart Contracts deployed instances across Flow Testnet and Mainnet.

| Smart Contract | Base URL                                                                                                                                   | Network |
|:---------------|:-------------------------------------------------------------------------------------------------------------------------------------------|:-------:|
| RaribleNFT     | [https://flowscan.org/contract/A.01ab36aaf654a13e.RaribleNFT](https://flowscan.org/contract/A.01ab36aaf654a13e.RaribleNFT)                 | Mainnet |
| RaribleNFT     | [https://testnet.flowscan.org/contract/A.ebf4ae01d1284af8.RaribleNFT](https://testnet.flowscan.org/contract/A.ebf4ae01d1284af8.RaribleNFT) | Testnet |

For more information, see [Rarible Protocol Flow Smart Contracts](https://github.com/rarible/flow-contracts) repo on GitHub.

## API Reference

Use these base URLs to access our API on different Flow networks:

| Base URL                                                                                       |     Network     |
|:-----------------------------------------------------------------------------------------------|:---------------:|
| [https://flow-api.rarible.com/v0.1/doc](https://flow-api.rarible.com/v0.1/doc)                 |     Mainnet     |
| [https://flow-api-staging.rarible.com/v0.1/doc](https://flow-api-staging.rarible.com/v0.1/doc) | Testnet Rinkeby |
| [http://flow-api-dev.rarible.com/v0.1/doc](http://flow-api-dev.rarible.com/v0.1/doc)           | Testnet Ropsten |

For more information, see [Flow Indexer](https://github.com/rarible/flow-nft-indexer) and [Flow OpenAPI](https://github.com/rarible/flow-protocol-api) repos on GitHub.

## SDK

Rarible Protocol Flow SDK enables applications to interact with Rarible Flow protocol easily.

With the Rarible Protocol Flow SDK, you can:

- Authenticate customer
- Logout customer
- Make regular mint
- Transfer tokens
- Burn tokens
- Create sell orders
- Cancel sell order
- Buy tokens for regular sell orders
- Sign user message
