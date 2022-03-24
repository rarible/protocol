---
title: Rarible Protocol Token types and Fees
description: Rarible Protocol is supported several types of NFT tokens and fees
---

# Tokens, Fees, and Royalties

## What is NFT

NFT means Non-Fungible Token. “Non-fungible” more or less means that it’s unique and can’t be replaced with something else. For example, a bitcoin is fungible — trade one for another bitcoin, and you’ll have exactly the same thing.

NFTs on the other hand are one-of-a-kind tokens that represent a unique good or asset which are non-fungible. If you traded it for a different NFT, you’d have something completely different.

NFTs can really be anything digital (such as drawings, music, videos, etc.), but a lot of the current excitement is around using the tech to sell digital art.

## Tokens

Rarible fully support several NFT standards:

* [ERC-721](https://eips.ethereum.org/EIPS/eip-721)
* [ERC-1155](https://eips.ethereum.org/EIPS/eip-1155)
* [Flow NFT standart](https://github.com/onflow/flow-nft/blob/master/contracts/NonFungibleToken.cdc)
* Tezos [FA2 (TZIP-012)](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-12/tzip-12.md)
* Rarible user-owned contracts (ERC-721 and ERC-1155) — users deploy these contracts, only owners can mint in these

User-owned contracts use beacon proxies, and these contracts can be updated by Rarible DAO. Rarible common contracts can be upgraded too.

You can query, issue, and trade these tokens with Rarible Protocol.

## Fees

`RaribleTransferManager` supports the following types of fees:

* Protocol fees — are charged on both sides of the transaction
* Origin fees — set for each order. It may differ for two orders
* Royalties — the author of the work will receive a part of each sale

## Royalties V2

Rarible defines an interface to query royalties from a contract. This is implemented on the standard [Rarible token contracts](https://github.com/rarible/protocol-contracts/blob/master/tokens/contracts/erc-721/ERC721Lazy.sol#L12).

It exposes `getRoyalties` method, which expects an ID as input (usually tokenId) and returns an array of accounts & basis points.

```javascript
function getRaribleV2Royalties(uint256 id) override external view returns (LibPart.Part[] memory) {
        return royalties[id];
}
```

## Royalties V1

The exchange contract interacts with the Rarible royalties implementation indirectly through a [Royalty Registry](https://github.com/rarible/protocol-contracts/blob/master/royalties-registry/contracts/RoyaltiesRegistry.sol#L63). The registry checks if the NFT contract supports the expected interface, and if so, queries for the Rarible royalties array.

This allows for Rarible to support different royalty standards for different collections.

Rarible Protocol Supports on-chain royalties. These are handled in the ExchangeV1 contract by the royalties array, which is needed to execute the mint function.

This tuple is made up of two variables, **fees.recipient** and **fees.value**.

* **fees.recipient** — refers to either the item owner (by default) or an address where the royalties will be received.
* **fees.value** — the royalties percentage. By default, this value is 1000 on Rarible, which is a 10% royalties fee. This is done using basis points. More information regarding basis point can be found [here](https://corporatefinanceinstitute.com/resources/knowledge/finance/basis-point-beep/).

Below, you can find the code block from ExchangeV1, which handles the on-chain royalties.

```javascript
contract HasSecondarySaleFees is ERC165 {
    event SecondarySaleFees(uint256 tokenId, address[] recipients, uint[] bps);
    /*
     * bytes4(keccak256('getFeeBps(uint256)')) == 0x0ebd4c7f
     * bytes4(keccak256('getFeeRecipients(uint256)')) == 0xb9c4d9fb
     *
     * => 0x0ebd4c7f ^ 0xb9c4d9fb == 0xb7799584
     */
    bytes4 private constant _INTERFACE_ID_FEES = 0xb7799584;
    constructor() public {
        _registerInterface(_INTERFACE_ID_FEES);
    }
    function getFeeRecipients(uint256 id) public view returns (address payable[] memory);
    function getFeeBps(uint256 id) public view returns (uint[] memory);
}
```