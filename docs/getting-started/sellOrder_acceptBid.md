---
title: Create Sell Order and Accept Bid in Rarible Protocol
description: The main information about creating a sell order and accepting a bid, or in other words - putting your NFT on sale and accepting proposed offer from sombeody else.
---

# Create Sell Order and Accept Bid

After reading this piece of content you should have a knowledge about creating sell orders and accepting bids using Rarible Protocol.

## Preparation

1. [Install and configure](https://docs.rarible.org/union-sdk/#installation) Protocol SDK.
2. [Connect the required wallet](https://docs.rarible.org/union-sdk/#metamask-integration-with-rarible).

## Executing actions

You can use SDK to create (mint), trade, transfer, burn NFTs. All actions are handled in the same manner:

- Invoke function from SDK (e.g.: `mint`).
- Async function returns so-called `PrepareResponse` (it's different for different actions).
- `PrepareResponse` contains all needed information to show user a form (for example, response for sell contains all supported currency types).
- Collect input from the user (show form and let user enter the data).
- Pass this data to submit Action.

You can find more information about Action abstraction in dedicated [repo readme]. Or you can use it as a regular async function and work with regular Promises.

## Multichain

### Create Sell Order

To create a sell order for NFT the following parameters are required:

- `Item ID` — Id of an item passed in blockchain:address:id manner, e.g. `FLOW:A.ebf4ae01d1284af8.RaribleNFT:2321`,
- `Asset type` - Asset which you want to receive for your NFT, e.g. FLOW_FT, ERC_20,
- `Price` - Amount of asset of your choice you want to receive,
- `Contract Address` - Address of a given asset format, e.g. for FLOW_FT, which stands for Flow Fungible Token (so just a flow token) you have to pass a contract of a flow token, which on testnet is as follows: `A.7e60df042a9c0868.FlowToken`.

You can find all of the information about its contract addresses here:
https://docs.onflow.org/core-contracts/flow-token/#gatsby-focus-wrapper

!!! note ""

    Whenever you see the need for Multichain / Contract address, you can create it as follows:

    1. Blockchain Name
    2. Hex Address

    Example:

    `BlockchainName:HexAddress` = `ETHEREUM:0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05`

1. Get an id of the item you want to create a sell order for, e.g. by copying it from rarible URL when you're on your token, and create an orderRequest with that.
   The only difference between different blockchains is currency, i.e. asset which we want to receive in return for our NFT.

It should look something like that:

- `FLOW:A.ebf4ae01d1284af8.RaribleNFT:2321`,
- `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:47`
- `TEZOS:KT1BMB8m1QKqbbDDZPXpmGVCaM1cGcpTQSrw:443`

```typescript

import { toContractAddress, toItemId } from "@rarible/types";

...

const itemId = "FLOW:A.ebf4ae01d1284af8.RaribleNFT:2321";

const orderRequest: PrepareOrderRequest = {
  itemId: toItemId(itemId);
}
```

2. Create a currency which you want to receive in return.

Available ones:

- FlowAssetTypeNft,
- FlowAssetTypeFt,
- TezosXTZAssetType,
  etc.
  You can find all of them in node_modules/@rarible/api-client/build/models/AssetType.d.ts of you project. Additionally you're able to find all of the needed properties for them like tokenId, @type, or contract.

```typescript

const tezosAddress = "TEZOS:KT18pVpRXKPY2c4U2yFEGSH3ZnhB2kL8kwXS";
const flowAddress = "FLOW:A.7e60df042a9c0868.FlowToken";

// ETH
const currency: EthEthereumAssetType = {
  "@type": "ERC20",
  contract:
}

// TEZOS
const currency: TezosFTAssetType = {
  "@type": "TEZOS_FT";
  contract: toContractAddress(tezosAddress);
  tokenId?: 2321;
}

// FLOW
const currency: FlowAssetTypeFt = {
  "@type": "FLOW_FT",
  contract: toContractAddress(flowAddress);
};
```

3. Get sell response using orderRequest from earlier

```typescript
const sellResponse = await sdk.order.sell(orderRequest);

// From sellResponse object you can get informations like:
// is multiple sell order allowed
// baseFee
// maxAmount
// originFeeSupport
```

Example of response

```json
{
  "multiple": false,
  "supportedCurrencies": [
    {
      "blockchain": "FLOW",
      "type": "NATIVE"
    }
  ],
  "baseFee": 250,
  "originFeeSupport": "FULL",
  "payoutsSupport": "NONE",
  "maxAmount": "1"
}
```

4. Execute submit method on sellResponse object

```typescript
const sellOrderCreated = await sellResponse.submit({
  price: 1,
  amount: 1,
  currency: currency,
});
```

Example of response

```
FLOW:33966044
```

Voila

### Accept Bid

Accepting a bid codeflow is similar to the one in creating sell order.
Codeflow is identical for all of the blockchains.

1. Create fillRequest with an orderId which you want to accept

```typescript
const orderId = "FLOW:32732635";

const fillRequest: PrepareFillRequest = {
  orderId: toOrderId(orderId),
};
```

2. Get fillResponse using fillRequest

```typescript
const fillResponse = await sdk.order.acceptBid(fillRequest);
```

Example of response

```json
{
  "multiple": false,
  "maxAmount": "1",
  "baseFee": 250,
  "supportsPartialFill": false,
  "originFeeSupport": "FULL",
  "payoutsSupport": "NONE"
}
```

3. Submit received response

```typescript
const fillSubmitResponse = await fillResponse.submit({
  amount: 1,
});
```
