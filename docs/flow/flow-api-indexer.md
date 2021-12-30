---
title: Flow API and Indexer Overview
description: The main functions of the Rarible Protocol Flow API and indexer
---

# API and Indexer Overview

Rarible Protocol Flow NFT Indexer is a spring boot application for indexing [Flow](https://onflow.org) blockchain and API for reading NFT.

## Architecture

The Rarible Protocol Flow indexer consists of the following parts:

* Backend API — Flow API implementation
* Scanner — core indexing functionality

To read NFT events, we need to add `Subscriber` (see `com.rarible.flow.scanner.subscriber` package) with the event's description (usually contract name and event name) and start block height.

The service uses Kafka to exchange messages with other Rarible services.

The service also uses MongoDB as a persistence storage.

## Controllers

1. To create or modify NFTs and search information about them:

    * flow-nft-item-controller
    * flow-nft-ownership-controller
    * flow-nft-collection-controller

2. To create or modify orders and search information about them:

    * flow-order-controller
    * flow-nft-order-activity-controller
    * flow-nft-order-item-controller
    * order-aggregation-controller

3. Additional controllers:

    * flow-nft-crypto-controller

For more information, see [Flow Indexer](https://github.com/rarible/flow-nft-indexer) and [Flow OpenAPI](https://github.com/rarible/flow-protocol-api) repos on GitHub.
