---
title: Rarible Protocol Overview
description: Rarible Protocol is a blockchain-agnostic and decentralized tool to query, issue, and trade NFTs. How to make NFT marketplace
---

# Protocol Overview

Rarible Multichain Protocol is a decentralized toolset that simplifies the way developers can work with NFTs. Protocol builds an abstraction layer for several blockchains and isolates the developer from their specifics with Multichain SDK.

Rarible Multichain SDK is fully blockchain-agnostic. You can find a list of supported blockchains on our [Features](../features.md) page.

We use different environments for blockchain networks. See actual information on [API Reference](../api-reference.md) page.

[Rarible Multichain SDK](https://github.com/rarible/sdk) enables applications to easily interact with Rarible Protocol: query, issue and trade NFTs on any blockchain supported. See more information on [Reference](../reference/reference-overview.md) section.

**Know about NFTs**

Rarible Multichain Protocol indexes and provides via API wide information about NFTs. The following data is accessible for developer using protocol near real time it is put into blockchain:

* Basic NFT information
* Owner
* Creator
* Metadata
* NFT transactions

In addition to on-chain information, Rarible Multichain Protocol collects of-chain information like:

* Orders put for selling
* Bids put on NFTs
* Auctions information

**Multiple blockchains support**

Rarible Multichain Protocol is completely blockchain agnostic. Developers do not have to know details about a specific blockchain and can easily start with any of blockchains currently supported (see full list on [Features](../features.md) page).

**Decrease entrance level for developer**

Rarible Multichain protocol provides easy-to-use API that can be used with:

* Frontend application
* Backend server application
* Mobile app on IOS/Android/Huawei platform

No specific knowledge needed to start working with Rarible Multichain Protocol.

**Reliability and Performance**

Rarible Multichain Protocol provides high performance and reliable tools for developers. Smart-contracts for Rarible Multichain Protocol pass security audit before publishing. We are indexing data with small delay between it appear on a blockchain and moment when it is accessible with Protocol API, for most performant blockchains we sync data with up to 2 seconds delay from origin.

**Low Gas Consumption**

Rarible Multichain Protocol focused on optimizing usage costs for the users. For blockchains like Ethereum, where gas price is sufficient, we are doing a lot to minimize gas usage:

* Storing a considerable amount of up-to-date data off-chain - developers using our API to fetch NFT information do not pay the gas fee
* Providing Lazy-mint functionality that does not cost gas for minter
* Continuous smart contracts review and update, including on-chain auctions

**Advanced and robust tech done for you**

Creating the tech from scratch is complicated and time-consuming. Rarible provides access to the tools that the team has been developing for the past 1,5 years, with wide functionality and data on all the NFTs created.

**Monetization**

Rarible protocol enables arbitrary front-end fees: you can additionally monetize your creations.
