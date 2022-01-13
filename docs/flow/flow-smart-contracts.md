---
title: Rarible Flow Smart Contracts
description: Rarible Flow Smart Contracts for Flow overview
---

# Flow Smart Contracts Overview

Rarible Smart Contracts for Flow consist of:

* `RaribleFee` — fee manager that holds the rates and addresses fees.
* `LicensedNFT` — contract interface adds royalties to NFT. You can implement this `LicensedNFT` in your contract (along with [`NonFungibleToken`](https://github.com/onflow/flow-nft)), and your royalties will be taken when trading on [Rarible](https://rarible.com/).
* `RaribleNFT` — Rarible NFT contract that implements the [Flow NFT standard](https://github.com/onflow/flow-nft) is equivalent to ERC-721 or ERC-1155 on Ethereum.
* `RaribleOrder` — marketplace contract is the wrapper for the standard [NFTStorefront](https://github.com/onflow/nft-storefront) for handling market orders.

For more information, see [Rarible Protocol Flow Smart Contracts](https://github.com/rarible/flow-contracts) repo on GitHub.
