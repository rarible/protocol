Meeting document for dev meeting on the 5th of November.

1. Update on the 12k$ contract upgrade.

When are we going to deploy that fix now that the gas fees seem to have lowered down?

2. Update on Flow. 

Are we still on track to deploy between 8th and the 12nd of November?

3. Bid

### Github

https://github.com/rarible/protocol/issues/140 - > When will the error message / html status be changed?

https://github.com/rarible/protocol/issues/133 - > Has this been fixed? If not, what is an ETA for a fix. 

https://github.com/rarible/protocol/issues/120 - > Have we found a way to implement this?

https://github.com/rarible/protocol/issues/152

https://github.com/rarible/protocol/issues/151 - > B

https://github.com/rarible/protocol-ethereum-sdk/issues/52 -> 


### Discord

```Nick - Ownerfy#8137```

Quote: "simple type, class com.rarible.protocol.dto.RaribleV2OrderFormDto] value failed for JSON property signature due to missing (therefore NULL) value for creator parameter signature which is a non-nullable type"

Answer: 

```Zoomer#5825```

Quote: "Hi frens. I'm trying to parse Rarible trades on Ethereum. I see here in the exchange contract's events that the events with topic0 as 0x268820db288a211986b26a8fda86b1e0046281b21206936bb0e61c67b5c79ef4 have all useful info in the arguments 
But the event with topic0 as 0xcae9d16f553e92058883de29cb3135dbc0c1e31fd7eace79fef1d80577fe482e
does not seem to contain the address of the traded NFT
What is the difference between these two events? And is there any simple way for me to get the contract address of the NFT being traded in the transaction with topic0 as 0xcae9d16f553e92058883de29cb3135dbc0c1e31fd7eace79fef1d80577fe482e?
(Here's a link of what I'm looking at https://etherscan.io/address/0x9757F2d2b135150BBeb65308D4a91804107cd8D6#events)"

Answer:

```alexon#6056```
 
Quote: "are you guys migrating to a new sdk? Just saw the docs link to a new repo.
I ask because I just created a bid with the procotol-ethereum-sdk and I used ETH as the make asset. The issue I'm seeing is that it's not coming back in the bids api from https://api-staging.rarible.com/protocol/v0.1/ethereum/order/bids/byItem.
I made a bit through rarible and that one does show up.
Actually, I noticed it's just because it's marked as INACTIVE. Is there a reason why it's that way?
I know rarible makes you convert eth to weth first to place a bid. But there is no exaplanation on how to do that in the docs. " 

Answer:
