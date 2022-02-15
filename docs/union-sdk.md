---
title: Rarible Protocol Multichain SDK
description: Rarible Protocol Multichain SDK enables applications to interact with protocol easily: query, issue, trade NFTs on any blockchain supported
---

# Rarible Protocol SDK

## Overview

Rarible creates Multichain SDK, an abstraction of complicated blockchain logic underneath, allowing end-users to interact with the blockchain to create some sorts of assets (ERC721, ERC1155) and list them to sell, trade, etc.

In other words, Multichain SDK is ready to go, NFT marketplace functionality, which you can use out of the box.

Currently, Rarible Protocol SDK supports following blockchains:

* Ethereum (mainnet, ropsten, rinkeby)
* Flow (mainnet, ropsten, rinkeby)
* Tezos (mainnet, granada)
* Polygon (mainnet, mumbai)

## Installation

Using SDK should be fast, easy and intuitive — that's for what we're aiming for. Below you can see an example of implementation.

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

In code, it looks like that (using TypeScript):

```typescript
--8<-- "docs/snippets/usage-sdk.md"
```

`RaribleSdk` object is ready for use.

Few more things:

1. If you're wondering what's "staging" in `createRaribleSdk` it's environment parameter. We have four options here:

    * `prod` (mainnet)
    * `dev` (ropsten)
    * `staging` (rinkeby)
    * `e2e` (you probably won't use this)

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

--8<-- "docs/snippets/usage-sdk-on-server.md"

Now we have the working example with Metamask connected and Rarible SDK configured.

[Here](https://github.com/rarible/example/tree/master/src/sdk) you can find code used in example in broader picture.

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
