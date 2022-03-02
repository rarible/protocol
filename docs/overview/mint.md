---
title: Mint NFTs in Rarible Protocol
description: The main information about minting NFTs in Rarible Multichain Protocol
---

# Mint

You can Mint NFTs with Rarible Multichain Protocol in different blockchains.

## Preparation

1. [Install and configure](https://docs.rarible.org/union-sdk/#installation) Protocol SDK.
2. [Connect the required wallet](https://docs.rarible.org/union-sdk/#metamask-integration-with-rarible).

## Minting Multichain

1. Create `PrepareMintRequest`

    ```typescript
    const mintRequest: PrepareMintRequest = {
      collectionId: toContractAddress(
        "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82"
      ),
    };    
    ```

    * ContractAddress — `BlockchainName:HexAddress` = `ETHEREUM:0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05`
    * BlockchainName:

        * `ETHEREUM`
        * `FLOW`
        * `TEZOS`
        * `POLYGON`

    `collectionId` also can be the address of Rarible Smart Contracts instance. You can find them on [Contract Addresses](../ethereum/contract-addresses.md) page.

2. Get `mintResponse`

    ```typescript
    const mintResponse = await sdk.nft.mint(mintRequest);
    
    const mintResult = await mintResponse.submit({
      uri: "ipfs:/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp",
      supply: 1,
      lazyMint: false
    });
   
    console.log(mintResult.itemId)
    if (result.type === MintType.ON_CHAIN) {
      // Wait for transaction receipt and hash if you mint on-chain item, unnecessary if off-chain
      const {hash} = await result.transaction.wait()
    } 
    ```

    * `uri` — address of data on IPFS. Paste the link to JSON file with "image", "name" and other NFT attributes. For example, [https://ipfs.io/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp](https://ipfs.io/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp)
    * `supply` — number of NFTs to create (not in every case it is supported, you can check it by reading `sdk.nft.mint` response under multiple parameters)
    * `lazyMint` — boolean, `false` if you want to mint item on the blockchain, `true` allow to you mint off-chain item without spending the gas
    * `itemId` —  ItemID of your NFT. For example, `ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:1`

    Example of a successful response:

    ```typescript
    itemId: "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382047";
    type: "off-chain"
    ```

To check the created item:

* Use the `getItemById` [API method](https://api.rarible.org/v0.1/doc#operation/getItemById)
* Check [Etherscan](https://etherscan.io/) for Ethereum and Polygon, [Flowscan](https://flowscan.org/) for Flow, or [tezblock](https://tezblock.io/) for Tezos.

You can find more information about Mint in [Rarible Protocol SDK](https://github.com/rarible/sdk#mint). Or you can use it as a regular async function and work with regular Promises.

## Minting in specific blockchain networks

We recommend using the Multichain Protocol for minting tokens. But you can also make Mint on a specific blockchain network.

??? tip "Ethereum"

    With Rarible Protocol Ethereum SDK, you can mint and lazy mint ERC-721 and ERC-1155 NFT tokens in the Ethereum network.
    
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
    * **tokenURI** — suffix for the token URI. The prefix is usually `ipfs://ipfs/`
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
    * **tokenURI** — suffix for the token URI. The prefix is usually `ipfs://ipfs/`
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

??? tip "Flow"

    With Rarible Protocol Flow SDK, you can mint Flow NFT tokens.
    
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

??? tip "Tezos"

    With Rarible Protocol Tezos SDK, you can mint Tezos NFT tokens.
    
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

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
