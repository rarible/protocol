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

## Matching Orders

Direct purchase of the item for sale is currently available. This means that you cannot bid on purchasing the item yet. But you can purchase an item for the amount the owner estimates the item.

The purchase can be divided into several stages:

* Submit an item for sale
* Purchase of an item

### Listing an item for sale

To list an item for sale, the seller has to:

* Select the item
* Indicate its cost

For more information, see [Rarible Protocol Flow SDK](flow-sdk.md#create-sell-order).

At the moment of placing an item for sale in a smart contract, all payments are calculated and recorded.

A smart contract implements such types of payments as:

* Commission for the sale of an item — it's 2.5% of the item's value, which the seller set. The seller pays the commission.
* Commission for the purchase of the item — it's 2.5% of the item's value, which the seller set. The buyer pays the commission.
* Royalties — are paid on the item's value as determined by the seller.
* Payment to the seller — the remainder of the item's value, minus the item's sale commission and royalties.

Thus, the seller, putting up an item with a royalty of 10% for sale for 100 FLOW, will receive 87.5 FLOW as he pays: 2.5 FLOW commissions and 10 FLOW royalties after the sale.

The buyer under the same conditions will purchase the item for 102.5 FLOW, where 2.5 FLOW will be counted as a commission.

!!! note ""

    If, after placing an item for sale, the item is transferred to another user or destroyed, the smart contract will automatically remove the item from the sale.

### Buying an item

The buyer needs to provide the order ID and the item owner to buy an item. During the execution of the transaction, the buyer must have sufficient funds to purchase the item.

For more information, see [Rarible Protocol Flow SDK](flow-sdk.md#buy-an-item).

### Coming soon

Soon we will implement the following features:

* Put an item up for auction
* Place a bid on an item
* Accept a bid
