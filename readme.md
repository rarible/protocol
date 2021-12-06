# Rarible Protocol Overview

Rarible Protocol is a tool to query, issue and trade NFTs on these blockchains:

- [Ethereum](./ethereum/ethereum-overview.md)
- [Flow](./flow/flow-overview.md) (WIP, currently on devnet)
- [Tezos](./tezos/tezos-overview.md) (WIP, currently on granada testnet)
- Polygon (WIP, coming soon)
- Other blockchains ([tell us](https://github.com/rarible/protocol/discussions) what blockchain you want)

## Getting Started

- Install and start to use [Protocol SDK](docs/overview/union-sdk.md)
- Use [Protocol API](docs/overview/api-reference.md)

Look at [Example App](docs/getting-started/protocol-example.md) for a quick start.

## Protocol Features

- [query](https://github.com/rarible/sdk#querying) information about NFTs
- [mint](https://github.com/rarible/sdk#mint) (issue, create) NFTs
- trade NFTs ([sell](https://github.com/rarible/sdk#sell), [bid](https://github.com/rarible/sdk#bid), [auction](https://github.com/rarible/sdk#auction))
- [transfer](https://github.com/rarible/sdk#transfer)
- [burn](https://github.com/rarible/sdk#burn)

## Architecture

The architecture of the Protocol:

![](docs/overview/img/union_architecture.png)

Protocol is based on the blockchain layer (smart contracts written for every blockchain supported). These smart contracts allow users to mint and exchange tokens.

On top of the contracts we built indexers to index part of the blockchain state. This gives us the possibility to query data about NFTs.

Then, SDKs were written to interact with smart contracts.

All these components are written for every blockchain supported and are used in [Union service](https://github.com/rarible/union-service) and [Union SDK](https://github.com/rarible/sdk)

Applications need to integrate [Union service](https://github.com/rarible/union-service) and [Union SDK](https://github.com/rarible/sdk) to be able to interact with all blockchains in the same way.

## Suggestions

You are welcome to [suggest features](https://github.com/rarible/protocol/discussions) and [report bugs found](https://github.com/rarible/protocol/issues)!

## Audits

Rarible Protocol is audited. Check this report by [ChainSecurity.com](https://chainsecurity.com/security-audit/rarible-exchange-v2-smart-contracts/).

## License

Rarible Protocol is available under [GPL v3](docs/LICENSE).

SDK and openapi (with generated clients) are available under [MIT](docs/MIT-LICENSE).
