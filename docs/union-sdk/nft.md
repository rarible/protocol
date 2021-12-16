# Transfer, Mint, Burn

Transfer, minting and burning are the primary operations we can invoke on the blockchain. Below you can find a "how to use it" description.

## ERC721-NFT Lazy Minting

In order to lazy mint an item following parameters are required:

- URI - address of data on IPFS
- supply - number of NFTs to create (not in every case it is supported, you can check it by reading sdk.nft.mint response under multiple parameter)
- lazyMint - boolean, if we want to mint it lazily or normally
- creators - array of creators, which allows to distribute profits from sell in accordance to defined criteria
- royalties - array of royalties, which allows to take defined amount of any consecutive sell

Disclaimer:
Whenever you see the need of Union / Contract address you can create it as follows:

1. Blockchain Name
2. Hex Address

Example:
BlockchainName:HexAddress
ETHEREUM:0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05

```typescript
// Examplary values of URI and supply
const [uri, setUri] = useState<string>(
  "ipfs:/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp"
);
const [supply, setSupply] = useState<number>(1);

const currentWallet = wallet as EthereumWallet;
const makerAccount = await currentWallet.ethereum.getFrom();

// 1. Create PrepareMintRequest
// Collection ids are the address of Rarible Smart Contracts instance
// You can find them here:
// https://docs.rarible.org/ethereum/contract-addresses/

const mintRequest: PrepareMintRequest = {
  // Using Rarible API, tokenId would also be needed, but SDK takes care for that
  collectionId: toContractAddress(
    "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82"
  ),
};

// 2. Get Mint Response
// From mintResponse you can extract additional info e.g. is supply > 1 enabled
const mintResponse = await sdk.nft.mint(mintRequest);

// If you want to divide profits here you can add more than one creator object
// Combined value amount has to be 10000 which equals to 100 %, same with royalties
const creators = [
  {
    account: `ETHEREUM:${makerAccount}`,
    value: 10000,
  },
];

const royalties = [];

// 3. Submit Mint Response
const submitResponse = await mintResponse.submit({
  uri,
  supply,
  lazyMint: true,
  creators,
  royalties,
});

// Example of successful response
// itemId: "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382047"
//type: "off-chain"
```

## ERC721-NFT Lazy Mint & Sell

Often you want to list your nft on the sale right after creation. If it's the case for you, you can as well use mintAndSell function which allows you to do exactly that.

```typescript
// We can get user account in that way, or just extract it from accounts
// which we saved with Metamask
const currentWallet = wallet as EthereumWallet;
const makerAccount = await currentWallet.ethereum.getFrom();

// Price in ETH
const price: number = 1;

const mintRequest: PrepareMintRequest = {
  collectionId: toContractAddress(
    "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82"
  ),
};

const ethCurrency: EthErc20AssetType = {
  "@type": "ERC20",
  contract: toContractAddress(
    "ETHEREUM:0xc778417e063141139fce010982780140aa0cd5ab"
  ),
};

const mintResponse = await sdk.nft.mintAndSell(mintRequest);

const response = await mintResponse.submit({
  uri,
  supply: 1,
  lazyMint: true,
  price,
  creators: [
    {
      account: toUnionAddress(`ETHEREUM:${makerAccount}`),
      value: 10000,
    },
  ],
  currency: ethCurrency,
});

// Response:
// ItemId
// OrderId
```

## Transfer NFT Token

If we want to transfer NFT Token from one wallet address to another one it is super simple.
Of course if you want to submit a transfer transaction, you have to be the owner of an NFT.

You will need:

- tokenId
- transferRequest: PrepareTransferRequest

```typescript
const tokenId =
  "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382052";

const transferRequest: PrepareTransferRequest = {
  itemId: toItemId(tokenId),
};

const transferResponse = await sdk.nft.transfer(transferRequest);

const response = await transferResponse.submit({
  to: toUnionAddress("ETHEREUM:0x79Ea2d536b5b7144A3EabdC6A7E43130199291c0"),
});
```

## Burning tokens 🔥

Burning tokens is equivalent to sending them to address 0x0, because nobody has a private key for that.

Using SDK you can do that as follows:

```typescript
const tokenId =
  "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382052";

const burnRequest: PrepareBurnRequest = {
  itemId: toItemId(tokenId),
};

const burnResponse = await sdk.nft.burn(burnRequest);

const response = await burnResponse.submit();
```

And that's it

## Generate Token ID Request

That's not an obligatory step, because while using mint / mintAndSell function it's automatically done underneath, but e.g. while using API it can be used for something.

Because of lazy minting specification Rarible is generating token id to store it off chain until the token is actually minted.

```typescript
const genTokenIdReq: GenerateTokenIdRequest = {
  collection: toUnionAddress(
    "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82"
  ),
  minter: toUnionAddress("ETHEREUM:0x79Ea2d536b5b7144A3EabdC6A7E43130199291c0"),
};

const tokenIdResponse = await sdk.nft.generateTokenId(genTokenIdReq);
```

## Preprocessing Metadata

If you want to prepare metadata for your token, before sending them to IPFS, you can use preprocess function.

```typescript
const blockchain = Blockchain.ETHEREUM;
const metadata: CommonTokenMetadata = {
  name: "Hey",
  description: undefined,
  image: undefined,
  animationUrl: undefined,
  externalUrl: undefined,
  attributes: [],
};

const request: PreprocessMetaRequest = {
  blockchain,
  ...metadata,
};

const response = sdk.nft.preprocessMeta(request);
```
