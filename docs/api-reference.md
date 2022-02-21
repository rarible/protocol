---
title: Rarible Protocol API Reference
description: API references for different blockchain networks working with the protocol
---

# API Reference

Use these base URLs to access our API on different networks.

`api.rarible.org` or any testnet equivalent is compatible with all blockchains supported by the Rarible Protocol. We also use the term multichain to describe this compatibility case in the docs.

| Base URL                                                                     | Network                                 |
|:-----------------------------------------------------------------------------|:----------------------------------------|
| [https://api.rarible.org/v0.1](https://api.rarible.org/v0.1)                 | Production (Mainnet)                    |
| [https://api-staging.rarible.org/v0.1](https://api-staging.rarible.org/v0.1) | Staging (Rinkeby, Mumbai)               |
| [https://api-dev.rarible.org/v0.1](https://api-dev.rarible.org/v0.1)         | Development (Ropsten, Mumbai, Hangzhou) |
| [https://api-e2e.rarible.org/v0.1](https://api-e2e.rarible.org/v0.1)         | e2e                                     |

Protocol API documentation can be found here:

* [Mainnet](https://api.rarible.org/v0.1/doc)
* [Staging](https://api-staging.rarible.org/v0.1/doc)
* [Development](https://api-dev.rarible.org/v0.1/doc)
* [e2e testing](https://api-e2e.rarible.org/v0.1/doc)

The API interacts with different blockchain networks for different environments.

**Production environments**:

* Ethereum: mainnet
* Tezos: mainnet
* Flow: mainnet
* Polygon: mainnet

**Staging environments**:

* Ethereum: rinkeby
* Flow: devnet
* Polygon: mumbai

**Development environments**:

* Ethereum: ropsten
* Tezos: hangzhou
* Flow: devnet
* Polygon: mumbai

## Usage with SDK

API is pretty easy when it comes to SDK, you can use it with SDK like this:

```typescript
const response = await sdk.apis.order. (function you want to invoke)
```

The most important thing is to remember that there are different endpoints for different environments when it comes to the API.

While changing environments, you would need to change endpoints accordingly because different APIs function in other chains. E.g., there're different endpoints for Rinkeby than for Ropsten. SDK is taking full care of managing that.
