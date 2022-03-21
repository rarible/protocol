---
title: Burn NFTs in Rarible Protocol
description: The main information about burning NFTs in Rarible Multichain Protocol
---

# Burn

You can burn NFTs with Rarible Multichain Protocol in different blockchains.

## Preparation

1. [Install and configure](https://docs.rarible.org/union-sdk/#installation) Protocol SDK.
2. [Connect the required wallet](https://docs.rarible.org/union-sdk/#metamask-integration-with-rarible).
3. [Mint NFT](mint.md).

## Burn NFTs

Burning tokens is equivalent to sending them to address 0x0 because nobody has a private key for that.

To burn NFTs create `PrepareBurnRequest` and get `sdk.nft.burn()`:

```typescript
const itemId =
  "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382052";

const burnRequest: PrepareBurnRequest = {
  itemId: toItemId(itemId),
};

const burnResponse = await sdk.nft.burn(burnRequest);

const response = await burnResponse.submit();
```

* `itemId` — ItemID of your NFT in format `${blockchain}:${token}:${tokenId}`. Supported blockchains: `ETHEREUM`, `POLYGON`, `TEZOS`, `FLOW`.

    For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:1`

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
