---
title: Initialize wallets on Rarible Multichain SDK
description: The main information about initializing wallets on Rarible Multichain SDK
---

# Wallets initialization

To use SDK, you have to create a Wallet — abstraction to communicate with real blockchain wallets. Initialize wallets for used blockchains or use Rarible Wallet Connector (in general for frontend). It is possible to use SDK without wallet (for ex. `sdk.balances.getBalance`), but in that case you can't send transactions and sign messages:

```ts
const raribleSdk = createRaribleSdk(undefined, "prod")
```

## Initialize simple wallets

* Ethereum / Polygon

    You can create EthereumWallet with one of the following providers:

    * Web3 instance. For example, Metamask (`window.ethereum`) or HDWalletProvider
    * ethers.providers.Web3Provider
    * ethers.Wallet

    ```ts
    import Web3 from "web3"
    import * as HDWalletProvider from "@truffle/hdwallet-provider"
    import { Web3Ethereum } from "@rarible/web3-ethereum"
    import { ethers } from "ethers"
    import { EthersEthereum, EthersWeb3ProviderEthereum } from "@rarible/ethers-ethereum"
    import { EthereumWallet } from "@rarible/sdk-wallet"
    
    // if using another browser provider (not HD Wallet Provider), you will need to make a connection
    await provider.request({ method: "eth_requestAccounts" })
  
    // creating EthereumWallet with Web3
    const web3 = new Web3(provider)
    const web3Ethereum = new Web3Ethereum({ web3 })
    const ethWallet = new EthereumWallet(web3Ethereum)
    
    // or with HDWalletProvider
    const provider = new HDWalletProvider({
      url: "<NODE_URL>",
      privateKeys: ["0x0..."],
      chainId: 1,
    })
    const web3 = new Web3(provider)
    const web3Ethereum = new Web3Ethereum({ web3 })
    const ethWallet = new EthereumWallet(web3Ethereum)
    
    // creating EthereumWallet with ethers.providers.Web3Provider
    const ethersWeb3Provider = new ethers.providers.Web3Provider(provider)
    const ethersProvider = new EthersWeb3ProviderEthereum(ethersWeb3Provider)
    const ethWallet = new EthereumWallet(ethersProvider)
    
    // creating EthereumWallet with ethers.Wallet
    const ethersWeb3Provider = new ethers.providers.Web3Provider(provider)
    const ethersProvider = new EthersEthereum(new ethers.Wallet(wallet.getPrivateKeyString(), ethersWeb3Provider))
    const ethWallet = new EthereumWallet(ethersProvider)
    
    // Second parameter — is environment: "prod" | "staging" | "dev"
    const raribleSdk = createRaribleSdk(ethWallet, "staging")
    ```


* Flow

    ```ts
    import * as fcl from "@onflow/fcl"
    import { FlowWallet } from "@rarible/sdk-wallet"
    
    const wallet =  new FlowWallet(fcl)
    ```

    You also need to configure Flow Client Library (FCL), because Flow-sdk use [@onflow/fcl-js](link:https://github.com/onflow/fcl-js):

    ```javascript
    //example config for testnet
    import { config } from "@onflow/fcl";
    config({
      "accessNode.api": "https://access-testnet.onflow.org", // Mainnet: "https://access-mainnet-beta.onflow.org"
      "discovery.wallet": "https://fcl-discovery.onflow.org/testnet/authn" // Mainnet: "https://fcl-discovery.onflow.org/authn"
    })
    ```

    See more configuration details on [Flow documentation](https://docs.onflow.org/fcl/tutorials/flow-app-quickstart/#configuration).


* Tezos

    To initialize wallets, you can use:

    * in_memory_provider (also for backend)
    * beacon_provider (@rarible/tezos-sdk/dist/providers/beacon/beacon_provider)

    ```ts
    //in_memory_provider usage example
    import { in_memory_provider } from "@rarible/tezos-sdk/dist/providers/in_memory/in_memory_provider"
    import { TezosWallet } from "@rarible/sdk-wallet"
    
    const provider = in_memory_provider("edsk...", nodeUrl)
    const wallet = new TezosWallet(provider)
    ```

## Wallet Connector

It is better to use Wallet Connector because there is a lot of the logic described above already implemented and the connect function for each blockchain is unified.

--8<-- "docs/snippets/WalletConnectorReadme.md"

[Read more](https://github.com/rarible/sdk/tree/master/packages/connector) about installation and using examples of Rarible SDK Wallet Connector.
