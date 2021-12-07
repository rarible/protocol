# API and Indexer Overview

API and Indexer main functions:

- Follow the blockchain
- Handle read requests
- Process creation requests

## Architecture

The Rarible Protocol Ethereum Indexer consists of the following parts:

- [NFT indexer](https://github.com/rarible/ethereum-indexer/blob/master/nft) — aggregates NFTs data
- [ERC-20 indexer](https://github.com/rarible/ethereum-indexer/blob/master/erc20) — aggregates data about ERC-20 tokens and balances
- [Order indexer](https://github.com/rarible/ethereum-indexer/blob/master/order) — aggregates Orders data from different platforms

Each Indexer listens to a specific part of the Ethereum blockchain. Users can use Indexers to request data about the state of the blockchain.

Indexers generate events when the state changes. They are developed with Spring Framework and use these external services:

- MongoDB — main data storage
- Apache Kafka — event handling

![](../img/eth_6.png)

## Controllers

1. To create or modify NFTs and search information about them:
   1. nft-transaction-controller
   2. nft-lazy-mint-controller
   3. nft-activity-controller
   4. nft-ownership-controller
   5. nft-item-controller
   6. nft-collection-controller
2. To create or modify orders and search information about them:
   1. order-signature-controller
   2. order-encode-controller
   3. order-controller
   4. order-transaction-controller
   5. order-activity-controller
   6. order-aggregation-controller
   7. nft-order-ownership-controller
   8. nft-order-item-controller
   9. nft-order-activity-controller
   10. nft-order-collection-controller
3. Additional controllers:
   1. gateway-controller
   2. erc20-balance-controller
   3. erc20-token-controller
   4. lock-controller

## API usage Examples

* [Search Items](search-items.md)
* [Search Orders](search-orders.md)
* [Create Lazy Minting](create-lazy-minting.md)
* [Create Orders](create-orders.md)
