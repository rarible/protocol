---
title: Mint and Sell NFTs in Rarible Protocol
description: The main information about minting and selling NFTs in Rarible Multichain Protocol
---

# Mint and Sell

You can prepare Mint and put up on Sale NFTs with Rarible Multichain Protocol in different blockchains.

--8<-- "docs/snippets/preparation-sdk.md"

## Mint and List NFT for sale

Often required to put your NFT on the sale right after creation. If it's the case for you, you can also use the `mintOnChain` function with `sellAction`:

```typescript
import { createRaribleSdk } from "@rarible/sdk"
import { toItemId } from "@rarible/types"
import type { BlockchainWallet } from "@rarible/sdk-wallet/src"
import type { RequestCurrency } from "@rarible/sdk/build/common/domain"

async function mintOnChain(wallet: BlockchainWallet, assetType: RequestCurrency) {
	const sdk = createRaribleSdk(wallet, "dev")
	const sellAction = await sdk.order.sell({
		itemId: toItemId("<YOUR_ITEM_ID>"),
	})
	const sellOrderId = await sellAction.submit({
		amount: 1,
		price: "0.000002",
		currency: assetType,
	})
	return sellOrderId
}
```

* `itemId` —  ItemID of your NFT, has format `${blockchain}:${token}:${tokenId}`. For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:12345`
* `amount` — amount of NFT tokens for sale
* `price` — price per 1 NFT in ETH
* `currency` — currency (ETH or specific ERC20 or Tez, Flow, etc.)

Example of a successful response:

```typescript
itemId: "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382047";
OrderId: "..."
```

## Update listed token price

Due to security circumstances, you can't update the token price to higher than the one created in the original sell order. If you want to boost the price, you need to cancel the sell order and create a new one.

For update listed NFT price use the `sellAndUpdate` function:

```typescript
import { createRaribleSdk } from "@rarible/sdk"
import { toItemId } from "@rarible/types"
import type { BlockchainWallet } from "@rarible/sdk-wallet/src"
import type { RequestCurrency } from "@rarible/sdk/build/common/domain"

async function sellAndUpdate(wallet: BlockchainWallet, assetType: RequestCurrency) {
	const sdk = createRaribleSdk(wallet, "dev")
	const sellAction = await sdk.order.sell({
		itemId: toItemId("<YOUR_ITEM_ID>"),
	})
	const sellOrderId = await sellAction.submit({
		amount: 1,
		price: "0.000002",
		currency: assetType,
	})
	const updateAction = await sdk.order.sellUpdate({ orderId: sellOrderId })
	//You can only decrease price of sell order for security reasons
	//If you want to force change sell price you should cancel sell order
	await updateAction.submit({ price: "0.000001" })
}
```

## Checking created order

To check the created order use the `getOrderById` [API method](https://api.rarible.org/v0.1/doc#operation/getOrderById)

??? note "getOrderById"

    Returns Order by ID.
    
    `https://api.rarible.org/v0.1/orders/{id}`
    
    **Example request (staging)**
    
    ```shell
    curl --request GET 'https://api-staging.rarible.org/v0.1/orders/ETHEREUM:0x0293c5918e9f7fb5eec101a656e5ba73fcfd61072ad211a9e80972cc487232ed'
    ```
    
    Request parameters:
    
    * `id` —  ID of your order, has format `${blockchain}:${id}`
    
        For example, `ETHEREUM:0x0293c5918e9f7fb5eec101a656e5ba73fcfd61072ad211a9e80972cc487232ed`
    
    **Example response (status 200)**

    ```json
    {
      "id": "ETHEREUM:0x0293c5918e9f7fb5eec101a656e5ba73fcfd61072ad211a9e80972cc487232ed",
      "fill": "0.00001",
      "platform": "RARIBLE",
      "status": "FILLED",
      "makeStock": "0",
      "cancelled": false,
      "createdAt": "2022-03-11T12:09:14.904Z",
      "lastUpdatedAt": "2022-03-11T12:17:21Z",
      "makePrice": "0.00001",
      "makePriceUsd": "0.026062773565248403",
      "priceHistory": [
        {
          "date": "2022-03-11T12:09:14.904Z",
          "makeValue": "1",
          "takeValue": "0.00001"
        }
      ],
      "maker": "ETHEREUM:0x2c02f0563eaf96dc3ddcb514f4d1832e7cbc801f",
      "make": {
        "type": {
          "@type": "ERC1155_Lazy",
          "contract": "ETHEREUM:0x4ff5fedb430f7393c8c5675e753782b595feb471",
          "tokenId": "19906957776073516298368660511705840565672843874722253325423575352615771308035",
          "uri": "https://shopdefi.gq/api/metadata/c13249c9-e99b-43cd-8a2f-9da5cd26881c",
          "supply": "1",
          "creators": [
            {
              "account": "ETHEREUM:0x2c02f0563eaf96dc3ddcb514f4d1832e7cbc801f",
              "value": 10000
            }
          ],
          "royalties": [
            {
              "account": "ETHEREUM:0x2c02f0563eaf96dc3ddcb514f4d1832e7cbc801f",
              "value": 1000
            }
          ],
          "signatures": [
              "0xee347802d66c1231e3b799dd35768d52df1cd0b8fac88675836c0b8c9394077302d45f29a1e1be7afcf7bd2a9e54cd235a8b632772228fb4cbd0ce013ac3cef71b"
          ]
        },
        "value": "1"
      },
      "take": {
        "type": {
          "@type": "ETH",
          "blockchain": "ETHEREUM"
        },
        "value": "0.00001"
      },
      "salt": "0xaea6697bb08038f1ee23254fef19181bab3694464b612fb6e527ecf85f4cb830",
      "signature": "0xa80eb9c4cbea283976ba4b0db925dae0aefb2d5d4dfedbaa4214ae99a2e5832552e41634ff998b558c258f8b8bd803681534c340029cd1478292ea3838d069791c",
      "pending": [],
      "data": {
        "@type": "ETH_RARIBLE_V2",
        "payouts": [],
        "originFees": []
      }
    }
    ```

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
