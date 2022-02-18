---
title: Rarible Protocol API Reference
description: API references for different blockchain networks working with the protocol
---

# API Reference

Use these base URLs to access our API on different networks.

`api.rarible.org` or any testnet equivalent is compatible with all blockchains supported by the Rarible Protocol. We also use the term multichain to describe this compatibility case in the docs.

| Base URL | Network                         |
| :--- |:--------------------------------|
| [https://api.rarible.org/v0.1/doc](https://api.rarible.org/v0.1/doc) | Production (Mainnet)            |
| [https://api-staging.rarible.org/v0.1/doc](https://api-staging.rarible.org/v0.1/doc) | Staging (Rinkeby)               |
| [https://api-dev.rarible.org/v0.1/doc](https://api-dev.rarible.org/v0.1/doc) | Development (Ropsten, Hangzhou) |
| [https://api-e2e.rarible.org/v0.1/doc](https://api-e2e.rarible.org/v0.1/doc) | e2e                             |

The API interacts with different blockchain networks for different environments.

**Production environments**:

* Ethereum: mainnet
* Tezos: mainnet
* Flow: mainnet
* Polygon: mainnet

**Staging environments**:

* Ethereum: rinkeby
* Flow: devnet
* Polygon: rinkeby

**Development environments**:

* Ethereum: ropsten
* Tezos: hangzhou
* Flow: devnet
* Polygon: ropsten

## Usage with SDK

API is pretty easy when it comes to SDK, you can use it with SDK like this:

```typescript
const response = await sdk.apis.order. (function you want to invoke)
```

The most important thing is to remember that there are different endpoints for different environments when it comes to the API.

While changing environments, you would need to change endpoints accordingly because different APIs function in other chains. E.g., there're different endpoints for Rinkeby than for Ropsten. SDK is taking full care of managing that.
