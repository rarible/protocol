# Sell

```typescript
// Putting Item on sale

// First, invoke sell function. It will return an object with some useful information 
const { 
  supportedCurrencies, // List of currencies supported by specific blockchain (ETH, ERC20 etc.)
  maxAmount, // Max amount of the NFT that can be put on sale; you can validate the input from use using this value
  baseFee, // Present it to a user, it's a base protocol fee that is taken on the trade
  submit, // Use this Action to submit information after user input
} = await sdk.order.sell({ itemId })

// Collect information from the user (show the form etc.)
// Then use submit Action to execute this action

submit({
  amount, // Amount of NFTs to put on sale: must be <= maxAmount
})
```

For example, sell ERC-721 by using ERC-20:

```typescript
const wallet1Address = wallet1.getAddressString()
const wallet2Address = wallet2.getAddressString()
await conf.testErc721.methods.mint(wallet1Address, 1, "").send({ from: wallet1Address, gas: 200000 })
await conf.testErc20.methods.mint(wallet2Address, 100).send({ from: wallet1Address, gas: 200000 })
const itemId = toItemId(`${conf.testErc721.options.address}:1`)

await awaitItem(raribleSdk, itemId)

const sellAction = await sdk1.order.sell({ itemId: toItemId(`ETHEREUM:${itemId}`) })
const hash = await sellAction.submit({
	amount: toBigNumber("1"),
	price: toBigNumber("1"),
	currency: { "@type": "ERC20", contract: toUnionAddress(conf.testErc20.options.address) },
})
const [, realHash] = hash.split(":")

await awaitStockToBe(raribleSdk, realHash, 1)

const fillAction = await sdk2.order.fill({ orderId: toOrderId(hash) })

const tx = await fillAction.submit.start({ amount: 1 })
	.runAll()
await tx.wait()

await awaitStockToBe(raribleSdk, realHash, 0)
```
