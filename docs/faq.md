---
title: FAQ
description: Frequently Asked Questions about working with the Rarible Protocol
---

# Frequently Asked Questions

See [Discussion QA section](https://github.com/rarible/protocol/discussions/categories/q-a) on our GitHub repo, [Discord](https://discord.gg/raribleprotocol), and [documentation](https://docs.rarible.org/) for more answers.

If you haven't found an answer to your question, you can create a new discussion [here](https://github.com/rarible/protocol/discussions/new). 

_WIP. It's the first FAQ version._

### Do I need tokenId to lazy minting NFT through SDK?

Token id is optional and generates inside the SDK if not provided. Just generate it using the API call and pass it to mint.

### How to connect Metamask with SDK?

Something like that:

```
new EthereumWallet(new Web3Ethereum({ web3: web31 }))
```

Now you can pass your wallet to the create SDK factory.

See [Rarible Protocol SDK](https://github.com/rarible/sdk#usage) for more information about using SDK.

### Why the price in the sell order can't be updated to a higher value?

That's a security issue. If you signed a message stating that you want to sell something for 1 ETH, you can't just ignore this and pretend that you want to sell for 1.5 ETH. If there is somewhere saved previous message, it can be used in the smart contract.

So, to make the price higher, you should cancel the order and sign a new message.

### What does the [union-service](https://github.com/rarible/union-service) repo do?

[Multichain service](https://docs.rarible.org/#architecture) also known as `union service` is a layer that connects different Blockchain APIs. It sits on top of all of them.

### What kind of fee model does the protocol use?

See [Smart contracts for Rarible protocol](https://github.com/rarible/protocol-contracts/blob/master/exchange-v2/contracts/RaribleTransferManager.md) repo on GitHub for more information about fees.

Also, you can find more information about fees in [Rarible Protocol Ethereum](https://docs.rarible.org/ethereum/smart-contracts/fees/) docs.

### What is "deploy" in the SDK used for?

It's used for deploying ERC-721/ERC-1155 token contracts. Users can deploy new collection contracts, for example.
