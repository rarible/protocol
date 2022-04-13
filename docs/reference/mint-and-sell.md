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
import { toCollectionId, toUnionAddress } from "@rarible/types"
import type { BlockchainWallet } from "@rarible/sdk-wallet/src"
import { MintType } from "@rarible/sdk/build/types/nft/mint/domain"
import type { RequestCurrency } from "@rarible/sdk/build/common/domain"

async function mintAndSell(wallet: BlockchainWallet, currency: RequestCurrency) {
	const sdk = createRaribleSdk(wallet, "dev")

	const mintAction = await sdk.nft.mintAndSell({
		collectionId: toCollectionId("<NFT_CONTRACT_ADDRESS>"),
	})
	/*
    You should upload json file with item metadata in the following format:
    {
      name: string
      description: string | undefined
      image: string | undefined
      "animation_url": string | undefined
      "external_url": string | undefined
      attributes: TokenMetadataAttribute[]
    }
    and insert link to json file to "uri" field.
    To format your json data use "sdk.nft.preprocessMeta()" method
   */
	const mintResult = await mintAction.submit({
		uri: "<YOUR_LINK_TO_JSON>",
		royalties: [{
			account: toUnionAddress("<ROYLATY_ADDRESS>"),
			value: 1000,
		}],
		creators: [{
			account: toUnionAddress("<CREATOR_ADDRESS>"),
			value: 10000,
		}],
		lazyMint: true,
		supply: 1,
		price: "0.000000000000000001",
		currency,
	})
	if (mintResult.type === MintType.OFF_CHAIN) {
		return mintResult.itemId
	}
}
```

* `collectionId` — your collection address, that can be already [deployed](create-collection.md). Also, can be the address of Rarible Smart Contracts instance. You can find them on [Contract Addresses](contract-addresses.md) page
* `ContractAddress` — `BlockchainName:HexAddress` = `ETHEREUM:0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05`
    * `BlockchainName` — `ETHEREUM`, `FLOW`, `TEZOS` or `POLYGON`
* `uri` — address of JSON file with "image", "name" and other NFT attributes. For example, on IPFS: [https://ipfs.io/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp](https://ipfs.io/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp)
* `royalties` — value and address for receiving royalties
    * `account` — address in Union format `${blockchainGroup}:${token}`. For example, `TEZOS:tz1dKxdpV1hgErMTTKBorb8R5tSz8hFzPhKh`
    * `value` — value of the royalties. For example, 2,5% value is `250`
* `creators` — value and address of the creator
    * `account` — address in Union format `${blockchainGroup}:${token}`. For example, `TEZOS:tz1dKxdpV1hgErMTTKBorb8R5tSz8hFzPhKh`
    * `value` — value of the royalties. For example, 2,5% value is `250`
* `lazyMint` — boolean, `false` if you want to mint item on the blockchain, `true` allow to you mint off-chain item without spending the gas
* `supply` — number of NFTs to create (not in every case it is supported, you can check it by reading `sdk.nft.mint` response under multiple parameters)
* `price` — price per 1 NFT in ETH
* `currency` — currency (ETH or specific ERC20 or Tez, Flow, etc.)

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
