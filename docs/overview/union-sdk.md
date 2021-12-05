# SDK Overview

Rarible Protocol Software Development Kit enables applications to interact with Rarible protocol easily: query, issue, trade NFTs on any blockchain supported.

Currently, these blockchains are supported:

- Ethereum (mainnet, ropsten, rinkeby)
- Flow (currently on devnet only)
- Tezos (on granada testnet)

## Installation

Using SDK should be fast, easy and intuitive - that's for what we're aiming for.
Below you can see examplary implementation.

1. Install needed packages with npm or yarn
   For most of the projects, apart of RaribleSDK we'll also need web3

```
npm install -D @rarible/sdk
npm install web3
```

or using yarn

```
yarn add @rarible/sdk -D
yarn add web3
```

2. Create a project with choosen JS framework (I'm going with NextJS here)

In order to properly set up RaribleSDK we need to follow standard web3 practices.

1. Grab ethereum object out of the global window object
2. Use it to create a new instance of Web3
3. Create new instance of EthereumWallet class
4. Create Rarible SDK with a new instance of ethereumWallet, created in previous step

In code it looks like that (using TypeScript):

```
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
   - e2e (you'll probably won't use it)
     The difference between them is chain Id and RaribleAPI endpoint.
2. If you're creating any sort of blockchain application which will interact with users you'll still need to implement connect metamask button in order to get their wallet connected.

See more information about usage Protocol SDK on [https://github.com/rarible/sdk](https://github.com/rarible/sdk)
