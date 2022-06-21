---
title: Rarible Multichain Protocol Overview
description: How to use the Rarible Multichain Protocol to find the NFT you need?
---

### Using Rarible API to fetch data fast and efficiently.

![One API to rule them all ⚔️](./img/1*XLVGtnxc86FuO27TEWmkeA.png)

# Rarible Multichain Protocol — Intro

[In the previous article](https://medium.com/rarible-dao/are-you-new-to-an-nft-world-d22c4a154901), we showed you how to find NFTs you’re interested in, by using different searching parameters (such as collection, address, or user name) on a marketplace’s website. In general, that’s a very simple process…unless you want to fetch details from many different NFTs.

In this article, we’ll learn how to get information on NFTs-related activities, straight from the source. In other words, we will cover how you can implement the same functionality you see on the [Rarible Marketplace](https://rarible.com/), using the Rarible Multichain Protocol.

The [Rarible Multichain protocol](https://multichain.redoc.ly/v0.1/) is an API developed by the Rarible team that allows you to fetch activity information of different NFT projects — NFTs details, orders, owners, bids, etc. Since we will be using an API to get information, you’ll be able to fully automate the search process and do it in a structured and repetitive manner.

# Rarible Multichain API — Overview

The [Rarible Multichain Protocol](https://multichain.redoc.ly/) organizes search capabilities in a set of controllers. Each controller provides a fine-grained API to retrieve certain pieces of information about the NFT, or any of its attributes.

The API is comprised of the following controllers:

- [Signature Controller](https://multichain.redoc.ly/v0.1#tag/signature-controller): responsible for verifying signatures of messages,

- [Currency Controller](https://multichain.redoc.ly/v0.1#tag/currency-controller): it allows us to get a USDC rate for a given token,

- [Item Controller](https://multichain.redoc.ly/v0.1#tag/item-controller): it lets us check all sorts of item-related information, like item details, owner, collection, etc.

- [Ownership Controller](https://multichain.redoc.ly/v0.1#tag/ownership-controller): returns ownership details,

- [Order Controller](https://multichain.redoc.ly/v0.1#tag/order-controller): responsible for fetching order information, like sell order, order by id, orders by the maker,

- [Auction Controller](https://multichain.redoc.ly/v0.1#tag/auction-controller): auctions related information (auctions are not yet supported on the API),

- [Activity Controller](https://multichain.redoc.ly/v0.1#tag/activity-controller): activity information, such as token transfer, minting, burning, aggregated by users, items, collections,

- [Collection Controller](https://multichain.redoc.ly/v0.1#tag/collection-controller): collections-related information.

As you can see, there is a controller for every imaginable parameter, so getting the desired information won’t be a problem. The hard part is to easily navigate through the information we get from them, and make our logic as simple as possible.

# Search for a collection

Let’s recreate a simple scenario, just to put this into context.

Let’s say that the only information we have about a collection is its ID, aka collection address. It’s the [moonbird collection](https://rarible.com/collection/0x23581767a106ae21c074b2276d25e5c3e136a68b/items), and we want to know everything about it. We access the [Rarible Multichain API docs](https://multichain.redoc.ly/v0.1#tag/collection-controller) and start building.

Since the only information we have is the collection address, the first endpoint we’ll use is “get collection by Id”. To be precise, it’s this one. 👇

![](./img/0*dyWJ8qYbIxnX8lKp.png)

As we can see, we have to pass the collection address as a parameter, along with the blockchain name in which the contract resides. To get the contract address of a collection, we access the [Rarible](https://rarible.com/collection/0x23581767a106ae21c074b2276d25e5c3e136a68b/items) website and find the collection by name. There, we’re able to get the contract address, which appears right under the collection’s name.

![](./img/0*HgbUQpYJIziddSHb.png)

We’re now ready to make the first request.

```
curl https://api.rarible.org/v0.1/collections/ETHEREUM:0x23581767a106ae21c074b2276d25e5c3e136a68b
```

We’re then able to retrieve the following information:

```
{
    "id": "ETHEREUM:0x23581767a106ae21c074b2276d25e5c3e136a68b",
    "blockchain": "ETHEREUM",
    "type": "ERC721",
    "name": "Moonbirds",
    "symbol": "MOONBIRD",
    "owner": "ETHEREUM:0x83895f7508926741cd2147c4aac65c30a851cc30",
    "features": ["APPROVE_FOR_ALL"],
    "minters": [],
    "meta": {
        "name": "Moonbirds",
        "description": "A collection of 10,000 utility-enabled PFPs that feature a richly diverse and unique pool of rarity-powered traits. What's more, each Moonbird unlocks private club membership and additional benefits the longer you hold them. We call it nesting – because, obviously.",
        "content": [{
            "@type": "IMAGE",
            "url": "https://lh3.googleusercontent.com/sn5iLHUcNuUO98w_9Z7cat32hiqvVkPYr6tzHUacESg4PePh9M3jySvpttyWWXHD2e8M4PNQqgorU9sUvpX-FHQHXFBiCpKjloC2nA=s120",
            "representation": "ORIGINAL"
        }],
        "externalLink": "https://moonbirds.xyz",
        "sellerFeeBasisPoints": 250,
        "feeRecipient": "ETHEREUM:0xc8a5592031f93debea5d9e67a396944ee01bb2ca"
    },
    "bestBidOffer": {...}
}
```

Let’s examine the received data. With the above response, we can see which blockchain the collection was minted on, what type of NFT it represents (ERC721 vs ERC1155), who is the owner of the collection (in other words, which address deployed the contract) and metadata information (which tells you the collection name, description, etc.).

Moving on, we have the bestBidOffer parameter, which looks like this:

```
"bestBidOrder": {
        "id": "ETHEREUM:0xc84b341bbf8724d3eb0778464e379669987f6dc68419b69b9d6d9e82195f7c1d",
        "fill": "0",
        "platform": "RARIBLE",
        "status": "ACTIVE",
        "makeStock": "633.499",
        "cancelled": false,
        "createdAt": "2022-04-17T16:42:45.598Z",
        "lastUpdatedAt": "2022-04-25T20:40:50Z",
        "takePrice": "633.499",
        "takePriceUsd": "633.7877712868179245043",
        "priceHistory": [{
            "date": "2022-04-19T12:53:30.340Z",
            "makeValue": "633.499",
            "takeValue": "1"
        }, {
            "date": "2022-04-18T15:36:07.181Z",
            "makeValue": "222.38",
            "takeValue": "1"
        }, {
            "date": "2022-04-17T16:42:45.598Z",
            "makeValue": "15.6",
            "takeValue": "1"
        }],
        "maker": "ETHEREUM:0x60f4c86457c1954c0ca963dc03534c3311967beb",
        "make": {
            "type": {
                "@type": "ERC20",
                "contract": "ETHEREUM:0x6b175474e89094c44da98b954eedeac495271d0f"
            },
            "value": "633.499"
        },
        "take": {
            "type": {
                "@type": "COLLECTION",
                "contract": "ETHEREUM:0x23581767a106ae21c074b2276d25e5c3e136a68b"
            },
            "value": "1"
        },
        "salt": "0xb069650f23bbbd630e5503868b730fabc3c3d667a875815a7eab52ff8ab0c8cf",
        "signature": "0x18f05f9ce1a04a4ab3472df33904c0d0c9cdd8dce0332d48b17d3be023e4c3563c15104eacb2b8f529b7d7e4b3c1509fb0d6e28de4871b049a070b5e37410f2d1b",
        "pending": [],
        "data": {
            "@type": "ETH_RARIBLE_V2",
            "payouts": [],
            "originFees": [{
                "account": "ETHEREUM:0x1cf0df2a5a20cd61d68d4489eebbf85b8d39e18a",
                "value": 250
            }]
        }
}
```

Here, we can see the bestBidOffer information related to the collection, which shows the details of an offer someone made to an NFT in this collection. We can also see which platform the offer was created on, if it’s active or not, the value associated with this offer, etc. In addition to the maker and taker parameters, we’re able to see what type of assets are offered. In this example, the maker offers 633 ERC20 tokens from a given address. You can check which token was offered, by typing its address on [etherscan](https://etherscan.io/address/0x6b175474e89094c44da98b954eedeac495271d0f). In this case, the offer was made in DAI tokens. You can also check what the offer maker wants in return, in the “take” parameter. It’s a collection type token from a given contract. In our case, the moonbird collection token.

# Get all NFTs in a collection

Moving on, since NFTs are created inside a collection, the next logical step will be to find all the NFTs in that collection. We will do it by using an [item controller](https://multichain.redoc.ly/v0.1#tag/item-controller) and the [getItemsByCollection](https://multichain.redoc.ly/v0.1#operation/getItemsByCollection) endpoint.

```
curl https://api.rarible.org/v0.1/items/byCollection?collection=ETHEREUM:0x23581767a106ae21c074b2276d25e5c3e136a68b
```

An example of a received response can be seen below.

```
{
    "total": 50,
    "continuation": "1651172244000_0x23581767a106ae21c074b2276d25e5c3e136a68b:533",
    "items": [{...}]
}
```

Since the moonbirds collection contains 10.000 NFTs, we won’t be able to fetch all of them with a single request. With a single request we’re able to get up to 50 items and the continuation string, which allows us to iterate over the next set of items. We just need to make a new request with added continuation string as a query parameter, like this:

```
curl https://api.rarible.org/v0.1/items/byCollection?collection=ETHEREUM:0x23581767a106ae21c074b2276d25e5c3e136a68b&continuation=1650617116000_0x23581767a106ae21c074b2276d25e5c3e136a68b:6208
```

The continuation string will be present until we fetch all of the NFTs. This is an example of how the item JSON looks. As you can see in the response below, you can find all of the information related to the NFT.

```
{
        "id": "ETHEREUM:0x23581767a106ae21c074b2276d25e5c3e136a68b:1474",
        "blockchain": "ETHEREUM",
        "collection": "ETHEREUM:0x23581767a106ae21c074b2276d25e5c3e136a68b",
        "contract": "ETHEREUM:0x23581767a106ae21c074b2276d25e5c3e136a68b",
        "tokenId": "1474",
        "creators": [{
            "account": "ETHEREUM:0x1bcb5e317671cf1931a2095cbc2ff1a1378a2fd4",
            "value": 10000
        }],
        "owners": [],
        "royalties": [{
            "account": "ETHEREUM:0xc8a5592031f93debea5d9e67a396944ee01bb2ca",
            "value": 500
        }],
        "lazySupply": "0",
        "pending": [],
        "mintedAt": "2022-04-16T15:47:56Z",
        "lastUpdatedAt": "2022-04-29T08:28:35Z",
        "supply": "1",
        "meta": {
            "name": "#1474",
            "attributes": [{
                "key": "Eyes",
                "value": "Open"
            }, {
                "key": "Headwear",
                "value": "Halo"
            }, {
                "key": "Body",
                "value": "Crescent"
            }, {
                "key": "Feathers",
                "value": "Purple"
            }, {
                "key": "Background",
                "value": "Yellow"
            }, {
                "key": "Beak",
                "value": "Long"
            }],
            "content": [{
                "@type": "IMAGE",
                "url": "https://live---metadata-5covpqijaa-uc.a.run.app/images/1474",
                "representation": "ORIGINAL",
                "mimeType": "image/png",
                "width": 1008,
                "height": 1008
            }],
            "restrictions": []
        },
        "deleted": false,
        "auctions": [],
        "totalStock": "0",
        "sellers": 0,
        "lastSale": {
            "date": "2022-04-26T00:58:00Z",
            "seller": "ETHEREUM:0xf16e9d68e71fb936cf7d35c4c2b25e1f7d13e70a",
            "buyer": "ETHEREUM:0x9e7e99d56f8cadb8fde5956bc1c9b9ab1550ed2f",
            "value": "1",
            "currency": {
                "@type": "ETH",
                "blockchain": "ETHEREUM"
            },
            "price": "27"
        }
    }
```

Now the fun begins! 🥳 Since you’re able to fetch all of the NFT details, you can use this information to gather orders assigned to it.

# Get information on NFT activities

So far, we know how to fetch collections and NFTs information. Now, we’re gonna learn how we can do the same with NFT activities. We’re gonna elevate an [activity controller](https://multichain.redoc.ly/v0.1#tag/activity-controller) for that.

To start, let’s quickly remember what the activity is. An activity represents any action taken on the blockchain. Examples of activities include: minting, burning, making a bid, buying, etc. Since [Rarible](https://www.rarible.com) has its own custom indexer (for people interested in this topic, we’ll cover it in other articles), it stores all of this data in a database, which you’re free to explore and use.

Activities can be fetched by a number of different parameters. You can get activities by user, item or collection. The structure is similar to the one used in previous requests.

Let’s fetch an activity of type MINT by item, with the following [request](https://multichain.redoc.ly/v0.1#operation/getActivitiesByItem):

```
curl https://api.rarible.org/v0.1/activities/byItem?itemId=ETHEREUM%3A0x23581767a106ae21c074b2276d25e5c3e136a68b%3A293&type=MINT
```

Which provides us with this information:

```
{
    "activities": [{
        "@type": "MINT",
        "id": "ETHEREUM:625ada80037fb52f6c430f01",
        "date": "2022-04-16T15:01:22Z",
        "reverted": false,
        "owner": "ETHEREUM:0xac3b04591aeb4ab599c09207cbfafbab53d9074f",
        "contract": "ETHEREUM:0x23581767a106ae21c074b2276d25e5c3e136a68b",
        "tokenId": "293",
        "itemId": "ETHEREUM:0x23581767a106ae21c074b2276d25e5c3e136a68b:293",
        "value": "1",
        "transactionHash": "0x352486eb8f51d4a600b59e2c10f869d17b3c8b9c42fd900e7dd231722ff59201",
        "blockchainInfo": {
            "transactionHash": "0x352486eb8f51d4a600b59e2c10f869d17b3c8b9c42fd900e7dd231722ff59201",
            "blockHash": "0x8f5943b376319495f447fb2595d454f3f2b38bc8de8e1027d6627f27cde43905",
            "blockNumber": 14597015,
            "logIndex": 288
        }
    }]
}
```

Boom. 💥 You can now see all available activity info, such as type, date, reverted (it tells you if the transaction was indexed but not reflected in the blockchain), etc.

# Rarible Multichain API — Summary

In this article, we gave you an overview of the [Rarible Multichain Protocol API](https://multichain.redoc.ly/v0.1/), which allows you to fetch many different information about NFT collections, activities, and more. We mainly focused on the most used controllers, i.e. [items](https://multichain.redoc.ly/v0.1#tag/item-controller), and [collection](https://multichain.redoc.ly/v0.1#tag/collection-controller) controllers. There are many more, though!

The [Rarible Multichain API](https://multichain.redoc.ly/v0.1) can be used to build your custom apps. It’s free and it allows you to include tons of functionalities out of the box. You can list NFTs, activities, and marketplaces, all without a single line of solidity code.
