---
title: Sell, Fill, Bid with Rarible Protocol SDK
description: Sell, Fill, and Bid operations with Rarible Protocol SDK
---

# Sell, Fill, Bid

When you have your NFT created, there is a high chance that you will want to sell it. Or try at least. The same way somebody may like your NFT, which is currently not for sale and create a bid for that. In this chapter, you can find cookbooks for all of that functionality.

## List NFT on sell

To list your NFT on sell, you'll need a token address, the one you get back from

```typescript
await mintResponse.submit();
```

If you want to create a sell order immediately after lazy minting your token, you can use the `mintAndSell` function.

It's pretty straightforward. All we need is:

* `tokenUnionAddress:` — string in `BLOCKCHAIN:CONTRACT_ADDRESS:TOKEN_ID` format, see code for example
* `price: number` — price in ETH for which we want to list the token (disclaimer: it's not in wei, it's in ETH, so 0.5 equals 0.5 ETH)
* `amount: number` — quantity of NFT we want to list. In case of ERC721 it's 1
* `currency` — type of currency: `FlowAssetTypeNft | TezosXTZAssetType | EthErc20AssetType` etc. you can find all supported currencies `@rarible/api-client/build/models/AssetType` in node modules

```typescript
// 1. Examplary values
const tokenUnionAddress: string =
  "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382052";
const ethCurrency: EthEthereumAssetType = {
  "@type": "ETH",
};
const price: number = 1;
const amount: number = 1;

// 2. Create PreapreOrderRequest type object and pass it to sdk.order.sell
const orderRequest: PrepareOrderRequest = {
  itemId: toItemId(tokenUnionAddress),
};

// You can extract info about properties from orderResponse e.g.
// 1. Base fee
// 2. Max Amount
// etc.
const orderResponse = await sdk.order.sell(orderRequest);

// 3. Submit the transaction -> it will pop up the metamask asking you to sign a transaction
const response = await orderResponse.submit({
  price,
  amount,
  currency: ethCurrency,
});
// We get order id from the response. It can be useful when we want to update sell order
```

## Update listed token price

To update the listed token price, you need a sell order id.

Due to security circumstances, you can't update the token price to higher than the one created in the original sell order. If you want to boost the price, you need to cancel the sell order and create a new one.

```typescript
const price: number = 0.8;
const ethCurrency: EthEthereumAssetType = {
  "@type": "ETH",
};

const orderId =
  "ETHEREUM:0x6e794fd04bcf21ee7f347874aefdf36ec1a7b73b5694760b367a7644765a6368";

const updateOrderRequest: PrepareOrderUpdateRequest = {
  orderId: toOrderId(orderId),
};

const updateResponse = await sdk.order.sellUpdate(updateOrderRequest);

const response = await updateResponse.submit({
  price,
});
```

## Fill sell order

Filling a sell order can be compared to paying for an object in a physical store. The sell order is the object being displayed, and filling would represent taking it to the cash register and paying for it.

In order to fill up a sell order, the only required data is orderId.

```typescript
const orderId: string = "ETHEREUM:0x6e794fd04bcf21ee7f347874aefdf36ec1a7b73b5694760b367a7644765a6368";

const fillRequest: PrepareFillRequest = {
  orderId: toOrderId(orderId);
};

const fillResponse = await sdk.order.fill(fillRequest);

const response = await fillResponse.submit({
  amount: 1 // Number of NFTs to buy
})

```

## Create a bid

If filling a sell order can be compared with taking something to the cash register and paying for it, bidding can be compared to seeing something you want, going up to the owner, and saying, "Hey, I want that, here's my offer."

In practice, it works in the same way. You can place your bid for any given NFT, even if there isn't any sell offer associated with it. It's up to the owner if they accept it or not.

You will need:

* `tokenUnionAddress`
* `currency` — type of currency: `FlowAssetTypeNft | TezosXTZAssetType | EthErc20AssetType` etc. you can find all supported currencies `@rarible/api-client/build/models/AssetType` in node modules
* `price`
* `amount`

!!! note ""

    The contract in ethCurrency is NOT an ERC721 address which you can find [here](https://docs.rarible.org/ethereum/contract-addresses/).

    It's a WETH address. For different chains, they are as follow:

    * Mainnet: 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2
    * Rinkeby / Ropsten: 0xc778417e063141139fce010982780140aa0cd5ab

```typescript
const tokenUnionAddress =
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
  itemId: toItemId(tokenUnionAddress),
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
