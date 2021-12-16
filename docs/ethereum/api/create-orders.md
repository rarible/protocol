# Create Orders

To create an order, use the upsertOrder method in [order-controller](https://ethereum-api.rarible.org/v0.1/doc#tag/order-controller).

## [upsertOrder](https://ethereum-api.rarible.org/v0.1/doc#operation/upsertOrder)

Creates or updates an Order.

`https://ethereum-api.rarible.org/v0.1/order/orders`

Example request (staging):

```shell
curl --request POST 'https://ethereum-api-staging.rarible.org/v0.1/order/orders' \
  --header 'content-type: application/json' \
  --data-raw '{"maker":"0xb7d1f311ef648f0a9d9eff2b47f5bbb53e583dca","type":"RARIBLE_V2","data":{"dataType":"RARIBLE_V2_DATA_V1","payouts":[],"originFees":[{"account":"0x76c5855e93bd498b6331652854c4549d34bc3a30","value":250}]},"salt":"86881339267547208763979074509610437060593762063071194041427040496432360352297","signature":"0xd3147a72aa61e2ff970c05dac9b87c4a7187a5d0d6dc125f187e40612cea73d637608995704da1d35dc0f92c153811167860a85889de9b96c9c80e9b960d80681c","make":{"assetType":{"@type":"ERC721","contract":"0x6ede7f3c26975aad32a475e1021d8f6f39c89d82","tokenId":"83144199935168800027256855471009236590928205711995533202494108027144764391425","uri":"/ipfs/QmWeVMxWPbz2AdGhrZdi3ZQXVdppzPPakXfdavtu9syyA7","creators":[{"account":"0xb7d1f311ef648f0a9d9eff2b47f5bbb53e583dca","value":10000}],"royalties":[{"account":"0xb7d1f311ef648f0a9d9eff2b47f5bbb53e583dca","value":1000}],"signatures":["0xf91e21cda6fc519f4b3ea77086393482a65f715b3e981da8d31c753bf5c5060018b4460cc9935f397808d14365e64214c18d0fc46441b55e0858a398ff7ffc8c1b"],"assetClass":"ERC721_LAZY"},"value":"1"},"take":{"assetType":{"assetClass":"ETH"},"value":"10000000000000000"}}'
```

Request parameters:

* **type** — order type `RARIBLE_V1` or `RARIBLE_V2`
* **data** — data for creating or updating the order. The required fields depend on order type
* **maker** — address of the order creator
* **taker** — address of the recipient of the order (optional)
* **make** — make the side of the order. What the creator has
* **take** — take the side of the order. What the creator wants to get in exchange for the make side
* **salt** — the string of data that is passed to the hash function along with the input array of data to calculate the hash
* **start** — the start date of the order placement, from which the buyer can make a Bid (optional) p.s. unix time is used 
* **end** — the end date of the order placement, before which the buyer can make a Bid (optional) p.s. unix time is used 
* **signature** — the digital signature of the order creator

Response example (status 200):

```json
{
  "type": "RARIBLE_V2",
  "maker": "0xb7d1f311ef648f0a9d9eff2b47f5bbb53e583dca",
  "make": {
    "assetType": {
      "assetClass": "ERC721_LAZY",
      "contract": "0x6ede7f3c26975aad32a475e1021d8f6f39c89d82",
      "tokenId": "83144199935168800027256855471009236590928205711995533202494108027144764391425",
      "uri": "/ipfs/QmWeVMxWPbz2AdGhrZdi3ZQXVdppzPPakXfdavtu9syyA7",
      "creators": [
        {
          "account": "0xb7d1f311ef648f0a9d9eff2b47f5bbb53e583dca",
          "value": 10000
        }
      ],
      "royalties": [
        {
          "account": "0xb7d1f311ef648f0a9d9eff2b47f5bbb53e583dca",
          "value": 1000
        }
      ],
      "signatures": [
        "0xf91e21cda6fc519f4b3ea77086393482a65f715b3e981da8d31c753bf5c5060018b4460cc9935f397808d14365e64214c18d0fc46441b55e0858a398ff7ffc8c1b"
      ]
    },
    "value": "1",
    "valueDecimal": 1
  },
  "take": {
    "assetType": {
      "assetClass": "ETH"
    },
    "value": "10000000000000000",
    "valueDecimal": 0.01
  },
  "fill": "0",
  "fillValue": 0,
  "makeStock": "1",
  "makeStockValue": 1,
  "cancelled": false,
  "salt": "0xc015186be955e586fb9d3bc1ddbbf43470a40d18b4ccdc750af405155eee6a29",
  "signature": "0xd3147a72aa61e2ff970c05dac9b87c4a7187a5d0d6dc125f187e40612cea73d637608995704da1d35dc0f92c153811167860a85889de9b96c9c80e9b960d80681c",
  "createdAt": "2021-11-23T15:37:13.158Z",
  "lastUpdateAt": "2021-11-23T15:37:13.158Z",
  "pending": [],
  "hash": "0x279863b844f7bae2db201bff5abd9467f380eb029399e1339671d9d51f9a0280",
  "makeBalance": "0",
  "makePrice": 0.01,
  "makePriceUsd": 40.193574609729986,
  "priceHistory": [
    {
      "date": "2021-11-23T15:37:13.158Z",
      "makeValue": 1,
      "takeValue": 0.01
    }
  ],
  "status": "ACTIVE",
  "data": {
    "dataType": "RARIBLE_V2_DATA_V1",
    "payouts": [],
    "originFees": [
      {
        "account": "0x76c5855e93bd498b6331652854c4549d34bc3a30",
        "value": 250
      }
    ]
  }
}
```

Response parameters:

* **type** — order type `RARIBLE_V1`, `RARIBLE_V2`, `OPEN_SEA_V1` or `CRYPTO_PUNK`
* **data** — information about order type, Fees, etc.
* **maker** — address of the order creator
* **taker** — address of the recipient of the order
* **make** — make the order side. What the creator has
* **take** — take the side of the order. What the creator wants to get in exchange for the make side
* **fill** — filling in data when matching
* **fillvalue** — data filling value
* **start** — the starting date of the order placement, from which the buyer can make a Bid
* **end** — the end date of the order placement before which the buyer can make a Bid
* **makestock** — how much is available for sale
* **makestockvalue** — the value of how much is available for sale
* **cancelled** — the order is canceled or not
* **salt** — the string of data that is passed to the hash function along with the input array of data to calculate the hash
* **signature** — digital signature of the order creator
* **createdAt** — date of order creation
* **lastupdateat** — order update date
* **pending** — whether the order is incomplete. For example, it is in the status of `CANCEL`, `ORDER_SIDE_MATCH` or `ON_CHAIN_ORDER`
* **hash** — hash of the order
* **makebalance** — balance of the order creator
* **makeprice** — order price
* **Takeprice** — buyer's suggested price
* **makepriceusd** — order price in USD
* **takepriceusd** — price in USD suggested by the buyer
* **pricehistory** — history of price changes
* **status** — order status `ACTIVE`, `FILLED`, `HISTORICAL`, `INACTIVE` or `CANCELLED`
