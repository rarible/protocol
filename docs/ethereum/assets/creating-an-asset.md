---
description: >-
  This Documentation will give you a very brief overview of creating an item
  using Rarible Protocol.
---

# Asset Creation

## Asset Introduction

Rarible protocol has two asset types, ERC721, and ERC1155, the main difference between them is that ERC721 creates unique 1 of 1 item, whereas ERC1155, allows the user to create an item with multiple editions (The maximum amount of editions is 2\*\*256 - 1).

You can find the protocol smart contracts [here.](https://github.com/rariblecom/protocol-contracts)

#### Ropsten

#### Asset Contract ERC721 [Etherscan link ↗](https://ropsten.etherscan.io/address/0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05)

```
0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05
```

#### Asset Contract ERC1155 [Etherscan link ↗](https://ropsten.etherscan.io/address/0x6a94aC200342AC823F909F142a65232E2f052183)

```
0x6a94aC200342AC823F909F142a65232E2f052183
```

#### Rinkeby

#### Asset Contract ERC721 [Etherscan link ↗](https://rinkeby.etherscan.io/address/0x6ede7f3c26975aad32a475e1021d8f6f39c89d82)

```
0x6ede7f3c26975aad32a475e1021d8f6f39c89d82
```

#### Asset Contract ERC1155 [Etherscan link ↗](https://rinkeby.etherscan.io/address/0x1AF7A7555263F275433c6Bb0b8FdCD231F89B1D7)

```
0x1AF7A7555263F275433c6Bb0b8FdCD231F89B1D7
```

## Asset Types Explained

### ERC721 & ERC1155

With the new ERC721 & ERC1155 Asset contracts we no longer call the mint function directly, instead, we implement lazy minting via the mintAndTransfer function. Lazy minting allows the item to be created and store off-chain until someone purchases/transfers this item, only at this point does the item get created on-chain.

Direct calls to `mint()` should be avoided and replaced with `mintAndTransfer()`. However, standard minting is still possible with this function. See **ERC721 Standard Minting** or **ERC1155 Standard Minting** for details.

_**Parameters**_

* **tokenId**

The `tokenId` must be supplied as a uint256, which is a unique identifying number for the token.

The `tokenId` is made up of two sections, the first 20 bytes is the user's address and the next 12 bytes can be any random number. [This API](https://api-reference.rarible.com/#operation/generateTokenId) will allow you to get the next available ID.

* **uri**

This is the suffix for the tokenURI. The prefix for Rarible protocol contracts is `ipfs://`

Sample IPFS uri:

`/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp`

Gets concatenated into the following upon minting:

`ipfs://ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp`

{% hint style="info" %}
If you are not storing your metadata on IPFS, you will need to create your own custom collection contract instead of using the protocol's asset contracts. See **Implementation** for details.
{% endhint %}

* **creators**

`creators` is an array of addresses and values. The `LibPart.Part` struct it derives from is provided below.

```
struct Part {
    address payable account;
    uint96 value;
}
```

This array should contain all the addresses of the creators of this token with their respective ownership or contribution to the creation - in basis points. The address array is public and can be queried by anyone.

Sum of the fields value in this array should be 10000 (100% in basis points). Can be divided in any number of ways.

I.e. The following array, `[[0x12345..., 5000], [0x6789..., 5000]]`, associates the creation of the given NFT to 2 creators at an equal 50% distribution.

* **royalties**

`royalties` is an array of addresses and values. Like `creators`, it's also derived from the `LibPart.Part` struct provided below.

```
struct Part {
    address payable account;
    uint96 value;
}
```

The fees array is public and can be queried by anyone. Values are specified in basis points. For example, 2000 means 20%.

I.e. One address recieves 20% royalties with the following array, `[[0x12345..., 2000]]`. But more than one address can be provided to recieve royalties at specified percentages.

* **signatures**

`signatures` is an array of wallet signatures for this transaction from every creator.

However, an empty signature, `[[0x]]`, can be passed if the creator is minting immediately instead of creating a Lazy Mint. The steps for standard minting are provided in **ERC721 Standard Minting**.

**ERC721 mintAndTransfer ABI**

```
    // ABI for ERC-721 mintAndTransfer
    {
      "inputs": [
        {
          "components": [
            {
              "internalType": "uint256",
              "name": "tokenId",
              "type": "uint256"
            },
            {
              "internalType": "string",
              "name": "uri",
              "type": "string"
            },
            {
              "components": [
                {
                  "internalType": "address payable",
                  "name": "account",
                  "type": "address"
                },
                {
                  "internalType": "uint256",
                  "name": "value",
                  "type": "uint256"
                }
              ],
              "internalType": "struct LibPart.Part[]",
              "name": "creators",
              "type": "tuple[]"
            },
            {
              "components": [
                {
                  "internalType": "address payable",
                  "name": "account",
                  "type": "address"
                },
                {
                  "internalType": "uint256",
                  "name": "value",
                  "type": "uint256"
                }
              ],
              "internalType": "struct LibPart.Part[]",
              "name": "royalties",
              "type": "tuple[]"
            },
            {
              "internalType": "bytes[]",
              "name": "signatures",
              "type": "bytes[]"
            }
          ],
          "internalType": "struct LibERC721LazyMint.Mint721Data",
          "name": "data",
          "type": "tuple"
        },
        {
          "internalType": "address",
          "name": "to",
          "type": "address"
        }
      ],
      "name": "mintAndTransfer",
      "outputs": [],
      "stateMutability": "nonpayable",
      "type": "function"
    }
```

### ERC721 Lazy Minting

If you're storing your metadata on IPFS, you can mint through the Rarible Protocol asset contracts without conflict.

Lazy minting requires the creator's signature in order to allow minting of their NFT when someone else purchases it and to retain its provenance.

We'll go through the steps of getting the creator's signature and creating a lazy mint below. You can also find various code implementations for lazy minting [here](https://github.com/ipatka/scaffold-eth/tree/rarible-starter-app), [here](https://github.com/MysteryDrop/mystery-drop/tree/master/packages/react-app/src/util), and [here](https://github.com/evgenynacu/sign-typed-data).

#### For 721 (Ropsten)

**Step 1**: Generate a token ID.

GET from `https://ethereum-api-dev.rarible.com/protocol/v0.1/ethereum/nft/collections/{ContractAddress}/generate_token_id?minter=${account}`

Since a lazy mint is stored off-chain, it's necessary to generate a token ID through this API to ensure you get the next available token ID since there's no certainty about when the NFT will actually be minted.

GET from `https://ethereum-api-dev.rarible.org/v0.1/nft/collections/{collection}/generate_token_id?minter=${account}`

```

const res = await fetch('https://ethereum-api-dev.rarible.org/v0.1/nft/collections/{collection}/generate_token_id?minter=${account}').then((res) => res.json());
```

Response

```
{
    tokenId: "10269532675691974816893214588076010230265315839066808147818573374451427049545", 
    signature: {
        r: "0x9f73810b77cee6ce00f3924091b22030ba707823bde53635d5ef2a3a1a605e8e"
        s: "0x00803ec40e179172973347ba9f1a8c8dd094e5b2e2e19504a09017f4358f2b1e"
        v: 28
    }
}
```

Get the `tokenId` from the response object.

**Step 2**: Create the Lazy Mint Request Body to be signed by the creator.

```
{
    "@type": "ERC721",
    "contract": "0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05",
    "tokenId": tokenId,
    "uri": "/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp",
    "creators": [
        { 
            account: "0x1234...", 
            value: "10000" 
        }
    ],
    "royalties": [
        { 
            account: "0x1234...", 
            value: 2000 
        }
    ],
  };
```

**Step 3**: Creator signs the provided typed data, thereby granting permission to mint their NFT upon purchase.

{% hint style="info" %}
See [EIP1271](../exchange/contract-wallets.md) for information on how smart contracts can interact with this order book.
{% endhint %}

**First**, construct the typed data structure:

```
"types": {
    "EIP712Domain" [
      {
        type: "string",
        name: "name",
      },
      {
        type: "string",
        name: "version",
      },
      {
        type: "uint256",
        name: "chainId",
      },
      {
        type: "address",
        name: "verifyingContract",
      }
    ],
    "Mint721": [
        {"name": "@type", "type": "string"},
        {"name": "contract", "type": "address"},
        {"name": "tokenId", "type": "uint256"},
        {"name": "tokenURI", "type": "string"},
        {"name": "uri", "type": "string"},
        {"name": "creators", "type": "Part[]"},
        {"name": "royalties", "type": "Part[]"}
    ],
    "Part": [
        { name: "account", type: "address" },
        { name: "value", type: "uint96" }
    ]
},
"domain": {
    name: "Mint721",
    version: "1",
    chainId: 3,
    verifyingContract: "0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05"
},
"primaryType": "Mint721",
"message": {
    "@type": "ERC721",
    "contract": "0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05",
    "tokenId": tokenId,
    "tokenURI": "/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp"
    "uri": "/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp",
    "creators": [
        { 
            account: "0x1234...", 
            value: "10000" 
        }
    ],
    "royalties": [
        { 
            account: "0x1234...", 
            value: 2000 
        }
    ],
 };
```

**Then** provide the data structure above to the creator for signing.

```
// Sample code

async function signTypedData(web3Provider, from, dataStructure) {
  const msgData = JSON.stringify(dataStructure);
  const signature = await web3Provider.send("eth_signTypedData_v4", [from, msgData]);
  const sig0 = sig.substring(2);
  const r = "0x" + sig0.substring(0, 64);
  const s = "0x" + sig0.substring(64, 128);
  const v = parseInt(sig0.substring(128, 130), 16);
  return {
    dataStructure,
    signature,
    v,
    r,
    s,
  };
}
```

**Finally**, get the `signature` from the object that the function above returns and add it as the final field of the Lazy Mint Request Body you created in Step 2.

E.g.

```
{
    "@type": "ERC721",
    "contract": "0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05",
    "tokenId": tokenId,
    "uri": "/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp",
    "creators": [
        { 
            account: "0x1234...", 
            value: "10000" 
        }
    ],
    "royalties": [
        { 
            account: "0x1234...", 
            value: 2000 
        }
    ],
    "signatures": ["0x2f1e8dd2838930f0230a9fcbb2977779838eb8dd44391af1…a6cb767fa157d5fb54c084e8ffb41be1c1bc5b6f067fd681b"]
  };
```

**Step 4**: Create your Lazy Minted NFT.

POST to `https://ethereum-api-dev.rarible.org/v0.1/nft/mints`

```
{
    "@type": "ERC721",
    "contract": "0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05",
    "tokenId": tokenId,
    "uri": "/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp",
    "creators": [
        { 
            account: "0x1234...", 
            value: "10000" 
        }
    ],
    "royalties": [
        { 
            account: "0x1234...", 
            value: 2000 
        }
    ],
    "signatures": ["0x2f1e8dd2838930f0230a9fcbb2977779838eb8dd44391af1…a6cb767fa157d5fb54c084e8ffb41be1c1bc5b6f067fd681b"]
  };
```

Response

```
{
  "id": ""0x3437df037bbbeb1aa3e417b32154bc2bb5da1c04:10269532675691974816893214588076010230265315839066808147818573374451427049549"",
  "contract": "0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05",
  "tokenId": tokenId,
  "creators": [
    {
      "account": "0x1234...",
      "value": 10000
    }
  ]
  "supply": 1,
  "lazySupply": 1,
  "owners": [
     "0x1234..."
  ],
  "royalties": [
    {
      "account": "0x1234...",
      "value": 2000
    }
  ],
  "pending": [
    {
      "date": "2019-08-24T14:15:22Z",
      "owner": "0x1234...",
      "from": "0x1234...",
      "contract": "0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05",
      "tokenId": tokenId,
      "value": 0,
      "type": "TRANSFER"
    }
  ]
}
```

You've successfully created a Lazy Minted NFT with the Rarible Protocol! 🎉 \


### ERC721 Standard Minting

You can mint NFTs through the Rarible asset contracts using `mintAndTransfer` like you would for a standard `mint` call. You just need to provide all the expected parameters seen below.

`mintAndTransfer(LibERC721LazyMint.Mint721Data memory data, address to)`

```
struct Mint721Data {
 uint tokenId;
 string uri;
 LibPart.Part[] creators;
 LibPart.Part[] royalties;
 bytes[] signatures;
}
```

You can do so by instantiating the contract in your app and calling the function directly using `ethers.js` or `web3.js`.

{% hint style="info" %}
For the signature, since you are minting an NFT as a direct call and not a lazy mint, you simply pass an empty signature. E.g. `0x`.

Royalties are set as basis point, so 1000 = 10%. [More info](https://corporatefinanceinstitute.com/resources/knowledge/finance/basis-point-beep/)
{% endhint %}

#### Example

```javascript
async function mintNow() {
    // Get a token id
    const tokenId = await fetch(`https://ethereum-api-dev.rarible.org/v0.1/nft/collections/{collection}/generate_token_id?minter=${account}`);

    // Instantiate the contract
    const provider = new ethers.providers.Web3Provider(userWalletProvider);
    const signer = provider.getSigner();
    const contract = new ethers.Contract(contractAddress, abi, signer);

    // Call the function
    const tx = await contract.mintAndTransfer(
        [
          tokenId.tokenId,
          uri,
          [[creator, 5000], [creator2, 5000]], // You can assign one or add multiple creators, but the value must total 10000
          [[creator, 1000], [creator2, 1000]], // Royalties are set as basis point, so 1000 = 10%. 
          ["0x"]
        ],
        minter,
      );

      const receipt = await tx.wait();
      console.log('Minting Success', receipt);
}
```

### ERC1155 Overview

`mintAndTransfer(LibERC1155LazyMint.Mint1155Data memory data, address to, uint256 _amount)`

**Mint1155Data Parameter Structure**

```
struct Mint1155Data {
 uint tokenId;
 string uri;
 uint supply;
 LibPart.Part[] creators;
 LibPart.Part[] royalties;
 bytes[] signatures;
}
```

_**Parameters**_

* **tokenId**

The `tokenId` must be supplied as a uint256, which is a unique identifying number for the token.

The `tokenId` is made up of two sections, the first 20 bytes is the user's address and the next 12 bytes can be any random number. [This API](https://api-reference.rarible.com/#operation/generateTokenId) will allow you to get the next available ID.

* **uri**

This is the suffix for the tokenURI. The prefix for Rarible protocol contracts is `ipfs://`

Sample IPFS uri:

`/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp`

Gets concatenated into the following upon minting:

`ipfs://ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp`

{% hint style="info" %}
If you are not storing your metadata on IPFS, you will need to create your own custom collection contract instead of using the protocol's asset contracts. See **Implementation** for details.
{% endhint %}

* **supply**

`supply` should be a uint256, this is the number of copies (or Editions) of this token that will ever exist. (Maximum value is 2\*\*256 - 1).

* **creators**

`creators` is an array of addresses and values. The `LibPart.Part` struct it derives from is provided below.

```
struct Part {
    address payable account;
    uint96 value;
}
```

This array should contain all the addresses of the creators of this token with their respective ownership or contribution to the creation - in basis points. The address array is public and can be queried by anyone.

Sum of the fields value in this array should be 10000 (100% in basis points). Can be divided in any number of ways.

I.e. The following array, `[[0x12345..., 5000], [0x6789..., 5000]]`, associates the creation of the given NFT to 2 creators at an equal 50% distribution.

* **royalties**

`royalties` is an array of addresses and values. Like `creators`, it's also derived from the `LibPart.Part` struct provided below.

```
struct Part {
    address payable account;
    uint96 value;
}
```

The fees array is public and can be queried by anyone. Values are specified in basis points. For example, 2000 means 20%.

I.e. One address recieves 20% royalties with the following array, `[[0x12345..., 2000]]`. But more than one address can be provided to recieve royalties at specified percentages.

* **signatures**

`signatures` is an array of wallet signatures for this transaction from every creator.

However, an empty signature, `[[0x]]`, can be passed if the creator is minting immediately instead of creating a Lazy Mint. The steps for standard minting are provided in **ERC1155 Standard Minting**.

**ERC1155 mintAndTransfer ABI**

```
    // ABI for ERC-1155 mintAndTransfer
    {
      "inputs": [
        {
          "components": [
            {
              "internalType": "uint256",
              "name": "tokenId",
              "type": "uint256"
            },
            {
              "internalType": "string",
              "name": "uri",
              "type": "string"
            },
            {
              "internalType": "uint256",
              "name": "supply",
              "type": "uint256"
            },
            {
              "components": [
                {
                  "internalType": "address payable",
                  "name": "account",
                  "type": "address"
                },
                {
                  "internalType": "uint256",
                  "name": "value",
                  "type": "uint256"
                }
              ],
              "internalType": "struct LibPart.Part[]",
              "name": "creators",
              "type": "tuple[]"
            },
            {
              "components": [
                {
                  "internalType": "address payable",
                  "name": "account",
                  "type": "address"
                },
                {
                  "internalType": "uint256",
                  "name": "value",
                  "type": "uint256"
                }
              ],
              "internalType": "struct LibPart.Part[]",
              "name": "royalties",
              "type": "tuple[]"
            },
            {
              "internalType": "bytes[]",
              "name": "signatures",
              "type": "bytes[]"
            }
          ],
          "internalType": "struct LibERC1155LazyMint.Mint1155Data",
          "name": "data",
          "type": "tuple"
        },
        {
          "internalType": "address",
          "name": "to",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "_amount",
          "type": "uint256"
        }
      ],
      "name": "mintAndTransfer",
      "outputs": [],
      "stateMutability": "nonpayable",
      "type": "function"
    }
```

### ERC1155 Lazy Minting

If you're storing your metadata on IPFS, you can mint through the Rarible Protocol asset contracts without conflict.

Lazy minting requires the creator's signature in order to allow minting of their NFT when someone else purchases it and to retain its provenance.

We'll go through the steps of getting the creator's signature and creating a lazy mint below. You can also find various code implementations for lazy minting [here](https://github.com/ipatka/scaffold-eth/tree/rarible-starter-app), [here](https://github.com/MysteryDrop/mystery-drop/tree/master/packages/react-app/src/util), and [here](https://github.com/evgenynacu/sign-typed-data).

#### For 1155 (Ropsten)

**Step 1**: Generate a token ID.

Since a lazy mint is stored off-chain, it's necessary to generate a token ID through this API to ensure you get the next available token ID since there's no certainty about when the NFT will actually be minted.

GET from `https://ethereum-api-dev.rarible.org/v0.1/nft/collections/{collection}/generate_token_id?minter=${account}`

```
// Sample Call 

const res = await fetch('https://ethereum-api-dev.rarible.org/v0.1/nft/collections/{collection}/generate_token_id?minter=${account}').then((res) => res.json());
```

Response

```
{
    tokenId: "10269532675691974816893214588076010230265315839066808147818573374451427049545", 
    signature: {
        r: "0x9f73810b77cee6ce00f3924091b22030ba707823bde53635d5ef2a3a1a605e8e"
        s: "0x00803ec40e179172973347ba9f1a8c8dd094e5b2e2e19504a09017f4358f2b1e"
        v: 28
    }
}
```

Get the `tokenId` from the response object.

**Step 2**: Create the Lazy Mint Request Body to be signed by the creator**.**

```
{
    "@type": "ERC1155",
    "contract": "0x6a94aC200342AC823F909F142a65232E2f052183 ",
    "tokenId": tokenId,
    "uri": "/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp",
    "supply": 10,
    "creators": [
        { 
            account: "0x1234...", 
            value: "10000" 
        }
    ],
    "royalties": [
        { 
            account: "0x1234...", 
            value: 2000 
        }
    ],
  };
```

**Step 3**: Creator signs the provided typed data, thereby granting permission to mint their NFT upon purchase.

{% hint style="info" %}
See [Signatures](https://hackmd.io/ktJuljjGTA2TivezBXKA5g?view#Signatures) for more details on typed data and EIP-712 and EIP-1271.
{% endhint %}

**First**, construct the typed data structure:

```
"types": {
    "EIP712Domain" [
      {
        type: "string",
        name: "name",
      },
      {
        type: "string",
        name: "version",
      },
      {
        type: "uint256",
        name: "chainId",
      },
      {
        type: "address",
        name: "verifyingContract",
      }
    ],
    "Mint1155": [
        {"name": "@type", "type": "string"},
        {"name": "contract", "type": "address"},
        {"name": "tokenId", "type": "uint256"},
        {"name": "tokenURI", "type": "string"},
        {"name": "uri", "type": "string"},
        { name: 'supply', type: 'uint256' },
        {"name": "creators", "type": "Part[]"},
        {"name": "royalties", "type": "Part[]"}
    ],
    "Part": [
        { name: "account", type: "address" },
        { name: "value", type: "uint96" }
    ]
},
"domain": {
    name: "Mint1155",
    version: "1",
    chainId: 3,
    verifyingContract: "0x6a94aC200342AC823F909F142a65232E2f052183 "
},
"primaryType": "Mint1155",
"message": {
    "@type": "ERC1155",
    "contract": "0x6a94aC200342AC823F909F142a65232E2f052183 ",
    "tokenId": tokenId,
    "tokenURI": "/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp"
    "uri": "/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp",
    "supply": 10,
    "creators": [
        { 
            account: "0x1234...", 
            value: "10000" 
        }
    ],
    "royalties": [
        { 
            account: "0x1234...", 
            value: 2000 
        }
    ],
 };
```

**Then** provide the data structure above to the creator for signing.

```
// Sample code

async function signTypedData(web3Provider, from, dataStructure) {
  const msgData = JSON.stringify(dataStructure);
  const signature = await web3Provider.send("eth_signTypedData_v4", [from, msgData]);
  const sig0 = sig.substring(2);
  const r = "0x" + sig0.substring(0, 64);
  const s = "0x" + sig0.substring(64, 128);
  const v = parseInt(sig0.substring(128, 130), 16);
  return {
    dataStructure,
    signature,
    v,
    r,
    s,
  };
}
```

**Finally**, get the `signature` from the object that the function above returns and add it as the final field of the Lazy Mint Request Body you created in Step 2.

E.g.

```
{
    "@type": "ERC1155",
    "contract": "0x6a94aC200342AC823F909F142a65232E2f052183 ",
    "tokenId": tokenId,
    "uri": "/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp",
    "supply": 10,
    "creators": [
        { 
            account: "0x1234...", 
            value: "10000" 
        }
    ],
    "royalties": [
        { 
            account: "0x1234...", 
            value: 2000 
        }
    ],
    "signatures": ["0x2f1e8dd2838930f0230a9fcbb2977779838eb8dd44391af1…a6cb767fa157d5fb54c084e8ffb41be1c1bc5b6f067fd681b"]
  };
```

**Step 4**: Create your Lazy Minted NFT.

POST to `https://ethereum-api-dev.rarible.org/v0.1/nft/mints`

```
{
    "@type": "ERC721",
    "contract": "0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05",
    "tokenId": tokenId,
    "uri": "/ipfs/QmWLsBu6nS4ovaHbGAXprD1qEssJu4r5taQfB74sCG51tp",
    "supply": 10
    "creators": [
        { 
            account: "0x1234...", 
            value: "10000" 
        }
    ],
    "royalties": [
        { 
            account: "0x1234...", 
            value: 2000 
        }
    ],
    "signatures": ["0x2f1e8dd2838930f0230a9fcbb2977779838eb8dd44391af1…a6cb767fa157d5fb54c084e8ffb41be1c1bc5b6f067fd681b"]
  };
```

Response

```
{
  "id": ""0x3437df037bbbeb1aa3e417b32154bc2bb5da1c04:10269532675691974816893214588076010230265315839066808147818573374451427049549"",
  "contract": "0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05",
  "tokenId": tokenId,
  "creators": [
    {
      "account": "0x1234...",
      "value": 10000
    }
  ]
  "supply": 1,
  "lazySupply": 1,
  "owners": [
     "0x1234..."
  ],
  "royalties": [
    {
      "account": "0x1234...",
      "value": 2000
    }
  ],
  "pending": [
    {
      "date": "2019-08-24T14:15:22Z",
      "owner": "0x1234...",
      "from": "0x1234...",
      "contract": "0xB0EA149212Eb707a1E5FC1D2d3fD318a8d94cf05",
      "tokenId": tokenId,
      "value": 0,
      "type": "TRANSFER"
    }
  ]
}
```

You've successfully created a Lazy Minted NFT with the Rarible Protocol! 🎉 \


### ERC1155 Standard Minting

You can mint NFTs through the Rarible asset contracts using `mintAndTransfer` like you would for a standard `mint` call. You just need to provide all the expected parameters seen below.

`mintAndTransfer(LibERC1155LazyMint.Mint1155Data memory data, address to, uint256 _amount)`

```
struct Mint1155Data {
 uint tokenId;
 string uri;
 uint supply;
 LibPart.Part[] creators;
 LibPart.Part[] royalties;
 bytes[] signatures;
}
```

You can do so by instantiating the contract in your app and calling the function directly using `ethers.js` or `web3.js`.

{% hint style="info" %}
For the signature, since you are minting an NFT as a direct call and not a lazy mint, you simply pass an empty signature. E.g. `0x`.

Royalties are set as basis point, so 1000 = 10%. [More info](https://corporatefinanceinstitute.com/resources/knowledge/finance/basis-point-beep/)
{% endhint %}

#### Example

```javascript
async function mintNow() {
    // Get a token id
    const tokenId = await fetch(`https://ethereum-api-dev.rarible.org/v0.1/nft/collections/{collection}/generate_token_id?minter=${account}`);

    // Instantiate the contract
    const provider = new ethers.providers.Web3Provider(userWalletProvider);
    const signer = provider.getSigner();
    const contract = new ethers.Contract(contractAddress, abi, signer);

    // Call the function
    const tx = await contract.mintAndTransfer(
        [
          tokenId.tokenId,
          uri,
          totalSupply,
          [[creator, 5000], [creator2, 5000]], // You can assign one or add multiple creators, but the value must total 10000
          [[creator, 1000], [creator2, 1000]], // Royalties are set as basis point, so 1000 = 10%. 
          ["0x"]
        ],
        minter,
        amount
      );

      const receipt = await tx.wait();
      console.log('Minting Success', receipt);
}
```

### Uploading the image to IPFS

The image needs to be hosted on IPFS, at Rarible we use pinata, below is a NodeJS example of uploading an image using their API.

```javascript
const axios = require("axios");
const fs = require("fs");
const FormData = require("form-data");

export const pinFileToIPFS = (pinataApiKey, pinataSecretApiKey) => {
  const url = `https://api.pinata.cloud/pinning/pinJSONToIPFS`;
  let data = new FormData();

  data.append("file", fs.createReadStream("./yourfile.png"));

  return axios.post(url, data, {
      headers: {
        "Content-Type": `multipart/form-data; boundary= ${data._boundary}`,
        pinata_api_key: pinataApiKey,
        pinata_secret_api_key: pinataSecretApiKey,
      },
    })
    .then(function (response) {
      console.log(repsonse.IpfsHash);
    })
    .catch(function (error) {
      console.log(error)
    });
};
```

This will return our IPFS CID, the full response looks like this:

```javascript
{
    IpfsHash: // This is the IPFS multi-hash provided back for your content,
    PinSize: // This is how large (in bytes) the content you just pinned is,
    Timestamp: // This is the timestamp for your content pinning (represented in ISO 8601 format)
}
```

### Creating our NFT's Metadata

Now that we have our IPFS CID (Called hash here on out), we can begin constructing our NFT's Metadata file that will be linked to the NFT on-chain. Below is a Metadata file with an explanation of the key and its value.

```javascript
{
   "name": /* NFT Name - This must be a string */,
   "description": /* Description of the NFT - This must be a string */,
   "image": /*  IPFS Hash to our content, this must be prefixed with "ipfs://ipfs/{{ IPFS_HASH ))" - This must be a string */,
   "external_url": /* This is the link to Rarible which we currently don't have, we can fill this in shortly */,
   "animation_url": /* IPFS Hash just as image field, but it allows every type of multimedia files. Like mp3, mp4 etc */,
   // the below section is not needed.
   "attributes": [
      {
         "key": /* Key name - This must be a string */,
         "trait_type": /* Trait name - This must be a string */,
         "value": /* Key Value - This must be a string */
      }
   ]
}
```

### Adding Generated Metadata to IPFS

First, we need to make sure our `external_url` is a Rarible link. We can calculate this link based on the tokenId we create (The tokenId typically is made up of two sections, the first 20 bytes in the users' address and the next 12 bytes can be any random number. We will provide an API to allow you to get the next free available ID.), for this example, our external\_url must be the collection address + tokenId and it will look like this

```javascript
"external_url": "https://app.rarible.com/0x60f80121c31a0d46b5279700f9df786054aa5ee5:123913"
```

_**Notice we use the collection address and value address from our previous call to the tokens endpoint.**_

Now we need to post our NFT's Metadata to IPFS below is an example of how to do this:

```javascript
var axios = require('axios');
var data = JSON.stringify({"name":"Test NFT","description":"Test NFT","image":"ipfs://ipfs/QmW4P1Mgoka8NRCsFAaJt5AaR6XKF6Az97uCiVtGmg1FuG/image.png","external_url":"https://app.rarible.com/0x60f80121c31a0d46b5279700f9df786054aa5ee5:123913","attributes":[{"key":"Test","trait_type":"Test","value":"Test"}]});

var config = {
  method: 'post',
  url: 'https://api.pinata.cloud/pinning/pinFileToIPFS',
  headers: { 
    'pinata_api_key': // KEY_HERE, 
    'pinata_secret_api_key': // SECRET_KEY_HERE, 
    'Content-Type': 'application/json'
  },
  data: data
};

axios(config).then(function (response) {
  console.log(JSON.stringify(response.data));
}).catch(function (error) {
  console.log(error);
});
```

Our Result will look something similar to this:

```javascript
{
    "IpfsHash": "QmNybufJtuvWCZ355HGejvKfUXK8VeLcPA5G7CxT9MXJJp",
    "PinSize": 290,
    "Timestamp": "2021-02-10T14:06:09.255Z"
}
```

Make a note of your new `IpfsHash` since this is now the hash we need to attach to our NFT.

### Custom Contracts

If you are **not** storing your metadata on IPFS, you will need to use your own contracts that have a `baseURI` better suited for where the metadata is stored.

As a starting point, so long as your contract follows the [ERC-721](https://eips.ethereum.org/EIPS/eip-721) or [ERC-1155](https://eips.ethereum.org/EIPS/eip-1155) standard it's NFTs can be bought and sold on Rarible and most other NFT marketplaces. Helpful guides on these standards can be found at [OpenZeppelin](https://docs.openzeppelin.com/contracts/4.x/erc721).

However, you'll need to add more to support royalties and lazy minting as these are not built into the current standards. To support royalties, your contract will need to inherit from the appropriate interfaces, which you can find [here](https://www.npmjs.com/package/@rarible/royalties) or [here](https://www.npmjs.com/package/@rarible/royalties-upgradeable) for an upgradeable version.

Similarly for lazy minting support, you will need to add a `mintAndTransfer` function in your contract for the protocol to call that inherits the expected behavior. You can add this yourself or use [this interface](https://www.npmjs.com/package/@rarible/lazy-mint).

In many cases, it may be easier and faster to just [fork the protocol contracts](https://github.com/rariblecom/protocol-contracts/tree/57043e3f9e93223ef9d65dae351d3c55b34e5bf1/tokens) you wanted to use and change the `baseURI` and any other data upon deployment.

{% hint style="info" %}
You can supply your own `tokenId` instead of getting one from the API call used for Lazy Minting when rolling your own contracts, however, the token id needs to have the minter's address followed by 96 bits, which can include any number you want, in order to pass the `require` checks in the default `mintAndTransfer` function. Alternatively, you can still use the generate token id API used above to supply a tokenId for them.
{% endhint %}

**YAY! Your NFT is now minted! Visit the next section on** [**how to create a sell order**](../exchange/creating-a-sell-order.md) **or to check if your Asset is indexed you can** [**view this page**](https://github.com/rariblecom/protocol-documentation/tree/3f1c8c9f6c98ecb68caeab3c6778338ec28d979a/asset-discovery.md)**.**
