---
title: ExchangeV2 Sell and Bid
description: The main information about Sell and Bid in Rarible Smart Contracts
---

# ExchangeV2 Sell and Bid

## Sell Order

To create a Sell Order, use the Ethereum SDK:

1. Check that the exchange contract can dispose of assets, tokens. Call setApprovalForAll if necessary.
2. Create a signature:
    1. [Encrypt the order for signing](https://github.com/rarible/ethereum-sdk/blob/master/packages/sdk/src/order/encode-data.ts ).
    2. [Sign the order](https://github.com/rarible/ethereum-sdk/blob/master/packages/sdk/src/order/sign-order.ts).
3. Send the signed order to the API.

[Example of creating a Sell Order in SDK.](https://github.com/rarible/ethereum-sdk#create-sell-order)

## Bid

To make a purchase or accept a Bid, send a transaction to the matchOrders function of the contract [ExchangeV2](https://github.com/rarible/protocol-contracts/blob/master/exchange-v2/contracts/ExchangeV2Core.sol).

matchOrders function has parameters:

* left order
* left order signature
* right order
* right order signature

[Example of creating a Bid in SDK.](https://github.com/rarible/ethereum-sdk#create-bid)
