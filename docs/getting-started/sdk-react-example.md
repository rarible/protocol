---
title: Rarible SDK React example
description: How to start using Rarible Multichain SDK with React example
---

# Rarible SDK React example

This example will help you get started with the Rarible SDK. It is written using React. See more information with our prepared [Example APP](https://github.com/rarible/sdk/tree/master/packages/example).

## Install dependencies

```shell
yarn add @rarible/connector @rarible/connector-helper
yarn add @rarible/connector-beacon @rarible/connector-fcl @rarible/connector-fortmatic @rarible/connector-iframe @rarible/connector-mew @rarible/connector-phantom @rarible/connector-portis @rarible/connector-solflare @rarible/connector-torus @rarible/connector-walletconnect @rarible/connector-walletlink
yarn add @rarible/sdk @rarible/types
```

## Setup connectors

??? example "Setup connectors"

    ```typescript
    import { NetworkType as TezosNetwork } from "@airgap/beacon-sdk"
    import { RaribleSdkEnvironment } from "@rarible/sdk/build/config/domain"
    import {
    	ConnectionProvider,
    	Connector,
    	IConnectorStateProvider,
    	InjectedWeb3ConnectionProvider,
    } from "@rarible/connector"
    import { FclConnectionProvider } from "@rarible/connector-fcl"
    import { MEWConnectionProvider } from "@rarible/connector-mew"
    import { BeaconConnectionProvider } from "@rarible/connector-beacon"
    import { TorusConnectionProvider } from "@rarible/connector-torus"
    import { WalletLinkConnectionProvider } from "@rarible/connector-walletlink"
    import { WalletConnectConnectionProvider } from "@rarible/connector-walletconnect"
    import { PhantomConnectionProvider } from "@rarible/connector-phantom"
    import { SolflareConnectionProvider } from "@rarible/connector-solflare"
    import type { IWalletAndAddress } from "@rarible/connector-helper"
    import { mapEthereumWallet, mapFlowWallet, mapSolanaWallet, mapTezosWallet } from "@rarible/connector-helper"
    // import { FortmaticConnectionProvider } from "@rarible/connector-fortmatic"
    // import { PortisConnectionProvider } from "@rarible/connector-portis"
    
    
    const ethereumRpcMap: Record<number, string> = {
    	1: "https://node-mainnet.rarible.com",
    	3: "https://node-ropsten.rarible.com",
    	4: "https://node-rinkeby.rarible.com",
    	17: "https://node-e2e.rarible.com",
    	137: "https://polygon-rpc.com",
    	80001: "https://rpc-mumbai.matic.today"
    }
    
    const ethereumNetworkMap: Record<number, string> = {
    	1: "mainnet",
    	3: "ropsten",
    	4: "rinkeby",
    	17: "e2e",
    	137: "polygon",
    	80001: "mumbai"
    }
    
    function environmentToEthereumChainId(environment: RaribleSdkEnvironment) {
    	switch (environment) {
    		case "prod":
    			return 1
    		case "dev":
    			return 3
    		case "e2e":
    			return 17
    		case "staging":
    		default:
    			return 4
    	}
    }
    
    function environmentToFlowNetwork(environment: RaribleSdkEnvironment) {
    	switch (environment) {
    		case "prod":
    			return {
    				network: "mainnet",
    				accessNode: "https://access.onflow.org",
    				walletDiscovery: "https://flow-wallet.blocto.app/authn",
    			}
    		case "dev":
    		case "e2e":
    		case "staging":
    		default:
    			return {
    				network: "testnet",
    				accessNode: "https://access-testnet.onflow.org",
    				walletDiscovery: "https://flow-wallet-testnet.blocto.app/authn",
    			}
    	}
    }
    
    function environmentToTezosNetwork(environment: RaribleSdkEnvironment) {
    	switch (environment) {
    		case "prod":
    			return {
    				accessNode: "https://tezos-node.rarible.org",
    				network: TezosNetwork.MAINNET
    			}
    		case "dev":
    		case "e2e":
    		case "staging":
    		default:
    			return {
    				accessNode: "https://test-tezos-node.rarible.org",
    				network: TezosNetwork.ITHACANET
    			}
    	}
    }
    
    const state: IConnectorStateProvider = {
    	async getValue(): Promise<string | undefined> {
    		const value = localStorage.getItem("saved_provider")
    		return value ? value : undefined
    	},
    	async setValue(value: string | undefined): Promise<void> {
    		localStorage.setItem("saved_provider", value || "")
    	},
    }
    
    export function getConnector(environment: RaribleSdkEnvironment): Connector<string, IWalletAndAddress> {
    	const ethChainId = environmentToEthereumChainId(environment)
    	const ethNetworkName = ethereumNetworkMap[ethChainId]
    	const isEthNetwork = ["mainnet", "ropsten", "rinkeby"].includes(ethNetworkName)
    	const flowNetwork = environmentToFlowNetwork(environment)
    	const tezosNetwork = environmentToTezosNetwork(environment)
    
    	const injected = mapEthereumWallet(new InjectedWeb3ConnectionProvider())
    
    	const mew = mapEthereumWallet(new MEWConnectionProvider({
    		networkId: ethChainId,
    		rpcUrl: ethereumRpcMap[ethChainId]
    	}))
    
    	const beacon: ConnectionProvider<"beacon", IWalletAndAddress> = mapTezosWallet(new BeaconConnectionProvider({
    		appName: "Rarible Test",
    		accessNode: tezosNetwork.accessNode,
    		network: tezosNetwork.network
    	}))
    
    	const fcl = mapFlowWallet(new FclConnectionProvider({
    		accessNode: flowNetwork.accessNode,
    		walletDiscovery: flowNetwork.walletDiscovery,
    		network: flowNetwork.network,
    		applicationTitle: "Rari Test",
    		applicationIcon: "https://rarible.com/favicon.png?2d8af2455958e7f0c812"
    	}))
    
    	let torus = undefined
    	if (isEthNetwork) {
    		torus = mapEthereumWallet(new TorusConnectionProvider({
    			network: {
    				host: ethNetworkName
    			}
    		}))
    	}
    
    	const walletLink = mapEthereumWallet(new WalletLinkConnectionProvider({
    		networkId: ethChainId,
    		estimationUrl: ethereumRpcMap[ethChainId],
    		url: ethereumRpcMap[ethChainId]
    	}, {
    		appName: "Rarible",
    		appLogoUrl: "https://rarible.com/static/logo-500.static.png",
    		darkMode: false,
    	}))
    
    	const walletConnect = mapEthereumWallet(new WalletConnectConnectionProvider({
    		rpc: ethereumRpcMap,
    		chainId: ethChainId,
    	}))
    
    	const phantomConnect = mapSolanaWallet(new PhantomConnectionProvider())
    	const solflareConnect = mapSolanaWallet(new SolflareConnectionProvider({
    		network: environment === "prod" ? "mainnet-beta" : "devnet"
    	}))
    
    	// Providers required secrets
    	// const fortmatic = mapEthereumWallet(new FortmaticConnectionProvider({ apiKey: "ENTER", ethNetwork: { chainId: 4, rpcUrl: "https://node-rinkeby.rarible.com" } }))
    	// const portis = mapEthereumWallet(new PortisConnectionProvider({ appId: "ENTER", network: "rinkeby" }))
    
    	const connector = Connector
    		.create(injected, state)
    		.add(walletLink)
    		.add(mew)
    		.add(beacon)
    		.add(fcl)
    		.add(walletConnect)
    		.add(phantomConnect)
    		.add(solflareConnect)
    	// .add(portis)
    	// .add(fortmatic)
    
    	if (torus) {
    		return connector.add(torus)
    	}
    
    	return connector
    }
    
    ```

## Create connection provider

Connection provider needed for handling blockchain wallet connection and pass connection and SDK objects to React context for using them in any app components.

??? example "Create connection provider"

    ```typescript
    import React, { useEffect, useState } from "react"
    import { createRaribleSdk } from "@rarible/sdk"
    import type { ConnectionState } from "@rarible/connector"
    import { getStateDisconnected, IConnector } from "@rarible/connector"
    import { IRaribleSdk } from "@rarible/sdk/build/domain"
    import type { IWalletAndAddress } from "@rarible/connector-helper"
    import { RaribleSdkEnvironment } from "@rarible/sdk/build/config/domain"
    import { getConnector } from "./connectors-setup"
    
    export interface IConnectorContext {
    	connector?: IConnector<string, IWalletAndAddress>
    	state: ConnectionState<IWalletAndAddress>
    	sdk?: IRaribleSdk
    	walletAddress?: string
    }
    
    export const ConnectorContext = React.createContext<IConnectorContext>({
    	connector: undefined,
    	state: getStateDisconnected(),
    	sdk: undefined,
    	walletAddress: undefined
    })
    
    const environment: RaribleSdkEnvironment  = "development"
    
    export function SdkConnectionProvider({children}: {children: React.ReactNode}) {
    	const [context, setContext] = useState<IConnectorContext>()
    	const [sdk, setSdk] = useState<IRaribleSdk>()
    	const connector = getConnector(environment)
    
    	useEffect(() => {
    		const subscription = connector.connection.subscribe(s => {
    			const sdkInstance = s.status === "connected" ? createRaribleSdk(s.connection.wallet, environment) : undefined
    			setSdk(sdkInstance)
    			const computedContext: IConnectorContext = {
    				connector,
    				state: s,
    				sdk,
    				walletAddress: s.status === "connected" ? s.connection.blockchain + ":" + s.connection.address : undefined,
    			}
    			setContext(computedContext)
    		})
    		return () => subscription.unsubscribe()
    //eslint-disable-next-line react-hooks/exhaustive-deps
    	}, [])
    
    	return <ConnectorContext.Provider value={context!}>
    		{children}
    	</ConnectorContext.Provider>
    }
    ```

## Usage in APP

??? example "Usage in APP"  

    ```typescript
    import React, { useContext, useEffect, useState } from "react"
    import { ConnectorContext } from "../connector/sdk-connection-provider"
    import { ProviderOption } from "@rarible/connector"
    import type { IWalletAndAddress } from "@rarible/connector-helper"
    import { toOrderId } from "@rarible/types"
    
    export function MainPage() {
    	const [options, setOptions] = useState<ProviderOption<string, IWalletAndAddress>[]>([])
    	const connection = useContext(ConnectorContext)
    
    	useEffect(() => {
    		connection?.connector?.getOptions().then(o => {
    			setOptions(o)
    		})
    	}, [connection])
    
    	const connect = async (option: ProviderOption<string, IWalletAndAddress>) => {
    		await connection.connector?.connect(option)
    	}
    	const disconnect = async () => {
    		if (connection?.state.status === "connected" && connection?.state?.disconnect) {
    			await connection?.state?.disconnect()
    		}
    	}
    
    	const someSdkAction = async () => {
    		const prepare = await connection?.sdk?.order.buy({orderId: toOrderId("orderid")})
    		await prepare?.submit({amount: 1})
    	}
    
    	return <div>
    		Connection status: {connection?.state?.status}
    		<div>
    			<button
    				disabled={connection?.state?.status !== "connected"}
    				onClick={disconnect}
    			>
    				Disconnect
    			</button>
    		</div>
    		{options.map((option, i) => {
    			return <div key={option.option}>
    				<button
    					onClick={() => connect(option)}
    					disabled={connection?.state?.status !== "disconnected"}
    				>
    					Connect {option.option}
    				</button>
    			</div>
    		})}
    	</div>
    }
    ```
