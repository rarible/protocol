# ExchangeV2 Overview

ExchangeV2 is a smart contract for the decentralized exchange of any assets represented in the Ethereum blockchain (or EVM compatible).

To make an exchange two orders are required:

1. Sale Order — Created by the seller.
2. Purchase Order — Bid made by the buyer.

The exchange occurs if the two orders above match.

The general process of creating and executing an order is as follows:

1. The seller confirms that the exchange contract can dispose of their assets/tokens.
2. The seller creates and signs an order. Specifies the types and amounts of assets they want to receive in return.
3. The seller sends the order to the indexer.
4. The buyer sends an indexer request to get an order for a specific item or collection.
5. The buyer creates a bid.
1. If the order and bid are matched, an exchange takes place.
2. If the order and bid do not match, then the seller can accept the Bid or not. If it accepts, then an exchange takes place.

The order can be signed or not. The signature may be missing if the transaction is executed by the person who created this order.

![](../img/eth_2.png)

See more information about:

- [ExchangeV2 Matching Orders](exchangev2-matching-orders.md)
- [ExchangeV2 Sell and Bid](exchangev2-sell-bid.md)
- [ExchangeV2 Update and Cancel](exchangev2-update-cancel.md)
