# Ethereum SDK

The Rarible Protocol Ethereum SDK enables applications to easily interact with Rarible protocol.

## Installation

```text
npm install -D @rarible/protocol-ethereum-sdk
```

## With the Rarible Protocol Ethereum SDK, you can:

* Create sell orders 💰
* Create/accept bid for auctions
* Buy tokens for regular sell orders
* Create Lazy Mint NFT ERC721 and ERC1155 tokens
* Make regular mint
* Transfer tokens
* Burn tokens

## Usage

The examples below can show how you can implement supported functions in you app.

### Configure and create Rarible SDK object

```text
import { createRaribleSdk } from "@rarible/protocol-ethereum-sdk"

const sdk = createRaribleSdk(web3, env, { fetchApi: fetch })
```

* web3 - configured with your provider web3js client
* env - environment configuration name, it should accept one of these values 'ropsten' \| 'rinkeby' \| 'mainnet' \| 'e2e'

### Create sell order

```text
const order: Order = await sdk.order.sell(request).then(a => a.runAll())
// Sell request example:
const contractErc20Address: Address = '0x0' // your ERC20 contract address
const contractErc721Address: Address = '0x0' // your ERC721 contract address
const tokenId: BigNumber = '0x0' // the ERC721 Id of the token on which we want to place a bid
const sellerAddress: Address = '0x0' // Owner of ERC721 token
const nftAmount: number = 1 // For ERC721 always be 1
const sellPrice: number = 10 // price per unit of ERC721 or ERC1155 token(s)
const request = {
    makeAssetType: {
        assetClass: "ERC1155",
        contract: contractErc721Address,
        tokenId: tokenId,
    },
    maker: sellerAddress,
    amount: nftAmount,
    originFees: [],
    payouts: [],
    price: sellPrice,
    takeAssetType: {
        assetClass: "ERC20",
        contract: contractErc20Address
    },
}
```

Returns an object of created order.

[Sell e2e test](https://github.com/rarible/protocol-e2e-tests/blob/master/packages/tests-current/src/erc721-sale.test.ts)

### Create bid

```text
const order: Order = await sdk.order.bid(request).then(a => a.runAll())

// Bid request example:
const contractErc20Address: Address = '0x0' // your ERC20 contract address
const contractErc721Address: Address = '0x0' // your ERC721 contract address
const tokenId: BigNumber = '0x0' // the ERC721 Id of the token on which we want to place a bid
const sellerAddress: Address = '0x0' // Owner of ERC721 token
const buyerAddress: Address = '0x0' // Who make a bid
const nftAmount: number = 1 // For ERC721 always be 1
const bidPrice: number = 10 // price per unit of ERC721 or ERC1155 token(s)

const request = {
    makeAssetType: {
        assetClass: "ERC20",
        contract: contractErc20Address,
    },
    maker: buyerAddress,
    takeAssetType: {
        assetClass: "ERC721",
        contract: contractErc721Address,
        tokenId: tokenId,
    },
    taker: sellerAddress,
    amount: nftAmount,
    originFees: [],
    payouts: [],
    price: bidPrice,
}
```

Returns an object of created bid order.

Bid [e2e test](https://github.com/rarible/protocol-e2e-tests/blob/master/packages/tests-current/src/create-bid.test.ts)

### Purchase order or accept bid \(fill order\)

```text
const order: SimpleOrder

sdk.order.fill(
    order,
    { payouts: [], originFees: [], amount: 1, infinite: true }
).then(a => a.runAll())
```

For example, you can get the order object using our sdk api methods sdk.apis.order.getSellOrders\({}\) and pass it to fill function. You can get more information in the test repository sell e2e test

Mint NFT Tokens There are support two ways of minting ERC721 and ERC1155 tokens:

* Regular "on chain" minting using contract.
* Off chain minting \(the transaction itself and payment for gas occurs at the time of purchase or transfer\)

### Mint request object

```text
const mintRequest = {
    collection: {
        id: toAddress(contractAddress), // contract address
        type: "ERC1155", // type of asset to mint, "ERC721" || "ERC1155"
        supportsLazyMint: true, // true if contract supports lazy minting  
    },
    uri: 'uri', // token uri
    supply: toBigNumber('100'), // supply - used only for ERC1155 tokens
    creators: [{ account: toAddress(minter), value: 10000 }], // creators of token
    royalties: [], // royalties
    lazy: true, // true if mint lazy or false when mint onchain
}
```

Mint examples Mint function always return tokenId as string

### ERC721 Lazy

```text
const tokenId = await mint({
    collection: {
        id: toAddress(contractAddress),
        type: "ERC721",
        supportsLazyMint: true,
    },
    uri: 'uri',
    creators: [{ account: toAddress(minter), value: 10000 }],
    royalties: [],
    lazy: true,
})
```

### ERC1155 Lazy

```text
const tokenId = await mint({
    collection: {
        id: toAddress(contractAddress),
        type: "ERC1155",
        supportsLazyMint: true,
    },
    uri: 'uri',
    supply: toBigNumber('100'),
    creators: [{ account: toAddress(minter), value: 10000 }],
    royalties: [],
    lazy: true,
})
```

### ERC721

```text
await mint({
    collection: {
        id: toAddress(contractAddress),
        type: "ERC721",
        supportsLazyMint: true,
    },
    uri: 'uri',
    creators: [{ account: toAddress(minter), value: 10000 }],
    royalties: [],
})
```

### ERC1155

```text
const tokenId = await mint({
    collection: {
        id: toAddress(contractAddress),
        type: "ERC1155",
        supportsLazyMint: true,
    },
    uri: 'uri',
    supply: toBigNumber('100'),
    creators: [{ account: toAddress(minter), value: 10000 }],
    royalties: [],
})
```

Mint e2e test

### Transfer

```text
transfer(asset, to[, amount])

Transfer request params:

asset: {
    tokenId: BigNumber, // - id of token to transfer
    contract: Address, // - address of token contract
    assetClass?: "ERC721" | "ERC1155" // - not required, type of asset
}
to: Address, // - ethereum address of receiver of token
amount: BigNumber // - amount of asset to transfer, used only for ERC1155 assets
```

Example

```text
const hash = await sdk.nft.transfer(
    {
        assetClass: "ERC1155",
        contract: toAddress(contractAddress),
        tokenId: toBigNumber(tokenId),
    },
    receiverAddress,
    toAddress('10')
)
```

### Burn

```text
const hash = await sdk.nft.burn({
    contract: contractAddress,
    tokenId: toBigNumber(tokenId),
})
```
