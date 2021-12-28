---
title: Rarible Union Protocol SDK
description: Rarible Union Protocol SDK enables applications to interact with protocol easily: query, issue, trade NFTs on any blockchain supported
---

# Union SDK

Rarible Protocol Software Development Kit enables applications to interact with Rarible protocol easily: query, issue, trade NFTs on any blockchain supported.

Currently, these blockchains are supported:

- Ethereum (mainnet, ropsten, rinkeby)
- Flow (currently on devnet only)
- Tezos (on granada testnet)

## Installation

Using SDK should be fast, easy and intuitive - that's for what we're aiming for.
Below you can see an example of implementation.

1. Install required packages using npm or yarn.

    For most of the projects, apart of the Rarible SDK we'll also need web3.

    ```
    npm install -D @rarible/sdk
    npm install web3
    ```

    or using yarn

    ```
    yarn add @rarible/sdk -D
    yarn add web3
    ```

2. Create a project with the JS framework of your choice (we'll be using NextJS here).

In order to properly set up the Rarible SDK we need to follow some standard web3 practices.

1. Grab ethereum object out of the global window object.
2. Use it to create a new instance of Web3.
3. Create new instance of EthereumWallet class.
4. Create Rarible SDK with a new instance of ethereumWallet, created in previous step.

In code it looks like that (using TypeScript):

```typescript
// Imports
import Web3 from "web3";
import { createRaribleSdk } from "@rarible/sdk";
import { EthereumWallet } from "@rarible/sdk-wallet";

// Code
const { ethereum } = window as any;

const web3 = new Web3(ethereum);
const ethWallet = new EthereumWallet(ethereum);

const raribleSdk = createRaribleSdk(ethWallet, "staging");
```

Boomm! 👊

RaribleSdk object is ready for use.

Few more things:

1. If you're wondering what's "staging" in createRaribleSdk it's environment parameter. We have four options here:

    - prod (mainnet)
    - dev (ropsten)
    - staging (rinkeby)
    - e2e (you probably won't use this)

    The difference between them is the chain Id and the Rarible API endpoint.

2. If you're creating any sort of blockchain application which will interact with users you'll still need to implement connect metamask button in order to get their wallet connected.

## Metamask integration with Rarible

In the previous chapter we talked about how we can initalize Rarible SDK, but it was more theoretical. In actual development, in almost any dApp we'd like to identify users through a wallet address they are using.

At first sight you may think that it's not really related to the Rarible Protocol, but a correct set up is required to use the SDK smoothly and easily.

In this chapter, I will guide you through this process (it's a proposition of implementation, not the only correct way, but widely used). Once you get the idea you can work with that however you'd like.

Below you can find a list of steps that should be taken after the "Connect Metamask" button is clicked.

1. Identify if user has a blockchain provider (i.e. if he has Metamask installed)

    ```typescript
    const getProvider = () => {
      // 1. Getting ethereum object out of global JS object
      if ((window as any).ethereum) {
        const { ethereum } = window as any;
    
        return ethereum;
      }
      // 2. If ethereum property does not exist it means that user needs to install Metamask
      else {
        alert("Please install Metamask");
      }
    };
    
    const provider = getProvider();
    ```

2. Request and get metamask accounts - metamask should pop up in this step, to authorize the app

    ```typescript
    const connect = async () => {
      if (!provider) {
        alert("No provider found!");
      } else {
        // 1. Making metamask request
        await provider.request({ method: "eth_requestAccounts" });
        // 2. Getting currently connected accounts
        const accounts = await provider.request({ method: "eth_accounts" });
    
        if (accounts.length > 0) {
          // First item is always currently used account
          setAccount(accounts[0]);
        }
        // Setting event listener on whenever user has changed account
        provider.on("accountsChanged", (accs: any) => {
          const [currentAccount] = accs;
          setAccount(currentAccount);
        });
      }
    };
    ```

3. Prepare EthereumWallet for RaribleSdk

    ```typescript
    const wallet = () => {
      // 1. Check if provider and currentAccount is successfully set
      if (provider && currentAccount) {
        return new EthereumWallet(
          new Web3Ethereum({ web3: new Web3(provider), from: currentAccount })
        );
      } else {
        return undefined;
      }
    };
    ```

4. Create RaribleSDK

    ```typescript
    // 1. "env" parameter is one of "prod" | "dev" | "staging" | "e2e" mentioned earlier
    const sdk = (env: string) => {
      if (wallet) {
        return createRaribleSdk(wallet, env as any);
      } else {
        return undefined;
      }
    };
    ```

And voila 🚀.

Now we have _real life_ working example with metamask connected and Rarible SDK configured as it should.

Here you can find code used in example in broader picture:
https://github.com/rarible/example/tree/master/src/sdk

## ERC721-NFT Lazy Minting

In order to lazy mint an item following parameters are required:

- URI - address of data on IPFS
- supply - number of NFTs to create (not in every case it is supported, you can check it by reading sdk.nft.mint response under multiple parameter)
- lazyMint - boolean, if we want to mint it lazily or normally
- creators - array of creators, which allows to distribute profits from sell in accordance to defined criteria
- royalties - array of royalties, which allows to take defined amount of any consecutive sell

Disclaimer:
Whenever you see the need of Union / Contract address you can create it as follows:

1. Blockchain Name
2. Hex Address

Example:
BlockchainName:HexAddress
ETHEREUM:0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05

```typescript
// Examplary values of URI and supply
const [uri, setUri] = useState<string>(
  "ipfs:/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp"
);
const [supply, setSupply] = useState<number>(1);

const currentWallet = wallet as EthereumWallet;
const makerAccount = await currentWallet.ethereum.getFrom();

// 1. Create PrepareMintRequest
// Collection ids are the address of Rarible Smart Contracts instance
// You can find them here:
// https://docs.rarible.org/ethereum/contract-addresses/

const mintRequest: PrepareMintRequest = {
  // Using Rarible API, tokenId would also be needed, but SDK takes care for that
  collectionId: toContractAddress(
    "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82"
  ),
};

// 2. Get Mint Response
// From mintResponse you can extract additional info e.g. is supply > 1 enabled
const mintResponse = await sdk.nft.mint(mintRequest);

// If you want to divide profits here you can add more than one creator object
// Combined value amount has to be 10000 which equals to 100 %, same with royalties
const creators = [
  {
    account: `ETHEREUM:${makerAccount}`,
    value: 10000,
  },
];

const royalties = [];

// 3. Submit Mint Response
const submitResponse = await mintResponse.submit({
  uri,
  supply,
  lazyMint: true,
  creators,
  royalties,
});

// Example of successful response
// itemId: "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382047"
//type: "off-chain"
```

## List NFT on sell

To list your NFT on sell, you'll need a token address, the one you get back from

```typescript
await mintResponse.submit();
```

If you want to create sell order immediately after lazy minting your token, you can grab it straight from the response. Otherwise you'll have to fetch it e.g. from API, or even paste it by hand using tokenId, which you can see in Rarible URL when you're on token you want to list.

It's pretty straightforward. All we need is:

- tokenUnionAddress: string e.g. ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382052
- price: number - price in ETH for which we want to list the token (disclaimer: it's not in wei, it's in ETH, so 0.5 equals 0.5 ETH)
- amount: number - quantity of NFT we want to list. In case of ERC721 it's 1
- currency: EthEthereumAssetType - currency which we want to get in return for our token

```typescript
// 1. Examplary values
const tokenUnionAddress: string =
  "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382052";
const ethCurrency: EthEthereumAssetType = {
  "@type": "ETH",
};
const price: number = 1;
const amount: number = 1;

// 2. Create PreapreOrderRequest type object and pass it to sdk.order.sell
const orderRequest: PrepareOrderRequest = {
  itemId: toItemId(tokenUnionAddress),
};

// You can extract info about properties from orderResponse e.g.
// 1. Base fee
// 2. Max Amount
// etc.
const orderResponse = await sdk.order.sell(orderRequest);

// 3. Submit the transaction -> it will pop up the metamask asking you to sign a transaction, signing is free so there should not be any price associated
const response = await orderResponse.submit({
  price,
  amount,
  currency: ethCurrency,
});
// We get order id from response, it can be useful when we want to update sell order
```

## Update listed token price

To update listed token price you need sell order id.

Due to security circumstances you can't update token price to higher than the one created in original sell order. If you want to boost the price up, you need to cancel sell order and create a new one.

```typescript
const price: number = 0.8;
const ethCurrency: EthEthereumAssetType = {
  "@type": "ETH",
};

const orderId =
  "ETHEREUM:0x6e794fd04bcf21ee7f347874aefdf36ec1a7b73b5694760b367a7644765a6368";

const updateOrderRequest: PrepareOrderUpdateRequest = {
  orderId: toOrderId(orderId),
};

const updateResponse = await sdk.order.sellUpdate(updateOrderRequest);

const response = await updateResponse.submit({
  price,
});
```

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
