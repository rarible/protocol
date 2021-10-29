# Exchange Overview

## Asset matching

The purpose of this is to validate that `makeAsset` of the **left** order matches `takeAsset` from the **right** order and vice versa. New types of assets can be added without a smart contract upgrade. This is done using a custom IAssetMatcher.

There are possible improvements to the protocol using these custom matcher contracts such as:

* Support for parametric assets. For example, the user can put an order to exchange 10ETH for any NFT from a popular collection.
* Support for NFT bundles.

The general process for completing an order with the Rarible Exchange is as follows:

1. Seller approves the Rarible exchange contract to transfer NFT on their behalf
2. Seller creates and signs an order. They specify the types and amounts of assets they would like in return.
3. Seller submits the order to the indexer
4. Potential buyers query the indexer to get sell orders for a specific item or collection
5. Buyers can create a matching buy order for a sell order from the indexer. The buyer can then submit a matching buy order to the smart contract and execute the transfer \(no sig required\).
6. Or the buyer can create a new bid and submit it to the indexer \(requires signature\)
7. If the buyer submits a bid, the seller can choose to accept it by creating the matching sell order and submitting it to the contract, or they can send a signed order back to the buyer which the buyer would submit to the contract.

## Order Structure

Each order \(both buy & sell\) consist of a `makeAsset` and a `takeAsset`

**Make Asset** is what you are sending.

* In a buy order this is what you are _paying_ for the seller's NFT. This can be ETH, ERC20, ERC721, ERC1155, or any custom asset using their Asset Matcher interface
* In a sell order this is the NFT you are selling

**Take Asset** is what you are accepting in return

* In a buy order this is the NFT you are buying
* In a sell order this is what you are willing to accept. 

### Order

| Field | Description | Required |
| :--- | :--- | :--- |
| **Maker** | Address of entity giving up `makeAsset` | Yes |
| **makeAsset** | Asset the entity is giving up | Yes |
| **taker** | Address of counterparty | no, if 0 then anyone can fill the order |
| **takeAsset** | Asset the entity is receving | Yes |
| **salt** | nonce for signatures submitted with the order | Generally signatures are only needed if msg.sender != maker |
| **start** | uint - order can't be filled before this time | no |
| **end** | uint - order can't be filled after this time | no |
| **dataType** | bytes4, usually hash of a string like v1 or v2 | Yes |
| **data** | generic `bytes`. Can be used for protocol extensions | no |

### Asset

| Field | Description | Required |
| :--- | :--- | :--- |
| assetType | Specifies ETH, specific ERC20, ERC721, ERC1155 | Yes |
| value | uint | Yes |

### AssetType

| Field | Description | Required |
| :--- | :--- | :--- |
| assetClass | bytes4 specifies ETH, ERC20, ERC721 | Yes |
| data | bytes - generic data depending on tp. Ex. address for ERC20, token + tokenID for ERC721 | yes |

### Asset Types

Asset Class data field is calculated as follows

```text
    bytes4 constant public ETH_ASSET_CLASS = bytes4(keccak256("ETH"));
    bytes4 constant public ERC20_ASSET_CLASS = bytes4(keccak256("ERC20"));
    bytes4 constant public ERC721_ASSET_CLASS = bytes4(keccak256("ERC721"));
    bytes4 constant public ERC1155_ASSET_CLASS = bytes4(keccak256("ERC1155"));
```

All asset types get encoded using these helper functions [https://github.com/rariblecom/protocol-contracts/blob/master/exchange-v2/test/assets.js](https://github.com/rariblecom/protocol-contracts/blob/master/exchange-v2/test/assets.js)

#### ERC721

`assetClass`: Truncated hash of string "ERC721" `data`: ABI encoded parameters of `address` and `tokenId` `value`: 1

ERC721 Input \(Pre encoding\)

```text
  {
    assetType: {
      assetClass: "ERC721",
      token: "0x25646b08d9796ceda5fb8ce0105a51820740c049",
      tokenId: "0xc66d094ed928f7840a6b0d373c1cd825c97e3c7c00000000000000000000000a"
    },
    value: "1",
  }
```

#### ERC1155

`assetClass`: Truncated hash of string "ERC1155" `data`: ABI encoded parameters of `address` and `tokenId` `value`: 1-&gt;totalSupply

ERC1155 Input \(Pre encoding\)

```text
  {
    assetType: {
      assetClass: "ERC1155",
      token: "0x25646b08d9796ceda5fb8ce0105a51820740c049",
      tokenId: "0xc66d094ed928f7840a6b0d373c1cd825c97e3c7c00000000000000000000000a"
    },
    value: "100",
  }
```

#### ERC20

`assetClass`: Truncated hash of string "ERC20" `data`: ABI encoded parameters of `address` `value`: 1-&gt;totalSupply

ERC20 Input \(Pre encoding\)

```text
  {
    assetType: {
      assetClass: "ERC20",
      token: "0x25646b08d9796ceda5fb8ce0105a51820740c049",
    },
    value: "10000000000000000",
  }
```

#### ETH

`assetClass`: Truncated hash of string "ETH" `data`: 0x `value`: 1-&gt;1e18

Input \(pre encoding\)

```text
  {
    assetType: {
      assetClass: "ETH"
    },
    value: "10000000000000000",
  },
```

#### Custom Asset Matcher

Any asset can be added

`assetClass`: Truncated hash of any string `data`: Whatever is relevant `value`: some uint

## Order validation

* Check the start/end date of the orders.
* Check if the taker of the order is blank or taker = `order.taker`
* Check if the order is signed by its maker or maker of the order is executing the transaction.
* If the maker of the order is a contract, then an ERC-1271 check is performed.

{% hint style="info" %}
Currently, only off-chain orders are supported, this part of the smart contract can be easily updated to support on-chain order books.
{% endhint %}

## Order execution

Order execution is done by TransferManager. There are 2 variants:

* SimpleTransferManager \(it simply transfers assets from maker to taker and vice versa\).
* RaribleTransferManager \(sophisticated version, it takes into account protocol commissions, royalties, etc\).

{% hint style="success" %}
There are plans to extend RaribleTransferManager to support more royalty schemes and add new features like custom fees, multiple order beneficiaries.
{% endhint %}

This part of the algorithm can be extended with a custom ITransferExecutor. In the future, new executors will be added to support new asset types, for example, executor for handling bundles can be added.

{% hint style="info" %}
Possible improvements:

* Support bundles.
* Support random boxes.
{% endhint %}

## Fees

RaribleTransferManager supports these types of fees:

* Protocol fees \(These fees are taken from both sides of the deal\).
* Origin fees \(Origin and origin fee is set for every order. it can be different for two orders involved\).
* Royalties \(Authors of the work will receive part of each sale\).

**Fees calculation, fee side**

To take a fee we need to calculate, what side of the deal can be used as money. There is a simple algorithm to do it:

* If ETH is from any side of the deal, it's used.
* If not, then if ERC-20 is in the deal, it's used.
* If not, then if ERC-1155 is in the deal, it's used.
* Otherwise, the fee is not taken \(for example, two ERC-721 are involved in the deal\).

When we established, what part of the deal can be treated as money, then we can establish, that

* The Buyer is the side of the deal who owns the money.
* The Seller is the other side of the deal.

Then the total amount of the asset \(money side\) should be calculated

* Protocol fee is added on top of the filled amount.
* The origin fee of the buyer's order is added on top too.

If the buyer is using an ERC-20 token for payment, then he must approve at least this calculated amount of tokens.

If the buyer is using ETH, then he must send this calculated amount of ETH with the transaction.

