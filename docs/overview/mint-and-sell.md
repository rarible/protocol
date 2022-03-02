---
title: Mint and Sell NFTs in Rarible Protocol
description: The main information about minting and selling NFTs in Rarible Multichain Protocol
---

# Mint and Sell

You can prepare Mint and put up on Sale NFTs with Rarible Multichain Protocol in different blockchains.

## Preparation

1. [Install and configure](https://docs.rarible.org/union-sdk/#installation) Protocol SDK.
2. [Connect the required wallet](https://docs.rarible.org/union-sdk/#metamask-integration-with-rarible).

## Minting Multichain

Often you want to list your nft on the sale right after creation. If it's the case for you, you can also use the `mintAndSell` function, which allows you to do exactly that.

1. Create `PrepareMintRequest`

    ```typescript
    const mintRequest: PrepareMintRequest = {
      collectionId: toContractAddress(
        "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82"
      ),
    };
   
    const price: number = 1;
   
    const ethCurrency: EthErc20AssetType = {
      "@type": "ERC20",
      contract: toContractAddress(
        "ETHEREUM:0xc778417e063141139fce010982780140aa0cd5ab"
      ),
    };   
    ```

    * `ContractAddress` — `BlockchainName:HexAddress` = `ETHEREUM:0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05`
    * `BlockchainName`:

        * `ETHEREUM`
        * `FLOW`
        * `TEZOS`
        * `POLYGON`

    * `@type` — payment asset

    `collectionId` also can be the address of Rarible Smart Contracts instance. You can find them on [Contract Addresses](../ethereum/contract-addresses.md) page.

2. Get `mintResponse`

    ```typescript
    const mintResponse = await sdk.nft.mint(mintRequest);
    
    const mintResult = await mintResponse.submit({
      uri: "ipfs:/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp",
      supply: 1,
      lazyMint: false,
      price: 1,
      creators: [
        {
          account: toMultichianAddress(`ETHEREUM:${makerAccount}`),
          value: 10000,
        },
      ],
      currency: ethCurrency,   
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
    * `price` — price per 1 NFT in ETH
    * `creators` — address of the NFT creator
    * `currency` — currency (ETH or specific ERC20 or Tez, Flow, etc.)

    Example of a successful response:

    ```typescript
    itemId: "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382047";
    OrderId: "..."
    ```

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
