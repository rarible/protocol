# Minting

You can mint ERC721 and ERC1155.

Lazy Minting support - token metadata and minting signatures are stored on the Rarible back-end until a buyer fills the order.

## Scenario

1. Call the `MintRequest` function.

    ```typescript
    export type MintRequest = {
	    uri: string
	    supply: number
	    lazyMint: boolean
	    creators?: Creator[]
	    royalties?: Royalty[]
    }
    ```

2. The result of the `PrepareMintResponse` is returned.

    ```typescript
    export interface PrepareMintResponse extends AbstractPrepareResponse<"mint", MintRequest, MintResponse>{
	    multiple: boolean,
	    supportsRoyalties: boolean
	    supportsLazyMint: boolean
    }
    ```

3. Form display.
4. Form confirmation.
5. Sending data using `submit` from `PrepareMintResponse`.

## Parameters

- `URI` - string, required

  This is the suffix for the `tokenURI`. The prefix for Rarible protocol contracts is `ipfs://`

- `supply` - number, required

  The number of tokens to be minted.

- `lazyMint` - boolean, required

  Will the token be minted as lazy or not.

- `creators` - array

  Should contain all the addresses of the token creators with their respective ownership or contribution to the creation.

- `royalties` - array

  Royalties from the NFT contract.

## Examples

...

