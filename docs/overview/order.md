---
title: Sell NFTs with Rarible Protocol
description: The main information about selling NFTs in Rarible Multichain Protocol
---

# Sell NFTs

When you have your NFT created, there is a high chance that you will want to sell it. Or try at least. You can Sell NFTs with Rarible Multichain Protocol in different blockchains.

## Preparation

1. [Install and configure](https://docs.rarible.org/union-sdk/#installation) Protocol SDK.
2. [Connect the required wallet](https://docs.rarible.org/union-sdk/#metamask-integration-with-rarible).
3. [Mint NFT](mint.md).

## List NFT for sale

To list your NFT for sale, you'll need a token address, the one you get back from

```typescript
await mintResponse.submit();
```

If you want to create a sell order immediately after lazy minting your token, you can use the `mintAndSell` function.

It's pretty straightforward. All we need is:

* `tokenMultichainAddress:` — string in `BLOCKCHAIN:CONTRACT_ADDRESS:TOKEN_ID` format, see code for example
* `price: number` — price in ETH for which we want to list the token (disclaimer: it's not in wei, it's in ETH, so 0.5 equals 0.5 ETH)
* `amount: number` — quantity of NFT we want to list. In case of ERC721 it's 1
* `currency` — type of currency: `FlowAssetTypeNft | TezosXTZAssetType | EthErc20AssetType` etc. you can find all supported currencies `@rarible/api-client/build/models/AssetType` in node modules

```typescript
// 1. Examplary values
const tokenMultichainAddress: string =
  "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382052";
const ethCurrency: EthEthereumAssetType = {
  "@type": "ETH",
};
const price: number = 1;
const amount: number = 1;

// 2. Create PreapreOrderRequest type object and pass it to sdk.order.sell
const orderRequest: PrepareOrderRequest = {
  itemId: toItemId(tokenMultichainAddress),
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

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
