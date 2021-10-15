Meeting document for dev meeting on the 15th of October.

### Github

https://github.com/rarible/protocol-issues/discussions?discussions_q=is%3Aunanswered

I've recently started also looking through github discussions, and cherry picking the ones with high priority, but for this week all github discussions are either answered or more clarification is needed. 

### Discord 
Some matters have been raised in the #dev-general channel to be discussed in today's meeting. Apart from discussing those, we will also be discussing the questions that weren't properly answered throught the past 7 days, and we'll follow up individually with everyone who's listed down below for a question. 

All people listed below have also been invited to participate this dev call.


```alexon#6056```

Quote: "I was just trying to do this on rinkeby but it failed for me with INCORRECT_LAZY_NFT Invalid creator and signature size. Did this ever work for you?"

Quote 2: "It’s about minting an 1155 with 2+ more creators. The signature part keeps failing because there’s only one signature in the request, mine, and not from the other creators. 
I was just wondering how we could mint an nft with 2+ creators if only one of the creators is the one doing the mint action."

Answer: 

```inartin#9707```

Quote: "Is there an API call that will return ALL types of order activities? 
Not a separate one but all of them at once, MINT, TRANSFER, BURN, BID, LIST, SELL (or MATCH)?

The getNftOrderAllActivities does not have the Sell or MATCH type (it has in the documentation but it was a typo and will be removed from docs)....
So, how do I get all activities in one API call? "

Answer:

```chusla#6031```

Quote: "Should a minted (bought and minted not just lazy minted) nft that's been burned still be visible on rarible.com?  Etherscan shows it's been burned.  Do these also have to be manually deleted in lazy db?  https://etherscan.io/tx/0xb496e0e664c4529020ebd4ba5d2734f0d9aa1ecf2bacaeaa499d7ee1542da5e2. 
Thank you! trying to come with a plan of action to clear the collection for new mints 
If they do need to be manually deleted can we include in list of items to be cleared this week?  
Thank you!"

Answer: "If it was fully burned, it should not appear on .com" 

Quote: "Thanks Eduard we might want to test or check this if you burn an item even in rinkeby after it's been bought or minted it just goes back to the original owner.  The original owner can then put it back in for sale and then it can get purchased again!

![image](https://user-images.githubusercontent.com/39627934/137510284-7f2cd97b-9a43-4aa2-bc88-8fe0d1466035.png)

Fyi screen above shows history of an item that was put back on sale AFTER being burned.  I am have confirmed in rinkeby that this item can also be repurchased a second time by the buyer after it was burned."

Andrew has also opened an issue here: https://github.com/rarible/protocol-issues/issues/135

Answer:  

```mynamebrody#5466```

Quote: "Don't have time at the moment to write up an issue, but the production API endpoint for bidsByItem has "valueDecimal": null, under the make object, where in the rinkeby/ropsten version of the API return the value field as ETH instead of GWEI"

Answer: 

```tgb2929#1533```

Quote: "When creating a sell order using the SDK, if we want to sell for Ether, what do we input here: "takeAssetType: {        assetClass: "ERC20",        contract: contractErc20Address    }"
https://docs.rarible.org/sdk#create-sell-order"

Quote 2: "I'm using the SDK to create Buy orders. The issue is that almost always on the first buy attempt, the estimated gas fee is several Ether, which isn't really true. If I close and try again, then usually it's more reasonable.
Anyone know how to deal with handling buy orders and showing reasonable gas fees?"

Answer: 

```lazycaramel#4474```

Quote: "Hey guys, I was interested if I could use ERC1155Factory directly, or should I use SDK?
Also, what's the caveat to using this vs deploying my own ERC1155? Is there some kind of lock-in with Rarible taking 2.5% on each token sale even outside of the platform?"

Answer: 

```Rhabdodon#4653```

Quote: "We've been experiencing a tremendous amount of interest and usage of cocoNFT which is amazing! Want to first thank you all for the support along the way! ❤️ 

I also wanted to share the 5 biggest pieces of feedback we're getting from users that are related to the protocol.

1. Users want to be able to burn lazy minted NFTs without paying gas fees. There is certainly confusion around this. 

2. Users also want to be able to remove lazy minted NFTs from sale without paying gas fees. 

3. Users want more sale types supported (i.e. auctions for 721 and Open for Bids for 1155s). We're on an 1155 collection so the latter would be particularly helpful. 

4. Users want to setup their Rarible profile within cocoNFT. They don't understand why they have 2 different profiles. I really think the Rarible protocol could do something cool here for the ecosystem by building a unified profile system similar to what exists on Tezos but maybe the Rarible one is cross-chain. 

5. Users want to change the price for their lazy minted NFTs (I believe this is coming soon!)"

Answer: 

```agamanin#2389```

Quote: "Hi. I'm new to the community, glad to be here. I have a question about the protocol smart contracts licensing. There is no LICENCE file on github. Some research indicates that it means 'forbidden for private or commercial use' (i.e. https://github.com/github/choosealicense.com/issues/196). Does it basically mean one cannot fork it, then adapt to her own needs (i.e. change the protocol fees structure, and the fee recipient address) and run her own markeplace? 🙂
An open github issue with similar question does not make it more transparent as well
Also, 77 forks (at the moment of writing) would only make sense for educational purposes in this case, right?"

Answer - Eduard: AFAIK, anyone is allowed to fork and use rarible-protocol code for their own projects and whatnot. It's open source.

Quote: "Wow, that would be just great. BTW, as far as I can understand, tools like https://one2all.io/ already do this - they let anyone set an arbitrary fee recipient and assign the fee structure. But they may have special permission of Rarible to do that, I don't know. Anyhow, having a more explicit license stating what can be done and what cannot would be beneficial for everyone."

Answer - Eugene: 

```Unnatural Space#0655```

Quote: "is the rarible protocol compatible with polygon network?"

Answer - Eduard: I'd have answered that it's in the plans to be implemented soon, but Eugene, it'd be best for a more accurate answer. 

Answer - Eugene: 

```chusla#6031```

Quote: "Hi all question on sdk.  My recent understanding is that the mint function automatically generates the contract token ID.  But how does this work with including token id in external URI in Json metadata?  Don't we need to generate token id before Json/ipfs upload and then mint?  Any thoughts on this much appreciated.  Seems like there may be an order of operations issue here?  I've been doing some testing and think lack of token id on external URI May cause issue with opensea rendering. Previously we were able to do in two steps. Generate token id, then get ipfs content id then mint.  Would be great to discuss on today's call thanks!"

Answer: 
