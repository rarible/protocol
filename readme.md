# Rarible Protocol Overview

Rarible protocol combines smart contracts for minting, exchanging tokens, APIs for order creation, discovery, standards used in smart contracts.

Rarible pursues the goal of creating a highly liquid environment for all NFTs out there: a robust on-chain protocol designed for NFTs to exist in a connected space. A separate initiative with a dedicated team will enable direct interactions with the protocol from multiple front ends like storefronts or wallets, offering additional distribution channels and enhancing liquidity. It will also fuel the discovery of new NFT trading mechanics.

NFT protocol designed by Rarible for all, owned and governed by the community. In this regard, a special place in the initiative is reserved for Rarible native governance token $RARI as the basic building block for the future NFT ecosystem.

## Why build on Rarible protocol?

1. **Supply and demand of the whole Rarible ecosystem** Rarible is one of the biggest NFT marketplaces out there with over $64 million in total lifetime volume and 57k monthly protocol users, slick UX, and a variety of use cases across industries. You can utilize the shared order book with Rarible.
2. **Advanced & robust tech done for you** Creating the tech from scratch is hard and time-consuming. Rarible provides access to the tools that the team has been developing for the past 1,5 years with wide functionality and data on all the NFTs created.
3. **Monetization**  Rarible protocol enables arbitrary front-end fees: you can additionally monetize your creations.
4. **DAO**  Rarible is steadily moving towards becoming a fully decentralized autonomous organization. The DAO will offer multiple opportunities for creators to get funding and exposure. It will incentivize people to build on top of the protocol, and we expect the DAO to reward the early builders.

## Protocol Features

Rarible's protocol includes contracts, standards, and APIs for:

**Minting**

* Minting \(Both ERC721 & ERC1155\)
* Lazy Minting - Token metadata & minting signatures are stored on Rarible back-end until a buyer fills the order. Then a `mintAndTransfer` call is made on chain when the order is filled

**Exchange** \(Buy, Sell, Bid\)

* Signature based order matching using an off chain order book
* Asset discovery is off chain, then buyers or sellers can submit both sides of an order, including relevant signatures to execute a transfer.
* Asset owners must `approve` the Rarible exchange to transfer on their behalf
* Multiple asset types are supported to fill orders \(ERC721, ERC1155, ERC20\)
* Bidding is supported

**Indexer**

* Rarible API exposes ways to query NFTs indexed on Ethereum
* Rarible API exposes ways to create orders
* Source code of the indexer is available at [https://github.com/rarible/ethereum-indexer](https://github.com/rarible/ethereum-indexer)

## Getting Started

1. Example App
2. Use cases

## Blockchains

1. [Ethereum](ethereum/ethereum-overview.md)
2. ...
3. ...
