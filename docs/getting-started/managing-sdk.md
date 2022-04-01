---
title: Managing SDK and connecting wallets
description: Step-by-step process of setting up Multichain SDK and connecting blockchain wallets
---

# Managing SDK and connecting blockchain wallets

We're glad you're here! It means that you gave us a chance. Now it's our turn.

You are able to do cool things with NFTs using Rarible Protocol like:

* minting
* burning
* selling
* transferring

And basically, everything else that you can imagine. There is just one step in-between, which is setting up an SDK.

The fastest way to set up Multichain SDK is to clone the [template](https://github.com/kolberszymon/sdk-template-updated) which we prepared for you. It already has all the necessary packages installed.

### Configure all wallets you want to use

In order to add a wallet of your choice (like fcl, mew, beacon, flow) you have to append chain it into Connector create in `src/sdk/connectors-setup` file. In sdk-template there is only Metamask implemented, if you want to add other ones, please refer to official tutorial [there](https://github.com/rarible/sdk/tree/master/packages/connector#usage-with-rarible-sdk).

```typescript
// Example of adding new wallet handler
function mapEthereumWallet<O>(
  provider: AbstractConnectionProvider<O, EthereumProviderConnectionResult>
): ConnectionProvider<O, WalletAndAddress> {
  return provider.map((state) => ({
    wallet: new EthereumWallet(
      new Web3Ethereum({ web3: new Web3(state.provider), from: state.address })
    ),
    address: state.address,
  }));
}

const mew = mapEthereumWallet(
  new MEWConnectionProvider({
    networkId: 4,
    rpcUrl: ethereumRpcMap[4],
  })
);
```

After adding all the desired wallets, you have to chain them to the connector, with Metamask being first, in create method. It should look like that:

```typescript
// Adding all wallets which you've earlier initalised
const connector = Connector.create(injected, state)
  .add(torus)
  .add(walletLink)
  .add(mew)
  .add(beacon)
  .add(fcl)
  .add(walletConnect);
```

### Changing buttons appearance

If you want to change buttons appearance (e.g. different one for Metamask, different one for flow), you can do it in `src/sdk/sdk-wallet-connector` file. To be precise, you can do it in the Options function, right where you see the o.option.

Feel free to create a component for every button and just switch the `o.option` which basically is just a string literal of the wallet i.e. "Metamask", "fcl", etc.

```typescript
function Options<C>({ connector, connectionState }: OptionsProps<C>) {
  const options$ = useMemo(() => from(connector.getOptions()), [connector]);
  return (
    <Rx value$={options$}>
      {(options) => (
        <div>
          {options.map((o) => (
            <div key={o.option}>
              <button
                className="p-2 border-radius border-gray-200 border-2"
                onClick={() => connector.connect(o)}
              >
                Connect to {o.option}
              </button>
              {connectionState.status === "connecting" &&
              connectionState.providerId === o.provider.getId()
                ? "Connecting..."
                : null}
            </div>
          ))}
        </div>
      )}
    </Rx>
  );
}
```

### App setup

```typescript
function MyApp({ Component, pageProps }) {
  return (
    <SdkWalletConnector connector={connector}>
      {(sdk, wallet, connection) => {
        return (
          <SDKContext.Provider value={{ sdk, wallet, connection }}>
            <Component {...pageProps} />
          </SDKContext.Provider>
        );
      }}
    </SdkWalletConnector>
  );
}
```

Setup of an App is pretty easy, you basically don't have to change anything there, but if you're curious — SdkWalletConnector is a file where we create buttons from a connector that we defined in the first step. 

It's responsible for showing a different view according to the current connection state. If the user has not connected his wallet, yet it will show a different view, and if he has connected his wallet it will show a Component function, which in that is just the desired page, on which we'll be able to use an SDK.

SDKContext is just a wrapper that holds information about SDK, wallet, and connection, so you can easily, and without any trouble, use it on every page.

```typescript
// Just like that
const { sdk, wallet } = useSdkContext();
```

### TLDR

When setting up the SDK, there are three main files:

* connectors-setup — responsible for desired wallet's configuration
* sdk-wallet-connector — responsible for buttons appearance and wrapping a whole app
* app.js — which we wrap inside `SDKWalletConnector` and `SDKContext`, so we can have easy access to SDK on every page from now on
