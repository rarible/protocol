---
title: Sdk Setup Tutorial
description: Step by step process of setting up Multichain SDK
---

# Multichain SDK

We're glad you're here! It means that you gave us a chance. Now it's our turn.
You are able to do cool things with NFTs using Rarible Protocol like:

- minting
- burning
- selling
- transfering

And basically everything else what you can imagine.
There is just one step in-between which is setting up an SDK.
Of course that you just can use a [template](https://github.com/kolberszymon/union-sdk-template.git) which we prepared for you and have it all set up in no time. Nevertheless, sometimes you just want to know what's under the hood and how to set it up from scratch. That's what we'll do in this document. Are you as excited as me? Let's get started

### The Fastest Way to set up Multichain SDK

Clone the [template](https://github.com/kolberszymon/union-sdk-template.git) which we prepared for you and choose wallets you want to use in \_app.tsx file.

```javascript
// In order to use the desired blockchain you need to pick the desired wallet
// Currently supported wallets are:
// Metamask, Torus, Walletlink, Mew, Beacon, Fcl

<SdkWalletConnector connector={connector} desiredWallets={["fcl"]}>
  {(sdk, wallet, connection) => {
    return (
      <SDKContext.Provider value={{ sdk, wallet, connection }}>
        <Component {...pageProps} />
      </SDKContext.Provider>
    );
  }}
</SdkWalletConnector>
```

Afterward, you're able to use SDK in all the following files just by extracting it out of SdkContext, like that:

```javascript
import { useSdkContext } from "../context/SDKContext";

const { sdk, wallet } = useSdkContext();
```

All of the needed functionality is already provided here :)

### The Multichain SDK Setup Breakdown

If you're still reading, it means that you want to break setup down a little.
That's perfectly fine, I also like to be aware of what I'm doing (most of the time).
We're gonna start with discussing app wrappers because that's what provides us with the whole app availability of SDK.

```javascript
<SdkWalletConnector connector={connector} desiredWallets={["fcl"]}>
  {(sdk, wallet, connection) => {
    return (
      <SDKContext.Provider value={{ sdk, wallet, connection }}>
        <Component {...pageProps} />
      </SDKContext.Provider>
    );
  }}
</SdkWalletConnector>
```

As you can see we have two context wrappers here:

- SDKWalletConnector - responsible for providing the right buttons, so we can connect users to right blockchains
- SDKContext - responsible for storing retrieved objects

First, we're gonna decompose SDKContext

#### SDKContext

##### SDKContext Structure

```javascript
import { IRaribleSdk } from "@rarible/sdk/build/domain";
import { BlockchainWallet } from "@rarible/sdk-wallet";
import { createContext, useContext } from "react";
import { Maybe } from "../common/maybe";
import type { ConnectionState } from "@rarible/sdk-wallet-connector";

type ContextProps = {
  sdk: IRaribleSdk,
  connection: ConnectionState<BlockchainWallet>,
  wallet: Maybe<string>,
};

export const SDKContext = createContext < Partial < ContextProps >> {};
export const useSdkContext = () => useContext(SDKContext);
```

SDKContext job is to store values that we retrieve from SDKWalletConnector. We have an SDK property here, which stores an SDK object. We have a connection property which tells us what is the wallet connection state (connected, connecting, initializing, etc.). We also have a wallet property which provides us with currently connected and chosen wallets (as you can see it can be null if no wallet is currently connected).

##### SDKContext Usage

```javascript
import { useSdkContext } from "../context/SDKContext";

const { sdk, wallet } = useSdkContext();

...

const orderResponse = await sdk.order.sell(orderRequest);
```

#### SDKWalletConnector

##### SDKWalletConnector Structure

This file is a little bigger than SDKContext so we won't paste it here, but feel free to see it [here](https://github.com/kolberszymon/union-sdk-template/blob/main/src/sdk/sdk-wallet-connector.tsx).

Now we'll break it down, one step at a time :).

**ConnectorComponentProps**

```javascript
export type ConnectorComponentProps = {
  connector: IConnector<string, BlockchainWallet>,
  desiredWallets: Array<string>,
  children: (
    sdk: IRaribleSdk,
    walletAddress: Maybe<string>,
    connection: ConnectionState<BlockchainWallet>
  ) => JSX.Element,
};
```

Here we define what props are allowed:

- connector - handle providers, connection state, etc. Basically all of the stuff which we need in order to be able to interact with the blockchain
- desiredWallet - an array of wallets for which we want buttons to connect, e.g. if you put "metamask" here you'll get a button that will connect you with a Metamask account
- children is a JSX element that we return

When it comes to things we can alter here connector is definitely **not** one of them. It's handling heavy logic which is responsible for connecting to the proper blockchain after clicking a button.

Desired wallets is a place to go. Going further we have Options function which is responsible for showing buttons. It looks like that:

```javascript
function Options<C>({
  connector,
  connectionState,
  desiredWallets,
}: OptionsProps<C>) {
  const options$ = useMemo(() => from(connector.getOptions()), [connector]);

  return (
    <Rx value$={options$}>
      {(options) => (
        <div>
          <p>Connect to:</p>
          {options
            .filter((o) =>
              desiredWallets.length > 0
                ? desiredWallets.includes(o.option)
                : true
            )
            .map((o) => (
              <div key={o.option}>
                <button
                  onClick={() => {
                    connector.connect(o);
                  }}
                >
                  {o.option}
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

As you can see filtering is happening here:

```javascript
options.filter((o) =>
  desiredWallets.length > 0 ? desiredWallets.includes(o.option) : true
);
```

So if you're interested in styling a button you should do it there:

```javascript
<button
  onClick={() => {
    connector.connect(o);
  }}
>
  {o.option}
</button>
```

And that's all you need to know.
I hope that this explanation had help you in SDK setup understanding and that now you can do it like a pro.
