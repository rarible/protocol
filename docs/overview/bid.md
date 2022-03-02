---
title: Create and Accept Bids with Rarible Protocol
description: The main information about creating and accepting bids in Rarible Multichain Protocol
---

# Sell NFTs

You can Create and Accept Bids with Rarible Multichain Protocol in different blockchains.

## Preparation

1. [Install and configure](https://docs.rarible.org/union-sdk/#installation) Protocol SDK.
2. [Connect the required wallet](https://docs.rarible.org/union-sdk/#metamask-integration-with-rarible).
3. [Mint NFT](mint.md).
4. [List NFT for sale](order.md)

## Create a bid

If filling a sell order can be compared with taking something to the cash register and paying for it, bidding can be compared to seeing something you want, going up to the owner, and saying, "Hey, I want that, here's my offer."

In practice, it works in the same way. You can place your bid for any given NFT, even if there isn't any sell offer associated with it. It's up to the owner if they accept it or not.

You will need:

* `tokenMultichainAddress`
* `currency` — type of currency: `FlowAssetTypeNft | TezosXTZAssetType | EthErc20AssetType` etc. you can find all supported currencies `@rarible/api-client/build/models/AssetType` in node modules
* `price`
* `amount`

!!! note ""

    The contract in ethCurrency is NOT an ERC721 address which you can find [here](https://docs.rarible.org/ethereum/contract-addresses/).

    It's a WETH address. For different chains, they are as follow:

    * Mainnet: 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
    * Rinkeby / Ropsten: 0xc778417e063141139fce010982780140aa0cd5ab

```typescript
const tokenMultichainAddress =
  "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382052";
const currency: EthErc20AssetType = {
  "@type": "ERC20",
  contract: toContractAddress(
    // WETH address on Rinkeby/Ropsten testnets
    "ETHEREUM:0xc778417e063141139fce010982780140aa0cd5ab"
  ),
};

const price: number = 1;
const amount: number = 1;

const orderRequest: PrepareOrderRequest = {
  itemId: toItemId(tokenMultichainAddress),
};

const bidResponse = await sdk.order.bid(orderRequest);

const response = await bidResponse.submit({
  amount,
  price,
  currency,
});
```

## Update a bid

Similarly to updating a sell order, there is also a possibility to update a bid.  It can be only higher than the original bid order price.

You will need:

* `bidOrderId` — you can obtain it from `bidResponse.submit`
* `price`
* `updateBidRequest: PrepareOrderUpdateRequest`

```typescript
const bidOrderId =
  "ETHEREUM:0x27b554bdf22fe72e89f113e9523e8d8a75fb4477d455e100dc2bb132e7f51682";
const price: number = 2;

const updateBidRequest: PrepareOrderUpdateRequest = {
  orderId: toOrderId(bidOrderId),
};

const updateResponse = await sdk.order.bidUpdate(updateBidRequest);

const response = await updateResponse.submit({
  price,
});
```

## Cancel a bid

In order to cancel a bid, you need an `orderId`.

```typescript
const bidOrderId =
  "ETHEREUM:0x27b554bdf22fe72e89f113e9523e8d8a75fb4477d455e100dc2bb132e7f51682";

const cancelOrderRequest: CancelOrderRequest = {
  orderId: toOrderId(bidOrderId),
};

const cancelResponse = await sdk.order.cancel(cancelOrderRequest);
```

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
