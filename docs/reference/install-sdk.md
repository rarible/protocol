---
title: Install Rarible SDK
description: The main information about installing and initializing Rarible Multichain SDK
---

# Install Rarible SDK

```shell
yarn add @rarible/sdk -D
yarn add web3@1.5.0
yarn add tslib@2.3.1
```

If you need to initialize the wallets with ethers, you can install it like this:

```shell
yarn add ethers
```

To make sure the SDK is installed correctly, check version:

```shell
npm view @rarible/sdk version
```

## Initialize wallets

To use SDK, you have to create a Wallet — abstraction to communicate with real blockchain wallets.

Read more about initializing wallets on [Wallets](wallets.md) page.

## Using SDK on client application

SDK is written in TypeScript. You can use typings to explore SDK possibilities.

```ts
import { createRaribleSdk } from "@rarible/sdk"
```

--8<-- "docs/snippets/usage-sdk-on-server.md"
