---
title: Burn NFTs in Rarible Protocol
description: The main information about burning NFTs in Rarible Multichain Protocol
---

# Burn

You can burn NFTs with Rarible Multichain Protocol in different blockchains.

--8<-- "docs/snippets/preparation-sdk.md"

## Burn NFTs

Burning tokens is equivalent to sending them to address 0x0 because nobody has a private key for that.

Use `burn` function:

```typescript
import { createRaribleSdk } from "@rarible/sdk"
import { toItemId, toUnionAddress } from "@rarible/types"
import type { BlockchainWallet } from "@rarible/sdk-wallet/src"

async function burn(wallet: BlockchainWallet) {
	const sdk = createRaribleSdk(wallet, "dev")

	const burnAction = await sdk.nft.burn({
		itemId: toItemId("<ITEM_ID>"),
	})
	const burnTx = await burnAction.submit({
		amount: 1,
		//optional
		creators: [{
			account: toUnionAddress("<CREATOR_ADDRESS>"),
			value: 10000,
		}],
	})
	//transaction returned if item is on-chain
	if (burnTx) {
		await burnTx.wait()
	}
}
```

* `itemId` —  Id of your NFT, has format `${blockchain}:${token}:${tokenId}`. For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:12345`
* `amount` — amount of NFT tokens
* `creators` — value and address of the creator
    * `account` — address in Union format `${blockchainGroup}:${token}`. For example, `TEZOS:tz1dKxdpV1hgErMTTKBorb8R5tSz8hFzPhKh`
    * `value` — value of the part in the ownership of the item. For example, 100% value is `10000`. If there are several owners, the total cost cannot be more than `10000`

## Checking burned NFT

To check the burned item:

* Use the `getItemById` [API method](https://api.rarible.org/v0.1/doc#operation/getItemById)

    ??? note "getItemById"

        Returns Item by ID.
        
        `https://api.rarible.org/v0.1/items/{itemId}`
        
        **Example request (staging)**
        
        ```shell
        curl --request GET 'https://api-staging.rarible.org/v0.1/items/ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:19661880631107248865491477079747186145992059189823053172927066273904580362243'
        ```
        
        Request parameters:
        
        * `itemId` —  ItemID of your NFT, has format `${blockchain}:${token}:${tokenId}`
        
            For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:12345`
        
        **Example response (status 200)**
    
        ```json
        {
           "id": "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:19661880631107248865491477079747186145992059189823053172927066273904580362243",
           "blockchain": "ETHEREUM",
           "collection": "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82",
           "contract": "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82",
           "tokenId": "19661880631107248865491477079747186145992059189823053172927066273904580362243",
           "creators": [
              {
                 "account": "ETHEREUM:0x2b783ae5b5b8a7a822449c7d8b6f35f9abc827f5",
                 "value": 10000
              }
           ],
           "owners": [],
           "royalties": [],
           "lazySupply": "0",
           "pending": [],
           "mintedAt": "2022-03-09T22:48:33Z",
           "lastUpdatedAt": "2022-03-09T22:50:03.530Z",
           "supply": "1",
           "meta": {
              "name": "gbgbgbgbgbgb",
              "description": "",
              "attributes": [],
              "content": [
                 {
                    "@type": "IMAGE",
                    "url": "https://rarible.mypinata.cloud/ipfs/QmQCp8bhbaPwGEuHeeR8pme2q3zuSjam2JEuFgAvp4DZsU/image.jpeg",
                    "representation": "ORIGINAL",
                    "mimeType": "image/jpeg",
                    "size": 13311,
                    "width": 640,
                    "height": 640
                 }
              ],
              "restrictions": []
           },
           "deleted": false,
           "auctions": [],
           "totalStock": "0",
           "sellers": 0
        }
        ```

* Or check [Etherscan](https://etherscan.io/) for Ethereum and Polygon, [Flowscan](https://flowscan.org/) for Flow, or [tezblock](https://tezblock.io/) for Tezos.

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
