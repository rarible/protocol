---
title: MintGate use case with Rarible Protocol
description: MintGate integration Rarible Protocol by building their marketplace on it to provide the best experience for the community of creators and influencers
---

# MintGate

**TLDR:** 

MintGate decided to integrate Rarible protocol by building their marketplace on it to provide the best experience for their growing community of creators and influencers.

The usages of the Rarible Protocol within MintGate are:
Lazy Minting, Exchange, and Indexer
> We forked the 1155 contracts from Rarible to create a custom contract to mint from that has all the same functionality to abide by the royalties.
We are using that contract and the exchange contracts + indexer that Rarible provides through the APIs.
The steps for how we forked the contracts are listed below. From there we used the [starter app](https://github.com/austintgriffith/scaffold-eth/tree/rarible-starter-app) and [Eugene's sample project](https://github.com/rarible/protocol-example) as templates for creating signed sale orders to submit to the exchange. We use the indexer to pull created sale order data for purchases and information display, which are all included in the Rarible APIs.

**How MintGate would have changed things knowing what they know now:**

One thing Mintgate would have done differently based on experience is to prioritize the Rarible marketplace order creation features sooner instead of focusing on lazy minting alone. 

Mintgate hopes Rarible will be able to complete an SDK alternative to the API's because they fail from time to time, which can cause confusion for users and bugs when there is no sale order or lazy mint created. Using a SDK would hopefully prove more reliable.  

**Step by step instructions for how MintGate started building on Rarible protocol:**

*Always test on testnet before deploying to mainnet. Ropsten recommended for using Rarible APIs.*

1. Fork Rarible Protocol: https://github.com/rarible/protocol-contracts (Best to explore and get familiar)
2. Identify which NFT token type you will be using, 721 or 1155, and make any modifications necessary in the tokens folder: https://github.com/rarible/protocol-contracts/tree/master/tokens
3. Update the migrations files to pass in whatever parameters you want for the contract you plan to deploy: https://github.com/rarible/protocol-contracts/tree/master/tokens/migrations

    ???+ note

        Only migration files 1-4 are necessary for initial deployment, and only #2 for 721 and #3 for 1155 if you don't want to deploy contracts for both.

4. Take note of the addresses for the contracts. These are upgradeable contracts, so you will be directing calls to the proxy address. 
5. Test some functions like `name()` or `symbol()` in your terminal to ensure it's working
6. Start using Rarible's APIs for lazy minting and order creation to build out your marketplace: https://api-reference.rarible.com/#operation/upsertOrder

APIs for MintGate for token gating are available.
Full documentation and instructions can be found here:
[MintGate Docs](https://mintgate.gitbook.io/mintgate-docs/)
