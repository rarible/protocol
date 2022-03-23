---
title: Rarible Indexer Overview
description: What is a blockchain indexer, and how does Rarible implements it?
---

## What is an indexer?

It's nice to think that every service in the crypto space is fully decentralized. Of course, it isn't. Just imagine looking through the Ethereum blockchain for specific information. Right now i.e. 23.03.2022 the Ethereum blockchain size is almost 1 TB. It would be impossible to traverse that big chunk of a data in UX-friendly timeframe. That's why indexers originated. At the end of the day, what does indexing mean? It means to write data somewhere for later usage. In its essence indexer take the data which we're interested in from blockchain (most of the time, we're not interested in every specific transaction, just the ones connected to our dApp), and saves it in some sort of database. It can be SQL or NoSQL - it doesn't really matter. What matters is that now, we have some sort of structure, which we can travel fast and efficiently.

### Rarible

Now when we're conscious about indexer responsibilities and duty, we can lean over what types of indexers are used in Rarible.

On Rarible we have three different types of indexers implemented (which FYI are [opensourced](https://github.com/rarible/ethereum-indexer)):

- NFT Indexer,
- ERC20 Indexer,
- Order Indexer.

### NFT Indexer

NFT Indexer is used to index all history of NFTs related actions, i.e. mint, transfer and burn. Indexer gets logs from an Ethereum network, and accordingly creates NFT items in a NoSQL database. Especially it listens to a change of a state of an NFT item ownership.

### ERC20 Indexer

ERC20 is responsible for tracking user balances. If we would map it to the Rarible usage, it checks if a user has enough WETH (wrapped ETH) to make a bid. It handles all of the information about a user's wallet status.

### Order Indexer

In order to properly display order information (order means intent, e.g. intent to sell, or in simpler words, intent to sell an NFT for a given price), we need an order price in addition to other properties. That's where Order Indexer comes in. Listener catches logs which say e.g. if an order was executed, and what is the status of an order. It fetches order data from a few different places like OpenSea, Rarible OrderBook, or Cryptopunks.
