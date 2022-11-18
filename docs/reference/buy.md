---
title: Buy NFT with Rarible Protocol
description: How to buy NFT using Rarible Multichain Protocol
---

# Prerequisites

To buy NFT with Rarible Protocol you should have order id for NFT you are interested in - you can get order id with [Rarible API](search-capabilities.md)

You can buy NFTs with Rarible Multichain Protocol on different blockchains.

--8<-- "docs/snippets/preparation-sdk.md"

# Buy an NFT

You can buy any NFTfor which sell order is created

Use `buy` function:

```typescript
import { createRaribleSdk } from "@rarible/sdk"
import { toOrderId} from "@rarible/types"

async function buyNft(orderId: string) {
    const sdk = createRaribleSdk(wallet, "dev")
    
    // Get order info
    const buy = await sdk.order.buy.prepare({							
    orderId: toOrderId(orderId) 
    })
    
    /**
     * Number of NFTs to buy or to sell (in case of accepting bids)
     * amount: number
     * Origin fees, if not supported by the underlying contract, will throw Error
     * originFees?: UnionPart[]
     * Payouts, if not supported by the underlying contract, will throw Error
     * payouts?: UnionPart[]
     * Use infinite approvals (for ERC-20)
     * infiniteApproval?: boolean
     * ItemId for fill collection order
     * itemId?: ItemId | ItemId[]
     * Max fees value. Should be greater than 0. If required and not provided, will throw Error
     * maxFeesBasePoint?: number,
     * Force pay royalties. It's working only on AMM orders
     * addRoyalties?: boolean
    */
    
    // Send transaction
    const result = await buy.submit(
    amount: 1,    //amount of NFTs you want to buy
    )
    // result: IBlockchainTransaction
}
```

* `orderId` —  Id of NFT sale order, has format `${blockchain}:${orderId}`. For example, `ETHEREUM:0x19f487016770542dc6137b06499a4f7b42c9580f12d85d6347964b03b7682143`
* `amount` — amount of NFT tokens you want to buy

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
