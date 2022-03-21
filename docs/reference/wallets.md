---
title: Initialize wallets on Rarible Multichain SDK
description: The main information about initializing wallets on Rarible Multichain SDK
---

# Wallets initialization

To use SDK, you have to create a Wallet — abstraction to communicate with real blockchain wallets.

1. Use Rarible SDK Wallet Connector

    Create `Connector`, add all needed `ConnectionProvider's`
    
    ```ts
    import { Connector, InjectedWeb3ConnectionProvider, DappType } from "@rarible/connector"
    import { WalletConnectConnectionProvider } from "@rarible/connector-walletconnect"
    // create providers with the required options
    const injected = new InjectedWeb3ConnectionProvider()
    const walletConnect = new WalletConnectConnectionProvider()
    	
    // create connector and push providers to it 
    const connector = Connector
        .create([injected, walletConnect])
    		
    // subscribe to connection status
    connector.connection.subscribe((con) =>
        console.log("connection: " + JSON.stringify(con))
    )
    const options = await connector.getOptions(); // get list of available option
    await connector.connect(options[0]); // connect to selected provider
    ```

2. Initialize wallets

    See [code example](https://github.com/rarible/sdk/tree/master/packages/connector#usage-with-rarible-sdk) in the repository for initialize wallets with Wallet Connector.
    
    **Ethereum / Polygon**
    
    ```ts
    import Web3 from "web3"
    import { Web3Ethereum } from "@rarible/web3-ethereum"
    import { EthereumWallet } from "@rarible/sdk-wallet"
    const web3 = new Web3(provider)
    const web3Ethereum = new Web3Ethereum({ web3 })
    const ethWallet = new EthereumWallet(web3Ethereum)
    // Second parameter — is environment: "prod" | "staging" | "e2e" | "dev"
    const raribleSdk = createRaribleSdk(ethWallet, "staging")
    ```
    
    **Flow**
    
    ```ts
    import * as fcl from "@onflow/fcl"
    import { FlowWallet } from "@rarible/sdk-wallet"
    const wallet =  new FlowWallet(fcl)
    ```
    
    You also need to configure Flow Client Library (FCL) for using Flow. See more information on [Configure fcl](https://docs.rarible.org/flow/flow-sdk/#configure-fcl).
    
    **Tezos**
    
    Use [Wallet Connector](https://github.com/rarible/sdk/tree/master/packages/connector#usage-with-rarible-sdk) to initialize wallet for Tezos.
