# Token Factories

You can easily create ERC721 and ERC1155 smart contracts using our Token Factories. Find addresses for token factories on [Addresses](../contract-addresses.md) page.

Token Factories create [Beacon proxies](https://docs.openzeppelin.com/contracts/3.x/api/proxy#BeaconProxy): this means Rarible Protocol can upgrade these contracts automatically \(when all token contracts are upgraded\).

Currently, two token factories are available: ERC-721 and ERC-1155. These both contracts are public in terms of minting: anyone can mint tokens there.

Invoke function `createToken` to create tokens with custom name, symbol. Set base uri to "ipfs:/" if you want to use ipfs for metadata storage.

There are the parameters supported:

* name - name of the smart contract
* symbol - symbol of the smart contract
* base URI - prefix for the URI for created tokens \(will be prepended to URI for every token minted\). By default, use "ipfs:/"
* contractURI - URI holding metadata for the contract. Set [https://api-mainnet.rarible.com/contractMetadata/{address}](https://api-mainnet.rarible.com/contractMetadata/{address}) if you want to control metadata using Rarible UI

