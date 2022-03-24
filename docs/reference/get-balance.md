---
title: Get balance with Rarible Protocol
description: The main information about getting balance of your wallets with Rarible Multichain Protocol
---

# Get balance

You can transfer NFTs with Rarible Multichain Protocol in different blockchains.

--8<-- "docs/snippets/preparation-sdk.md"

To get balance of your wallet, use `getBalance` function:

```typescript
import { createRaribleSdk } from "@rarible/sdk"
import { toUnionAddress } from "@rarible/types"
import type { BlockchainWallet } from "@rarible/sdk-wallet/src"
import type { AssetType } from "@rarible/api-client"

async function getBalance(wallet: BlockchainWallet, assetType: AssetType) {
	const sdk = createRaribleSdk(wallet, "dev")
	const balance = await sdk.balances.getBalance(
		toUnionAddress("<YOUR_WALLET_ADDRESS>"),
		assetType
	)
	return balance
}
```

For getting balance from Polygon:

* Matic

    ```typescript
    const balance = await sdk.balances.getBalance(
      toUnionAddress("ETHEREUM:0xc8f35463Ea36aEE234fe7EFB86373A78BF37e2A1"), {
     "@type": "ETH",
     blockchain: Blockchain.POLYGON,
    })
    ```

* ERC20

    ```typescript
    const balance = await sdk.balances.getBalance(
    toUnionAddress("ETHEREUM:0xc8f35463Ea36aEE234fe7EFB86373A78BF37e2A1"), {
    			"@type": "ERC20",
    			contract: toContractAddress("POLYGON:0xa6fa4fb5f76172d178d61b04b0ecd319c5d1c0aa"),
    })
    ```
