---
title: Mint and Lazy Mint in Rarible Protocol
description: The main information about minting in Rarible Multichain Protocol
---

# Mint and Lazy Mint

Here we will figure out how to create mint and lazy mint NFT with Rarible Protocol.

## Preparation

1. [Install and configure](https://docs.rarible.org/union-sdk/#installation) Protocol SDK.
2. [Connect the required wallet](https://docs.rarible.org/union-sdk/#metamask-integration-with-rarible).

***

## Executing actions

You can use SDK to create (mint), trade, transfer, burn NFTs. All actions are handled in the same manner:

* Invoke function from SDK (e.g.: `mint`).
* Async function returns so-called `PrepareResponse` (it's different for different actions).
* `PrepareResponse` contains all needed information to show user a form (for example, response for sell contains all supported currency types).
* Collect input from the user (show form and let user enter the data).
* Pass this data to submit Action.

You can find more information about Action abstraction in dedicated [repo readme]. Or you can use it as a regular async function and work with regular Promises.

***

## Multichain

To mint ERC-721 NFT following parameters are required:

* `URI` — address of data on IPFS
* `supply` — number of NFTs to create (not in every case it is supported, you can check it by reading sdk.nft.mint response under multiple parameters)
* `lazyMint` — boolean, if we want to mint it lazily or normally
* `creators` — the array of creators, which allows distributing profits from sell in accordance to defined criteria
* `royalties` — the array of royalties, which allows taking a defined amount of any consecutive sell

!!! note ""

    Whenever you see the need for Multichain / Contract address, you can create it as follows:

    1. Blockchain Name
    2. Hex Address

    Example:

    `BlockchainName:HexAddress` = `ETHEREUM:0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05`

1. Add values of `URI` and `supply`, for example:

    ```typescript
    const [uri, setUri] = useState<string>(
      "ipfs:/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp"
    );
    const [supply, setSupply] = useState<number>(1);
    
    const currentWallet = wallet as EthereumWallet;
    const makerAccount = await currentWallet.ethereum.getFrom();
    ```

2. Create `PrepareMintRequest`

    Collection ids are the address of Rarible Smart Contracts instance. You can find them on [Contract Addresses page](https://docs.rarible.org/ethereum/contract-addresses/):
    
    ```typescript
    const mintRequest: PrepareMintRequest = {
      // Using Rarible API, tokenId would also be needed, but SDK takes care for that
      collectionId: toContractAddress(
        "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82"
      ),
    };
    ```

3. Get Mint Response

    From `mintResponse` you can extract additional info e.g. is supply > 1 enabled.
    
    ```typescript
    const mintResponse = await sdk.nft.mint(mintRequest);
    
    // If you want to divide profits here, you can add more than one creator object
    // Combined value amount has to be 10000, which equals to 100 %, same with royalties
    const creators = [
      {
        account: `ETHEREUM:${makerAccount}`,
        value: 10000,
      },
    ];
    
    const royalties = [];
    ```

4. Submit Mint Response

    ```typescript
    const submitResponse = await mintResponse.submit({
      uri,
      supply,
      lazyMint: true,
      creators,
      royalties,
    });
    ```

    Example of successful response:
    
    ```typescript
    itemId: "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382047";
    type: "off-chain"
    ```

To check the created item:

* Use the `getItemById` [API method](https://api.rarible.org/v0.1/doc#operation/getItemById)
* Check [Etherscan](https://etherscan.io/)

***

## Ethereum

With Rarible Protocol Ethereum SDK you can mint and lazy mint ERC-721 and ERC-1155 NFT tokens in Ethereum network.

### Mint

Minting is using the `mintAndTransfer` function for ERC-721 and ERC-1155 contracts.

For ERC-721, the function has the following signature:`mintAndTransfer(LibERC721LazyMint.Mint721Data memory data, address to)`.

```
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

```
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

### Lazy Mint

Lazy Minting is supported for ERC-721 and ERC-1155.

<figure markdown>
![Lazy mint](img/eth_4.png){ width="600" }
  <figcaption>Lazy mint</figcaption>
</figure>

To create Lazy Minting:

1. Generate a token ID.
2. Create a Lazy Minting request body that the creator must sign.
3. The creator signs the provided data.
4. Add signature to the request body
5. Send the data to the API.

[See an example](../ethereum/api/create-lazy-minting.md) of creating Lazy Minting by using API.

For more information about Lazy Minting, see [SDK](https://github.com/rarible/ethereum-sdk) page. 

***

## Flow

With Rarible Protocol Flow SDK you can mint Flow NFT tokens.

Mint response represents transaction result extended with `txId` and minted `tokenId`

```typescript
const {
  txId, // transaction id
  tokenId, // minted tokenId
  status, // flow transaction status
  statusCode, // flow transaction statusCode - for example: value 4 for sealed transaction
  errorMessage,
  events, // events generated from contract and include all events produced by transaction, deopsits withdrown etc.
} = await sdk.nft.mint(collection, "your meta info", [])
```

***

## Tezos

With Rarible Protocol Tezo SDK you can mint Tezos NFT tokens.

```typescript
const result = await mint(
  provider: Provider,
  contract: string,
  royalties : { [key: string]: BigNumber },
  supply?: BigNumber,
  token_id?: BigNumber,
  metadata?: { [key: string]: string },
  owner?: string,
)
```

