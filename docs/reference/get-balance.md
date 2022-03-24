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
