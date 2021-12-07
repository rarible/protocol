# Search Items

The main requests for working with Items relate to the [nft-itemcontroller](https://ethereum-api.rarible.org/v0.1/doc#tag/nft-item-controller). Let's look at the example of getNftAllItems.

## [getNftAllItems](https://ethereum-api.rarible.org/v0.1/doc#operation/getNftAllItems)

Returns all NFT items.

Example request:

```shell
curl --request GET 'https://ethereum-api.rarible.org/v0.1/nft/items/all?size=1'
```

Request parameters:

* **size** — the number of items to be returned
* **showDeleted** — display deleted items or not
* **lastUpdatedFrom** — returns items that have been updated since that date (timestamp in ms)
* **lastUpdatedTo** — returns items that have been updated to this date (timestamp in ms)
* **continuation** — continuation token from the previous response

Response example (status 200):

```json
{
    "total": 1,
    "continuation": "1637677864204_0xf6793da657495ffeff9ee6350824910abc21356c:0x8108800667cb3859020c77f7643cedb794b4455700000000000000000000000e",
    "items": [
        {
            "id": "0xf6793da657495ffeff9ee6350824910abc21356c:58363375839982426315252321964399886024230569048144758096248518895130164330510",
            "contract": "0xf6793da657495ffeff9ee6350824910abc21356c",
            "tokenId": "58363375839982426315252321964399886024230569048144758096248518895130164330510",
            "creators": [
                {
                    "account": "0x8108800667cb3859020c77f7643cedb794b44557",
                    "value": 10000
                }
            ],
            "supply": "1",
            "lazySupply": "1",
            "owners": [
                "0x8108800667cb3859020c77f7643cedb794b44557"
            ],
            "royalties": [
                {
                    "account": "0x8108800667cb3859020c77f7643cedb794b44557",
                    "value": 1000
                }
            ],
            "date": "2021-11-23T14:31:04.204Z",
            "pending": [],
            "deleted": false,
            "meta": {
                "name": "Rampows the Daltons",
                "description": "",
                "attributes": [],
                "image": {
                    "url": {
                        "ORIGINAL": "ipfs://ipfs/QmWXtdxkrR33rNxoNAbUDELsv2YBjajE4nhHGrgwT7UBHQ/image.jpeg"
                    },
                    "meta": {
                        "ORIGINAL": {
                            "type": "image/jpeg",
                            "width": 1792,
                            "height": 1401
                        }
                    }
                }
            }
        }
    ]
}
```

Response parameters:

* **total** — the number of items returned on request
* **continuation** — continuation token from the previous response
* **items** — list of found items with basic information about them
