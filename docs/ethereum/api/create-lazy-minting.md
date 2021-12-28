---
title: Using Lazy Minting with Ethereum API
description: The main requests for using lazy minting in Rarible Protocol Ethereum API
---

# Using Lazy Minting

To mint an NFT using Lazy Minting, use the mintNftAsset method in [nft-lazy-mint-controller](https://ethereum-api.rarible.org/v0.1/doc#tag/nft-lazy-mint-controller).

## [mintNftAsset](https://ethereum-api.rarible.org/v0.1/doc#operation/mintNftAsset)

Creates a Lazy Minted NFT token.

`https://ethereum-api-staging.rarible.org/v0.1/nft/mints`

Example request (staging):

```shell
curl --request POST 'https://ethereum-api-staging.rarible.org/v0.1/nft/mints' \
  --header 'content-type: application/json' \
  --data-raw '{"contract":"0x6ede7f3c26975aad32a475e1021d8f6f39c89d82","uri":"/ipfs/QmWeVMxWPbz2AdGhrZdi3ZQXVdppzPPakXfdavtu9syyA7","royalties":[{"account":"0xb7d1f311ef648f0a9d9eff2b47f5bbb53e583dca","value":1000}],"creators":[{"account":"0xb7d1f311ef648f0a9d9eff2b47f5bbb53e583dca","value":10000}],"tokenId":"83144199935168800027256855471009236590928205711995533202494108027144764391425","@type":"ERC721","signatures":["0xf91e21cda6fc519f4b3ea77086393482a65f715b3e981da8d31c753bf5c5060018b4460cc9935f397808d14365e64214c18d0fc46441b55e0858a398ff7ffc8c1b"]}'
```

Request parameters:

* **@typerequired** — token type `ERC721` or `ERC1155`
* **supply** — the total number of tokens for Mint. Only for ERC-1155
* **contract** — address of the smart contract
* **tokenId** — token ID
* **uri** — suffix for the token URI. The prefix is usually `ipfs:/`
* **creators** — an array of authors addresses
* **royalties** — royalty array
* **signatures** — array of digital signatures. Each creator must have a signature the only exception being when the creator sends a mint transaction.

Response example (status 200):

```json
{
  "id": "0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:83144199935168800027256855471009236590928205711995533202494108027144764391425",
  "contract": "0x6ede7f3c26975aad32a475e1021d8f6f39c89d82",
  "tokenId": "83144199935168800027256855471009236590928205711995533202494108027144764391425",
  "creators": [
    {
      "account": "0xb7d1f311ef648f0a9d9eff2b47f5bbb53e583dca",
      "value": 10000
    }
  ],
  "supply": "1",
  "lazySupply": "1",
  "owners": [
    "0xb7d1f311ef648f0a9d9eff2b47f5bbb53e583dca"
  ],
  "royalties": [
    {
      "account": "0xb7d1f311ef648f0a9d9eff2b47f5bbb53e583dca",
      "value": 1000
    }
  ],
  "date": "2021-11-23T15:37:03.610Z",
  "pending": [],
  "deleted": false,
  "meta": {
    "name": "Violence Token",
    "description": "",
    "attributes": [],
    "image": {
      "url": {
        "ORIGINAL": "ipfs://ipfs/QmbnW9qS5dcmXavo55yqzmF79wWT6qTcYKBAAaS3gDgrDa/image.jpeg"
      },
      "meta": {
        "ORIGINAL": {
          "type": "image/jpeg",
          "width": 400,
          "height": 400
        }
      }
    }
  }
}
```

Response parameters:

* **id** — item ID, has the format `${contract}:${tokenId}`
* **contract** — address of the smart contract
* **tokenId** — token ID
* **creators** — array of information about creators
* **supply** — number of tokens created
* **lazysupply** — the number of Lazy Minting tokens created
* **owners** — array of information about token owners
* **royalties** — an array of information about royalties
* **date** — date of token creation
* **pending** — whether the item is incomplete. For example, it is in the status `TRANSFER`
* **deleted** — is the order deleted
* **meta** — meta information about the item
