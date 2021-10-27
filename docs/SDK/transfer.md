# Transfer

For example, transfer ERC-1155:

```typescript
const sender = await senderEthereum.getFrom()
const receipent = await receipentEthereum.getFrom()

const tokenId = "1"
const itemId = toItemId(`${it.testErc1155.options.address}:${tokenId}`)
await it.testErc1155.methods.mint(sender, tokenId, 100, "123").send({ from: sender, gas: 200000 })

await awaitItem(raribleSdk, itemId)

const transfer = await senderSdk.nft.transfer({ itemId })
const tx = await transfer.submit.start({
	to: toUnionAddress(receipent),
	amount: 10,
}).runAll()

await tx.wait()

const balanceRecipient = await it.testErc1155.methods.balanceOf(receipent, tokenId).call()
expect(balanceRecipient).toBe("10")
```
