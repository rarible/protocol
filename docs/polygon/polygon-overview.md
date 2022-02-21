---
title: Rarible Protocol Polygon
description: Rarible Protocol Polygon is a set of tools to query, issue, and trade NFTs in the Polygon blockchain network
---

# Rarible Protocol Polygon

## Overview

Polygon is a decentralized Ethereum scaling platform that enables developers to build scalable, user-friendly dApps with low transaction fees without sacrificing security.

Main features:

* Supports all the existing Ethereum tooling
* Faster and cheaper transactions
* High throughput

## Smart Contracts

| Smart Contract         | Mainnet                                                                                                                  | Mumbai                                                                                                                          |
|:-----------------------|:-------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------|
| Exchange               | [0x835131b455778559CFdDd358eA3Fc762728F4E3e](https://polygonscan.com/address/0x835131b455778559CFdDd358eA3Fc762728F4E3e) | [0x4F05968D804902dd827Dd0F4fB37Ccc3071C4Bb5](https://mumbai.polygonscan.com/address/0x4F05968D804902dd827Dd0F4fB37Ccc3071C4Bb5) |
| Transfer Proxies       | [0xd47e14DD9b98411754f722B4c4074e14752Ada7C](https://polygonscan.com/address/0xd47e14DD9b98411754f722B4c4074e14752Ada7C) | [0x02e21199D043dab90248f79d6A8d0c36832734B0](https://mumbai.polygonscan.com/address/0x02e21199D043dab90248f79d6A8d0c36832734B0) |
| ERC-721 Token Factory  | [0x16911a36a56f828f17632cD4915614Dd5c7a45e0](https://polygonscan.com/address/0x16911a36a56f828f17632cD4915614Dd5c7a45e0) | [0xa85180a21786bA65b0778bE1cb5CBA5E5c6cD21d](https://mumbai.polygonscan.com/address/0xa85180a21786bA65b0778bE1cb5CBA5E5c6cD21d) |
| ERC-1155 Token Factory | [0xF46e8e6fA0F048DdD76F8c6982eBD059796298B8](https://polygonscan.com/address/0xF46e8e6fA0F048DdD76F8c6982eBD059796298B8) | [0xAa9CD5834E0009902EeAA3FEfAc6A160e9A096b4](https://mumbai.polygonscan.com/address/0xAa9CD5834E0009902EeAA3FEfAc6A160e9A096b4) |

To see more details about the smart contracts as well as their code, check the [Protocol Contracts](https://github.com/rarible/protocol-contracts) GitHub repo.

## API Reference

--8<-- "docs/snippets/subject-to-change-api.md"

Use these base URLs to access API on different Ethereum networks:

| Base URL                                                                                     | Network        |
|:---------------------------------------------------------------------------------------------|:---------------|
| [https://polygon-api.rarible.org/v0.1](https://polygon-api.rarible.org/v0.1)                 | Mainnet        |
| [https://polygon-api-staging.rarible.org/v0.1](https://polygon-api-staging.rarible.org/v0.1) | Mumbai Staging |
| [https://polygon-api-dev.rarible.org/v0.1](https://polygon-api-dev.rarible.org/v0.1)         | Mumbai Dev     |

Polygon API documentation can be found here:

* [Mainnet](https://polygon-api.rarible.org/v0.1/doc)
* [Staging](https://polygon-api-staging.rarible.org/v0.1/doc)
* [Development](https://polygon-api-dev.rarible.org/v0.1/doc)

## SDK

Polygon is using Ethereum SDK to interact with your application and the Rarible Protocol.

Main features:

* Create Mint and Lazy Minting ERC-721 and ERC-1155 tokens
* Create Sell Orders
* Create and accept Bid
* Buy tokens
* Transfer tokens
* Burn tokens

For more information on using the Rarible Protocol Ethereum SDK, see the page [Protocol Ethereum SDK](https://github.com/rarible/ethereum-sdk) on GitHub.
