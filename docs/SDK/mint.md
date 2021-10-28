# Minting

1. Invoke the Mint function.
2. The result of the `PrepareMintResponse` is returned. It has everything you need to display the form.
3. Collect information from the user (show the form etc).
4. Form confirmation.
5. Sending data using `submit`.

For example, minting ERC-1155:

```typescript
const sender = await ethereum.getFrom()

const action = await sdk.nft.mint({
	collection: {
		features: ["MINT_AND_TRANSFER"],
		id: erc1155Address,
		name: "Test-collection",
		type: "ERC1155",
	},
})

const result = await action.submit.start({
	uri: "uri",
	creators: [{ account: toUnionAddress(sender), value: toBigNumber("10000") }],
	royalties: [],
	lazyMint: false,
	supply: 1,
}).runAll()

if (result.type === MintType.ON_CHAIN) {
	await result.transaction.wait()
}
```

For more information, see [mint.ts](https://github.com/rarible/sdk/blob/master/packages/sdk/src/sdk-blockchains/ethereum/mint.ts).

## Parameters

- `URI` - string, required

    This is the suffix for the `tokenURI`. The prefix for Rarible protocol contracts is `ipfs://`

- `supply` - number, required

    The number of tokens to be minted.

- `lazyMint` - boolean, required

    Does the network supports lazyMint or not.

- `creators` - array

    Should contain all the addresses of the token creators with their respective ownership or contribution to the creation.

- `royalties` - array

    Royalties from the NFT contract.
