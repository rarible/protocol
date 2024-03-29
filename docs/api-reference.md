---
title: Rarible Protocol API Reference
description: API references for different blockchain networks working with the protocol
---

# API Reference

## Documentation and base URL

<span style="color:#541e18">**ATTENTION: Flow blockchain is temporary out of support - no data is provided on API for Flow blockchain, direct API calls with FLOW blockchain specified are ruturning ERROR 400 "Flow is not supported"**</span>

Use these base URLs to access our API on different networks.

`api.rarible.org` or any testnet equivalent is compatible with all blockchains supported by the Rarible Protocol. We also use the term multichain to describe this compatibility case in the docs.

| Documentation                                                                | Base URL                             | Environments                          |
|:-----------------------------------------------------------------------------|:-------------------------------------|:--------------------------------------|
| [multichain-api.rarible.org](https://multichain-api.rarible.org)             |                                      | For all environments                  |
| [api.rarible.org/v0.1/doc](https://api.rarible.org/v0.1/doc)                 | https://api.rarible.org/v0.1         | Production (Mainnet)                  |
| [testnet-api.rarible.org/v0.1/doc](https://dev-api.rarible.org/v0.1/doc)     | https://testnet-api.rarible.org/v0.1 | Development (Rinkeby, Mumbai, Ithaca) |

On the [multichain-api.rarible.org](https://multichain-api.rarible.org) page, you can make API requests using the **TryIt** function. To start using:

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
* Solana: mainnet-beta
* Immutablex: mainnet

**Testnet**:

* Ethereum: rinkeby
* Tezos: ithaca
* Flow: devnet
* Polygon: mumbai
* Solana: devnet
* Immutablex: ropsten

