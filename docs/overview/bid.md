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

## Checking created bid

To check the created bid use the `getAuctionBidsById` [API method](https://api.rarible.org/v0.1/doc#operation/getAuctionBidsById)

??? note "getAuctionBidsById"

    Returns Bids by ID.
    
    `https://api.rarible.org/v0.1/auctions/{id}/bids`
    
    **Example request (staging)**
    
    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/orders/bids/byItem?itemId=ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:18821466700545955594683918922933102928122274620066857937800231922729025011855&status=ACTIVE'
    ```
    
    Request parameters:
    
    * `itemId` —  ItemID of your NFT, has format `${blockchain}:${token}:${tokenId}`
    
        For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:12345`
    
    **Example response (status 200)**

    ```json
    {
        "orders": [
            {
                "id": "ETHEREUM:0xce5a4beadeddeefdd91dad3092315fbba176dd5325e032dd10194a9bc60bf28c",
                "fill": "0",
                "platform": "RARIBLE",
                "status": "ACTIVE",
                "makeStock": "0.12345",
                "cancelled": false,
                "createdAt": "2022-03-07T06:46:06.275Z",
                "lastUpdatedAt": "2022-03-07T06:46:06.275Z",
                "takePrice": "0.12345",
                "takePriceUsd": "0.12342413889756425082",
                "priceHistory": [],
                "maker": "ETHEREUM:0x45d5ef37dfa2a3cc91d5909fd493f1a480bba6b0",
                "make": {
                    "type": {
                        "@type": "ERC20",
                        "contract": "ETHEREUM:0x5592ec0cfb4dbc12d3ab100b257153436a1f0fea"
                    },
                    "value": "0.12345"
                },
                "take": {
                    "type": {
                        "@type": "ERC721_Lazy",
                        "contract": "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82",
                        "tokenId": "18821466700545955594683918922933102928122274620066857937800231922729025011855",
                        "uri": "/ipfs/QmcTxYXrcoHzi5EyoypK6PvCQxy8piZiYpFKjr75MRKp89",
                        "creators": [
                            {
                                "account": "ETHEREUM:0x299c92988198a5965111537797cc1789a5d7e336",
                                "value": 10000
                            }
                        ],
                        "royalties": [
                            {
                                "account": "ETHEREUM:0x299c92988198a5965111537797cc1789a5d7e336",
                                "value": 1000
                            }
                        ],
                        "signatures": [
                            "0xee5416f619e2efefbcf4a3cc8645ff61c298ada42a5c9c07e5ce3ed66444a937010daab240392eabad2b8e4bc95f527178c377937c25a655991532a3b2ffa9361c"
                        ]
                    },
                    "value": "1"
                },
                "salt": "0x24d4f84a848a4c49df39d73961b887958598046384639c09f61d4dd85f6c5f1e",
                "signature": "0x928e0d53da390ea7e58f2d5715d0492ad4dd4cae7a7126759682b642c32e3caf7395edeb8342ebf5fc57d959c996b41079e391565cc00b5966aac7f1788bc2d11c",
                "data": {
                    "@type": "ETH_RARIBLE_V2",
                    "payouts": [],
                    "originFees": [
                        {
                            "account": "ETHEREUM:0x76c5855e93bd498b6331652854c4549d34bc3a30",
                            "value": 250
                        }
                    ]
                }
            }
        ]
    }
    ```

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
