# Asset Discovery

## [Search Items](https://api-staging.rarible.com/protocol/ethereum/nft/indexer/v0.1/swagger/webjars/swagger-ui/index.html?configUrl=/protocol/ethereum/nft/indexer/v0.1/swagger/v3/api-docs/swagger-config#/item-controller/searchItems)

{% hint style="info" %}
In order to get latest information about API, please follow [OpenAPI doc](https://api-reference.rarible.com/#tag/item-controller) for item-controller part
{% endhint %}

There are some controllers to query items:

* [get all items](https://api-reference.rarible.com/#operation/getAllItems)
* [get items by owner](https://api-reference.rarible.com/#operation/getItemsByOwner)
* [get items by collection](https://api-reference.rarible.com/#operation/getItemsByCollection)
* other controllers in [item-controller](https://api-reference.rarible.com/#tag/item-controller) section of the [api-reference](https://api-reference.rarible.com)

These controllers have common parameters:

* size - how many items you want to get
* continuation - send this parameter to fetch next portion of data (you can find continuation value in the server response)
* also they have different query parameters for each. Please, see [api-reference](https://api-reference.rarible.com)

{% swagger baseUrl="http://api.rarible.com/protocol/v0.1/ethereum/nft/items/" path=":itemId/meta" method="get" summary="Item Metadata" %}
{% swagger-description %}
Displays all item Metadata (Stored on IPFS)
{% endswagger-description %}

{% swagger-parameter in="path" name="itemId" type="string" %}
The itemId is built by using collectionAddress:tokenId - An example is 0x60f80121c31a0d46b5279700f9df786054aa5ee5:21
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "name": "string",
  "description": "string",
  "image": "string",
  "external_url": "string",
  "animation_url": "string",
  "attributes": {}
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="http://api.rarible.com/protocol/v0.1/ethereum/nft/items/" path=":itemId" method="get" summary="Item Data" %}
{% swagger-description %}
Displays Item data such as Royalties, Unlockable content, etc.
{% endswagger-description %}

{% swagger-parameter in="path" name="itemId" type="string" %}
The itemId is built by using collectionAddress:tokenId - An example is 0x60f80121c31a0d46b5279700f9df786054aa5ee5:21
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "id": "string",
  "token": "string",
  "tokenId": 0,
  "unlockable": true,
  "creator": "string",
  "supply": 0,
  "owners": [
    "string"
  ],
  "royalties": [
    {
      "recipient": "string",
      "value": 0
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

{% hint style="danger" %}
If you wish to build an order for an ERC1155, it is important you also record the amount returned by the query.
{% endhint %}

**Visit the next section on** [**how to create a sell order**](../exchange/creating-a-sell-order.md)**!**
