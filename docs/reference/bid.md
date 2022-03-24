---
title: Create and Accept Bids with Rarible Protocol
description: The main information about creating and accepting bids in Rarible Multichain Protocol
---

# Create and Accept Bid

You can Create and Accept Bids with Rarible Multichain Protocol in different blockchains.

--8<-- "docs/snippets/preparation-sdk.md"

## Create a bid

You can place your bid for any given NFT, even if there isn't any sell offer associated with it. It's up to the owner if they accept it or not.

Use `bid` function:

```typescript
import { createRaribleSdk } from "@rarible/sdk"
import { toItemId } from "@rarible/types"
import type { BlockchainWallet } from "@rarible/sdk-wallet/src"
import type { RequestCurrency } from "@rarible/sdk/build/common/domain"

async function bid(wallet: BlockchainWallet, assetType: RequestCurrency) {
	const sdk = createRaribleSdk(wallet, "dev")
	const bidAction = await sdk.order.bid({
		itemId: toItemId("<ITEM_ID>"),
	})
	const bidOrderId = await bidAction.submit({
		amount: 1,
		price: "0.000002",
		currency: assetType,
	})
	return bidOrderId
}
```

* `itemId` —  ItemID of your NFT, has format `${blockchain}:${token}:${tokenId}`. For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:12345`
* `amount` — amount of NFT tokens 
* `price` — price per 1 NFT in ETH
* `currency` — currency (ETH or specific ERC20 or Tez, Flow, etc.)

## Update a bid

Similarly to updating a sell order, there is also a possibility to update a bid. It can be only higher than the original bid order price.

Use `bid` function with `updateAction`:

```typescript
import { createRaribleSdk } from "@rarible/sdk"
import { toItemId } from "@rarible/types"
import type { BlockchainWallet } from "@rarible/sdk-wallet/src"
import type { RequestCurrency } from "@rarible/sdk/build/common/domain"

async function bid(wallet: BlockchainWallet, assetType: RequestCurrency) {
	const sdk = createRaribleSdk(wallet, "dev")
	const bidAction = await sdk.order.bid({
		itemId: toItemId("<ITEM_ID>"),
	})
	const bidOrderId = await bidAction.submit({
		amount: 1,
		price: "0.000002",
		currency: assetType,
	})

	const updateAction = await sdk.order.bidUpdate({
		orderId: bidOrderId,
	})
	//You can only increase price of bid order for security reasons
	//If you want to force change bid price you should cancel order
	await updateAction.submit({ price: "0.000003" })
}
```

## Cancel a bid

To cancel a bid, use `cancelOrder` function:

```typescript
import { createRaribleSdk } from "@rarible/sdk"
import { toOrderId } from "@rarible/types"
import type { BlockchainWallet } from "@rarible/sdk-wallet/src"

async function cancelOrder(wallet: BlockchainWallet) {
	const sdk = createRaribleSdk(wallet, "dev")
	const cancelTx = await sdk.order.cancel({
		orderId: toOrderId("<YOUR_ORDER_ID>"),
	})
	await cancelTx.wait()
}
```

* `orderId` —  Id of your order, has format `${blockchain}:${id}`. For example, `ETHEREUM:1234567890`

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
