Meeting document for dev meeting on the 8th of October. 

###### Addresing the https://api-staging.rarible.com/ to https://ethereum-api.rarible.org/ replacement in the docs.
There are 4 instances where api-staging is used in the docs. 
1. https://docs.rarible.org/example-projects/picnic#api-calls
2. https://docs.rarible.org/exchange/order-discovery#search-orders
3. https://docs.rarible.org/exchange/creating-a-sell-order#creating-an-order
4. https://docs.rarible.org/asset/creating-an-asset#erc1155-lazy-minting

### Github
https://github.com/rarible/protocol-issues/discussions?discussions_q=is%3Aunanswered

I've realised that discussions that are not in the Q&A section won't get indexed in the link above so I've changed the section for a few of them, that's the reason there might be some older questions in there. 

### Discord 
- All members who have a question listed below have been invited to participate in this call
- All members will be notified about the answer to their question privately or in #dev-general (discord)
- Only the past 7 days of unanswered questions are indexed here. 

```Konstantin#3916```

Quote: "The question for lazy mint. Can I mint nft myself from order? For example, I will hit any sales order with a lazy mint, and I just do mint nft. Will the excenge method be able to make a new duplicate nft since the order remains?"
Answer: 

```Rhabdodon#4653```

Quote: "Thanks! Would love an update on how we're addressing this on the protocol. I believe @Eugene Nacu | Rarible has an idea for how we can address this but needs someone to work on it."

"this" meant: "Regarding the opensea bug it's caused by the function in the lazy minting contract that does the minting transfer as it was originally calling the function doing the minting at the Blackhole address and then doing the transfer to the OpenSea address. The fix requires  minting, sending to the creator of the lazy minter address and then to the buyer vs minting and sending from the blackHole address."

"@Eugene Nacu | Rarible do you think a fix to the OpenSea issue would be completed and shipped by the end of the week?"


```alexon#6056```

Quote: "Is there a way to use the protocol-ethereum-sdk in node without having to pass a web3 instance (since I don't need it)"
"I just tried it by configuring a web3 instance in node, but I'm getting FormData is not defined. So I'm guessing the sdk is not meant to be used in node then?"

Answer: 

```Laviniao#9840```

Quote: "Hi, does anyone in this chat know when L2 will be available on rarible?"

"Also, will generative art projects be able to be minted on platforms built on the protocol, in reglf to the smart contract element?"

Answer: 

```Peter Watts#5307```

Quote: "Hi. Is there a delay when adding Royalties to existing external contract? I followed the steps here (https://docs.rarible.org/asset/royalties-on-a-external-collection) and tx is here (https://etherscan.io/tx/0xb5f625595fed64d629818401b61342d1f0443867fa866fe588d442f36804f834) but it doesn't show up when selling on Rarible, nor when querying the API (https://api.rarible.com/protocol/v0.1/ethereum/nft/items/0x819327e005a3ed85f7b634e195b8f25d4a2a45f8:35739319466029867409935893104794648465119721019613204601875682368845852747852?includeMeta=true)"

Answer:

```AzFlin#5259```

Quote: "hey, can we not post a fixed price auction on rarible UI with an expiration date?"

Answer: 

```Alexandr Devyatkin#4906```

Quote: "Hi! Having trouble with local publishing scala-rpc. While using sbt publishM2 i receive this error: unable to locate a valid GitHub token from GitConfig(token). Which token could be used in that case? Thanks in advance. Link to repo: https://github.com/rarible/scala-rpc"

Answer: 

```bold#5220```

Quote: "Hey devs, many of these NFT projects (BAYC, Cool Cats, Pudgy Penguins, etc.) don't have the Rarible Royalties contracts built in. So do they just not receive royalties if traded on Rarible Marketplace, or does Rarible set up some kind of proxy contracts to account for royalties for them?"

"@Eugene Nacu | Rarible just want to confirm that going forward with a custom contract, I'd only have to include the EIP-2981 standard and not the overall RaribleRoyalties contracts found on Rarible's github, right?"

Answer:

```nullren#4914```

Quote: "for properties on an nft detail page, does rarible use the same metadata attributes as opensea? or does it use the enjin properties?
ie following or does rarible have it's own version of this https://docs.opensea.io/docs/metadata-standards"

Answer: 

```NiFTiChristian#7535```

Quote: "I'm using the ethereum sdk to create an order, but I get a 404: https://ethereum-api-staging.rarible.org/v0.1/nft/items/0x03c592e5f277C37A3e8dEE74f743a7972e5BF51B%3A1/lazy 404 has anyone experienced this while using the SDK?"

Answer: 


