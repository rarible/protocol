---
title: API Usage with Rarible Protocol SDK
description: API Usage with Rarible Protocol SDK for different blockchain networks
---

# API Usage with SDK

You can find all available endpoints on [API Reference](https://docs.rarible.org/api-reference/) page.

API is pretty easy when it comes to SDK, you can use it with SDK like this:

```typescript
const response = await sdk.apis.order. (function you want to invoke)
```

The most important thing is to remember that there are different endpoints for different environments when it comes to the API.

While changing environments, you would need to change endpoints accordingly because different APIs function in other chains. E.g., there're different endpoints for Rinkeby than for Ropsten. SDK is taking full care of managing that.

Mainnet environments:

* eth: mainnet
* tezos: mainnet
* flow: mainnet
* solana: mainnet

Testnet environments:

* eth: rinkeby
* tezos: hangzhou
* flow: devnet
* solana: testnet

The best documentation here is to explore SDK by holding CTRL / CMD and the left button to see the available endpoints and needed parameters.
