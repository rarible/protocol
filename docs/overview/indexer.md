---
title: Rarible Protocol Indexer
description: What is a blockchain indexer, and how does Rarible implement it
---

# Indexer

It's nice to think that every service in the crypto space is fully decentralized. Of course, it isn't. Just imagine looking through the Ethereum blockchain for specific information.

Right now, i.e. 23.03.2022 the Ethereum blockchain size is almost 1 TB. It would be impossible to traverse that big chunk of a data in UX-friendly timeframe. That's why indexers originated. At the end of the day, what does indexing mean? It means to write data somewhere for later usage.

In its essence, indexer take the data which we're interested in from blockchain (most of the time, we're not interested in every specific transaction, just the ones connected to our dApp), and saves it in some sort of database. It can be SQL or NoSQL — it doesn't really matter. What matters is that now, we have some sort of structure, which we can travel fast and efficiently.

## Rarible Multichain Indexer

Now, when we're conscious about indexer responsibilities and duty, we can lean over what types of indexers are used in Rarible.

On Rarible, we have three different types of indexers:

* NFT Indexer
* Token/Balance-Indexer
* Order Indexer

Additionally, in order for the services to work, we have a MongoDB instance, where all the indexed data from different blockchains sits, and a Multichain SDK API which allows for data traversing.

### NFT Indexer

NFT Indexer is used to index all history of NFTs related actions, i.e. mint, transfer and burn. Indexer gets logs from an Ethereum network, and accordingly creates NFT items in a NoSQL database. Especially, it listens to a change of a state of an NFT item ownership.

### Token/Balance-Indexer

Token/Balance-Indexer is responsible for tracking user balances. If we mapped it to the Rarible usage, it checks if a user has enough of a given currency to make a bid. It handles all the information about a user's wallet status.

### Order Indexer

In order to properly display order information (order means intent, e.g. intent to sell, or in simpler words, intent to sell an NFT for a given price), we need an order price in addition to other properties. That's where Order Indexer comes in.

Listener catches logs which say e.g. if an order was executed, and what is the status of an order. It fetches order data from a few different places like OpenSea, Rarible OrderBook, or Cryptopunks.

## How does the indexer gather the data?

It listens for specific events on a blockchain. Since every transaction and movement on a blockchain is emitted in a form of logs, and every log has its unique topic id, it can be explicitly identified.

Moreover, the indexer is also listening for block creation events. Listening from two sources simultaneously gives us the certainty that we will manage to catch all events we're interested in.

## What events do the indexer listen to?

Indexer listens mainly for transfer-type events. That's because almost all the NFT-related actions, including Minting, involve a transfer method, which creates an NFT (in that scenario we transfer the NFT from 0x0 address to the address of a creator).

From fetched logs, the indexer creates item and ownership objects that it stores in a database. It also tracks events for a specific collection (Rarible collection, etc.) from which it creates a token entity, and stores it in a database as well.

## Multichain abstraction

In order to be able to connect differently, not EVM based blockchains together, Rarible had to create a few different blockchain indexers. They all work based on the same principle, but since different blockchains like Tezos, Solana, Flow, have different architecture, they couldn't be simply merge.

But the merge could be abstracted, and that's what Rarible has done. It created a service called Union, and it works as a "really smart proxy" which allows you to use one API for all the blockchains. It takes all the Kafka proxy topics, from all the blockchains, and merges it into one topic. That's how you're able to get info from all the blockchains by using one Multichain API.
