# Tokens

The Rarible protocol for Ethereum supports two types of tokens:

* [ERC-721](https://eips.ethereum.org/EIPS/eip-721 ) is a standard interface for non-interchangeable tokens. This type of token is unique and may have a value different from the value of another token from the same smart contract.
* [ERC-1155](https://eips.ethereum.org/EIPS/eip-1155 ) is a standard interface for contracts that manage multiple types of tokens. One deployed contract can include any combination of interchangeable tokens, non-interchangeable tokens, or other configurations.

You can mint both types of tokens as follows:

* A regular minting in a blockchain network using a contract.
* Lazy minting - minting of the token occurs outside the blockchain network. Entry into the blockchain and payment for gas is made when purchasing or transferring the token.

Users can create tokens in different smart contracts.

Tokens also support saving information about Royalties and information about all creators.

## Token Factories

To create ERC-721 and ERC-1155 smart contracts, use our Token Factories. The addresses are available on the [Contract Addresses](../contract-addresses.md) page.

Using Token Factories, you can create the following types of smart contracts:

* Public ERC-721 and ERC-1155
* Private ERC-721 and ERC-1155

Token Factories create [beacon proxy servers](https://docs.open zeppelin.com/contracts/3.x/api/proxy#BeaconProxy). The Rarible Protocol can automatically update these contracts when all token contracts are updated.

## Minting

Minting is using the mintAndTransfer function for ERC-721 and ERC-1155 contracts.

For ERC-721, the function has the following signature:`mintAndTransfer(LibERC721LazyMint.Mint721Data memory data, address to)`.

```typescript
struct Mint721Data {
        uint tokenId;
        string tokenURI;
        address[] creators;
        LibPart.Part[] royalties;
        bytes[] signatures;
}
```

* **tokenId** — **tokenId** of the ERC-721 standard
* **tokenURI** — suffix for the token URI. The prefix is usually `ipfs:/`
* **creators** — an array of authors addresses
* **royalties** — royalty array
* **signatures** — array of signatures. Each creator must have a signature. The only exception is when the creator sends a Mint transaction.

For ERC-1155, the function has the following signature: `mintAndTransfer(LibERC1155LazyMint.Mint1155Data memory data, address to, uint256 _amount)`.

```typescript
struct Mint1155Data {
        uint tokenId;
        string tokenURI;
        uint supply;
        address[] creators;
        LibPart.Part[] royalties;
        bytes[] signatures;
}
```

* **tokenId** — **tokenId** of the ERC-1155 standard
* **tokenURI** — suffix for the token URI. The prefix is usually `ipfs:/`
* **supply** — total number of tokens for minting
* **creators** — an array of authors addresses
* **royalties** — royalty array
* **signatures** — array of signatures. Each creator must have a signature. The only exception is when the creator sends a Mint transaction.

## Lazy Minting

![](../img/eth_4.png)

Lazy Minting is supported for ERC-721 and ERC-1155.

To create Lazy Minting:

1. Generate a token ID.
2. Create a Lazy Minting request body that the creator must sign.
3. The creator signs the provided data.
4. Add signature to the request body
5. Send the data to the API.

[See an example](../api/create-lazy-minting.md) of creating Lazy Minting by using API.

For more information about Lazy Minting, see [SDK](https://github.com/rarible/ethereum-sdk) page. 

## Transfer

This function transfers the token from the sender to the new owner.

Arguments:

* **owner: Address** — address of the asset owner
* **asset: Asset** — asset type

The function checks the asset type and performs one of the following functions:

- **transferErc721**
- **transferErc1155**

transferErc1155 arguments:

```typescript
export async function transferErc1155(
	ethereum: Ethereum,
	send: SendFunction,
	contract: Address,
	from: Address,
	to: Address,
	tokenId: string | string[],
	tokenAmount: string | string[]
```

* **contract: Address** — contract address ERC-1155
* **from: Address** — address of the ERC-1155 token owner
* **to: Address** — address of the new owner
* **tokenId: string | string[]** — token ID or token array for transfer
* **tokenAmount: string | string[]** — number of ERC-1155 tokens or an array of tokens for transfer

transferErc721 arguments:

```typescript
export async function transferErc721(
	ethereum: Ethereum,
	send: SendFunction,
	contract: Address,
	from: Address,
	to: Address,
	tokenId: string
```

* **contract: Address** — contract address ERC-721
* **from: Address** — address of the ERC-721 token owner
* **to: Address** — address of the new owner
* **tokenId: string | string[]** — token ID for transfer

## Deploy

TODO

## Burn

To Burn a token, call the function:

```typescript
const hash = await sdk.nft.burn({
	contract: contractAddress,
	tokenId: toBigNumber(tokenId),
})
```

* **contract** — smart contract address
* **tokenId** — token identifier
