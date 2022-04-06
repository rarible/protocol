---
title: Tokens conversion with Rarible Multichain SDK
description: The main information about conversion wrapped fungible tokens with Rarible Multichain SDK
---

# Convert to/from wrapped fungible tokens

To convert to/from wrapped fungible tokens, for example, ETH to WETH, `use sdk.balances.convert` function:

```ts
import { Blockchain } from "@rarible/api-client"

//Convert 0.1 ETH to 0.1 wETH (Wrapped Ether)
const tx = await sdk.balances.convert(Blockchain.ETHEREUM, true, "0.1")
await tx.wait()

//Or unwrap 0.1 wETH to 0.1 ETH
const tx = await sdk.balances.convert(Blockchain.ETHEREUM, false, "0.1")
await tx.wait()
```
