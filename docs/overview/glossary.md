# Glossary

This document contains a glossary with an alphabetical list, definitions, and terms related to API.

[A](glossary.md#a)  |  [B](glossary.md#b)  |  [C](glossary.md#c)  |  [E](glossary.md#e)  |  [I](glossary.md#i)  |  [F](glossary.md#f)  |  [L](glossary.md#l)  |  [M](glossary.md#m)  |  [N](glossary.md#n)  |  [O](glossary.md#o)  |  [P](glossary.md#p)  |  [R](glossary.md#r)  |  [S](glossary.md#s)  |  [T](glossary.md#t)

## A

**API**

Application Programming Interface enables different systems to interact with each other programmatically.

**Activity**

Event history with orders or NFT tokens.

**Asset Type**

Type of asset on the blockchain (NFT, Fungible Token, Native token, etc.).

**Asset Class**

Class of blockchain Assets (Ethereum, ERC20, ERC721, FA2, etc.).

## B

**Bid**

Offer a certain amount in cryptocurrency for an NFT token, and compete with other people to buy it.

**Burn**

Burning NFT effectively destroys the token and removes it entirely from the blockchain.

## C

**Collection**

NFTs are grouped in collections. Usually, in Rarible Protocol, collections are smart contracts in which NFTs are minted.

**Continuation**

Continuation token from the previous response.

**Contract**

Address of the Smart Contract.

**Creator**

Address of the NFT item creator.

## E

**ERC-20**

[The standard](https://eips.ethereum.org/EIPS/eip-20) for fungible tokens. They have a property that makes each token the same (in type and value) as another token.

**ERC-721**

[The standard](https://eips.ethereum.org/EIPS/eip-721) for NFT. This token type is unique and can have a different value than another token from the same smart contract.

**ERC-1155**

[The multi-token standard](https://eips.ethereum.org/EIPS/eip-1155) for NFT. A single deployed contract may include any combination of fungible tokens, non-fungible tokens, or other configurations.

## I

**Item**

Address of the NFT item. Id of the Item has format `${contract}:${tokenId}`.

## F

**Fee**

Fee value for the operation. It can be Protocol fees, Origin fees, or Royalties.

## L

**Lazy Mint**

The way to defer the cost of minting an NFT until the moment it's sold to its first buyer. The gas fee for minting is included in the same transaction that assigns the NFT to the buyer.

## M

**Make**

Make side of the Order. Make - what maker (order creator) has.

**Maker**

Creator of the order.

**Mint, Minting**

Minting is the act of publishing a unique instance of the token on the blockchain.

## N

**NFT**

Non-Fungible Tokens are one-of-a-kind tokens that represent a unique good or asset, like digital art.

## O

**Origin Fee**

Extra fee that can be included in the order. This fee will be paid by exchange smart contract when order is matched. Usually, frontends can include custom origin fees to monetize.

**Owner**

Address of the NFT item owner.

**Ownership**

Entity which links owner and NFT (Item). It holds value - amount of NFTs owned by the user. Id of the Ownership has format `${contract}:${tokenId}:${owner}`.

## P

**Payouts**

Who will benefit when order is matched. If payouts are not specified, then order maker is the beneficiary. Otherwise, order maker can redirect payouts of assets to other user or users.

**Platform**

The platform where the order was created.

## R

**Royalties**

Fees that are usually paid to the creator on every sale.

## S

**Salt**

Salt is a string of data that is passed to the hash function along with the input array of data to calculate the hash.

**Smart Contract**

The programs stored on a blockchain that run when predetermined conditions are met.

**Supply**

Total number of tokens minted or to be minted.

## T

**Take**

Take side of the order, what order creator wants to get in return for `make` side.

**Token ID**

Token identifier.
