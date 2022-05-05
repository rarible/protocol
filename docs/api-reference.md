---
title: Rarible Protocol API Reference
description: API references for different blockchain networks working with the protocol
---

# API Reference

## Documentation and base URL

Use these base URLs to access our API on different networks.

`api.rarible.org` or any testnet equivalent is compatible with all blockchains supported by the Rarible Protocol. We also use the term multichain to describe this compatibility case in the docs.

| Documentation                                                                        | Base URL                             | Environments                            |
|:-------------------------------------------------------------------------------------|:-------------------------------------|:----------------------------------------|
| [https://multichain-api.rarible.org](https://multichain-api.rarible.org)                         |                                      | For all environments                    |
| [https://api.rarible.org/v0.1/doc](https://api.rarible.org/v0.1/doc)                 | https://api.rarible.org/v0.1         | Production (Mainnet)                    |
| [https://api-staging.rarible.org/v0.1/doc](https://api-staging.rarible.org/v0.1/doc) | https://api-staging.rarible.org/v0.1 | Staging (Rinkeby, Mumbai)               |
| [https://api-dev.rarible.org/v0.1/doc](https://api-dev.rarible.org/v0.1/doc)         | https://api-dev.rarible.org/v0.1     | Development (Ropsten, Mumbai, Ithaca) |

On the [https://multichain-api.rarible.org](https://multichain-api.rarible.org) page, you can make API requests using the **TryIt** function. To start using:

1. Change environments on the top left side
2. Choose API method
3. Click **Try it** button:
    1. Configure the request parameters if required
    2. Click **Send** button

Also see additional information and API usage examples on the [Search Capabilities](reference/search-capabilities.md) page.

## Environments

The API interacts with different blockchain networks for different environments.

**Production**:

* Ethereum: mainnet
* Tezos: mainnet
* Flow: mainnet
* Polygon: mainnet

**Staging**:

* Ethereum: rinkeby
* Flow: devnet
* Polygon: mumbai

**Development**:

* Ethereum: ropsten
* Tezos: ithaca
* Flow: devnet
* Polygon: mumbai

