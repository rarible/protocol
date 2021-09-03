# CoCoNFT
**TLDR:**

CoCo NFT helps new creators get into the NFT space by building an onRamp that makes it easy to manage your wallet via social media logins. 

CoCoNFT uses the following Smart Contract functionalities:  lazy minting, exchange, and indexer.
CoCoNFT uses lazy minting so that the creators dont have to pay for minting making the process easy for newbies to crypto. They are planning on using the ability to support checkout right on our website via the Rarible Protocol Exchange and the indexer I believe to show a user's Lazy Minted NFTs.

**How CocoNFT would have changed things knowing what they know now:**

> On the Protocol we developed code to handle many features that we needed Rarible Protocol to do. Instead of waiting for the protocol updates.
As we were building found alot of frameworks we would have used something like [starter app](https://github.com/austintgriffith/scaffold-eth/tree/rarible-starter-app) to jumpstart our development process.

In regards to the database side CocoNFT advises to understand how you structure your database. 

**Step by step instructions for teams to do the same:**
*Always test on testnet before deploying to mainnet. Ropsten recommended for using Rarible APIs.*

1. Fork Rarible Protocol: https://github.com/rarible/protocol-contracts (Best to explore and get familiar)
2. Identify which NFT token type you will be using, 721 or 1155, and make any modifications necessary in the tokens folder: https://github.com/rarible/protocol-contracts/tree/master/tokens
3. Update the migrations files to pass in whatever parameters you want for the contract you plan to deploy: https://github.com/rarible/protocol-contracts/tree/master/tokens/migrations
      
**Note:** Only migration files 1-4 are necessary for initial deployment, and only #2 for 721 and #3 for 1155 if you don't want to deploy contracts for both.

4. Take note of the addresses for the contracts. These are upgradeable contracts, so you will be directing calls to the proxy address. 
5. Test some functions like `name()` or `symbol()` in your terminal to ensure it's working
6. Start using Rarible's APIs for lazy minting and order creation to build out your marketplace: https://api-reference.rarible.com/#operation/upsertOrder



API and/or SDK is in the works for CocoNFT.
