---
title: Rarible Protocol Flow
description: Rarible Protocol integrated with Flow * fast, decentralized, and developer-friendly blockchain
---

# Rarible Protocol Flow

## Overview

Rarible Protocol Flow combines smart contracts for minting, exchanging tokens, APIs for order creation, discovery, standards used in smart contracts.

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
    * Provides ways to query NFT for contracts that you want to monitor.
    * Exposes ways to create orders.

## Smart Contracts

Here you can find Rarible Smart Contracts deployed instances across Flow Testnet and Mainnet.

| Smart Contract | Mainnet                                                                         | Testnet                                                                                                                                   |
|:---------------|:--------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------|
| RaribleNFT | [A.01ab36aaf654a13e.RaribleNFT](https://flowscan.org/contract/A.01ab36aaf654a13e.RaribleNFT) | [A.ebf4ae01d1284af8.RaribleNFT](https://testnet.flowscan.org/contract/A.ebf4ae01d1284af8.RaribleNFT)                                      |
| RaribleOrder | [A.01ab36aaf654a13e.RaribleOrder](https://flowscan.org/contract/A.01ab36aaf654a13e.RaribleOrder) | [A.ebf4ae01d1284af8.RaribleOrder](https://testnet.flowscan.org/contract/A.ebf4ae01d1284af8.RaribleOrder)                                  |
| RaribleFee | [A.336405ad2f289b87.RaribleFee](https://flowscan.org/contract/A.336405ad2f289b87.RaribleFee) | [A.ebf4ae01d1284af8.RaribleFee](https://testnet.flowscan.org/contract/A.ebf4ae01d1284af8.RaribleFee)                                      |
| LicensedNFT | [A.01ab36aaf654a13e.LicensedNFT](https://flowscan.org/contract/A.01ab36aaf654a13e.LicensedNFT) | [A.ebf4ae01d1284af8.LicensedNFT](https://testnet.flowscan.org/contract/A.ebf4ae01d1284af8.LicensedNFT)                                    |

For more information, see [Rarible Protocol Flow Smart Contracts](https://github.com/rarible/flow-contracts) repo on GitHub.

## API Reference

--8<-- "docs/snippets/subject-to-change-api.md"

Use these base URLs to access our API on different Flow networks:

| Base URL                                                                               | Network |
|:---------------------------------------------------------------------------------------|:--------|
| [https://flow-api.rarible.com/v0.1](https://flow-api.rarible.com/v0.1)                 | Mainnet |
| [https://flow-api-staging.rarible.com/v0.1](https://flow-api-staging.rarible.com/v0.1) | Testnet |
| [http://flow-api-dev.rarible.com/v0.1](http://flow-api-dev.rarible.com/v0.1)           | Testnet |

Flow API documentation can be found here:

* [Mainnet](https://flow-api.rarible.com/v0.1/doc)
* [Staging](https://flow-api-staging.rarible.com/v0.1/doc)
* [Development](http://flow-api-dev.rarible.com/v0.1/doc)

For more information, see [Flow Indexer](https://github.com/rarible/flow-nft-indexer) and [Flow OpenAPI](https://github.com/rarible/flow-protocol-api) repos on GitHub.

## SDK

Rarible Protocol Flow SDK enables applications to interact with Rarible Flow protocol easily.

With the Rarible Protocol Flow SDK, you can:

* Authenticate customer
* Logout customer
* Make regular mint
* Transfer tokens
* Burn tokens
* Create sell orders
* Cancel sell order
* Buy tokens for regular sell orders
* Sign user message
