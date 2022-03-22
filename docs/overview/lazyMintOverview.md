---
title: Lazy Minting & Why should you use it.
description: Lazy minting process explained, alongside with benefits of Lazy Mint.
---

## Introduction

In order to be able to fully understand what lazy minting is, and the benefits of doing so, we have to scratch the other aspects of blockchain and NFTs first. This document will touch three main aspects which in my opinion are crucial in lazy minting process understanding:

1. Technical description of NFT,
2. Minting
3. Lazy Minting

### Technical description of NFT

If you're familiar with the concept of NFTs creation feel free to skip this section.
NFT in its essence is just a variable in a Smart Contract code. The most common approach is as follows:

1. Upload metadata (image, description, attributes, etc.) to IPFS, which is a decentralized JSON-like database (if you ever used a NoSQL database like MongoDB or Firebase, that's basically that, only decentralized). Based on all of the properties you've uploaded hash is calculated, by which you can now access your asset. Professionally it's called URI, which stands for Unique Resource Identifier. Moreover since storing image data on the blockchain would be expensive, instead of image data itself you just store image URL in your NFT. The image itself can be stored on IPFS. Just not in the JSON you use for NFT creation.
2. Invoke Smart Contract function responsible for minting, and assign URI created in the earlier step to your account address. That's it. Since code on the blockchain is immutable, and we have tokenId variable which tracks every unique NFT creation on a given smart contract, even if the same URI would be used twice, it will still be a different NFT.

### Minting

If you've read the first point, this one will be a repetition. Minting can be described as a process of a write operation (it's important because if you're writing on the blockchain, you're paying a gas fee), which has one goal. Associate address of a creator with a tokenId, which points to token metadata URI on IPFS. Pardon those who thought that it is more complicated. Of course, there are some language-specific restrictions and security steps that we have to take care of, but it's enough to use OpenZeppelin implementation of ERC721/ERC1155 to safely elevate core functionality, which in this case is NFT creation.

### Lazy Minting

The most important difference to point out between minting and lazy minting is writing to the blockchain action. As it was said before when writing on a blockchain occurs, the money from your wallet disappears i.e. you pay a gas fee. In normal minting, this process takes place immediately. In lazy minting, it can be postponed to the first transfer action (mostly it will be a buy action). How does that work underhood? There is some sort of API involved there. Basically, instead of immediately minting an NFT it stores its details on an API, so it is able to properly display all of the information, image, creator, etc. When the first buy occurs it is then minted straight to the buyer, but keeping all of the information about an author or royalties if there are some. The benefits of that are obvious - you as the creator don't pay a gas limit. You get the same functionality without any cost. You can then either lower the price of an NFT since the duty of gas payment lies on the buyer's side, or you can just get more money. The choice is yours.
