# Protocol Flow

1. [Creating ERC721/1155 Asset Metadata and Calling the Mint function](asset/creating-an-asset.md) In this step, we build asset metadata, upload this metadata to IPFS and finally create our NFT on-chain. It is also very important to read up about our [Royalties Schema](asset/royalties-schema.md).
2. [Asset Discovery](asset/asset-discovery.md) In our Asset Discovery section, you will learn how to query items and their metadata, using filters and paging, this includes items created outside of Rarible.
3. [Creating a sell order](exchange/creating-a-sell-order.md) In this section you will learn about approving assets through the transfer proxy, generating the order structure, calculating origin and protocol fees as well as signing your order and submitting it to the Rarible Indexer.
4. [Accepting a buyer/bid order](exchange/accepting-a-buy-order.md) In this section we will demonstrate the conversion of ETH to WETH \(For placing a bid\), approvals via the ERC20 Proxy Contract, generating the buy/bid order structure,  Calculating Protocol and Origin fees as well as Submitting your order to the Rarible Indexer.
5. [Order Discovery](exchange/order-discovery.md) Order Discovery explorers finding active orders \(Buy/Sell\) for items via an API query.
6. [Matching Order](smart-contracts/matching-orders.md) Matching Orders is a very important section as it deals with the Rarible Protocols Matching system, as well as custom matching contracts which can be created externally and utilized.  
7. [Updating/Canceling An Order](exchange/updating-cancelling-an-order.md) As the name suggests, this deals with the on-chain calls required to cancel an order \(Buy/Sell/Bid\) as well as how to update an order.
8. API Reference.
