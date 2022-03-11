---
title: Transfer tokens between addresses
description: Explanation of token transfering process
---

# Transfering token between two addresses

Process of transfering tokens between two addresses is straightforward. In order for the transfer to be successful it has to be created from an address to which an NFT belongs to. Signing of the transaction by the owner will also be required.

Basically what we need is two things:

- itemId: which allows to uniquely identify any NFT on any blockchain,
- recipientAddress: which tells us where the token should be transfered.

### Create an ItemId & PrepareTransferRequest

Item Id, as a lot of addresses in Rarible Protocol, consist of a few parts, separated by colon sign - ':'.

We can create Item Id by merging:

1. Blockchain name - ETHEREUM, TEZOS, FLOW, etc.,
2. Contract address - address of a smart contract responsible for NFT creation (you can find a smart contract address for specific blockchain [here]("/")),
3. Token Id - id of minted / lazy minted token.

So the ItemId, in theory, will look like that:
{BLOCKCHAIN_NAME}:{CONTRACT_ADDRESS}:{TOKEN_ID}

while in practice it can look like that:

```typescript
ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382070;
```

On the other hand we have a PrepareTransferRequest which is a simple object of PrepareTransferRequest type with an itemId property.

In code you can do it like that:

```typescript
// Imports
// unionAddress will be used and explained further in the article
import { toItemId, toUnionAddress } from "@rarible/types";

const itemId =
  "ETHEREUM:0x6ede7f3c26975aad32a475e1021d8f6f39c89d82:55143609719300586327244080327388661151936544170854464635146779205246455382070";

const transferRequest: PrepareTransferRequest = {
  itemId: toItemId(itemId),
};
```

### Call sdk.nft.transfer method with transferRequest as an argument

In the next step we take PrepareTransferRequest that we've created in previous step and use it to call sdk.nft.transfer method. It will return us a submit function as well as available options for that operation.

```typescript
const transferResponse = await sdk.nft.transfer(transferRequest);

// Example of a response
// {
//     "multiple": false,
//     "maxAmount": "1",
//     "submit": f()
// }
```

### Call a submit function

Now, there is one thing left and it is to call a submit function we previously fetched. This is the step which will trigger a Metamask window and a payment, since we're doing write operation on a blockchain (changing an owner is a write operation).

Submit object consist of two parameters:

- to (required) - which is of type of UnifiedAddress {BLOCKCHAIN_NAME}:{ADDRESS},
- amount - if the multiple flag from the previous step was true, it's possible to transfer more than one NFT, default to one.

```typescript
const response = await transferResponse.submit({
  to: toUnionAddress("ETHEREUM:0x18c37f21D3C29f9a53A96CA678026DC660180065"),
  amount: 1,
});

// Example of a response
// {
//     "transaction": {
//         "receipt": {},
//         "hash": "0xe78cb6963ac4c960c5c623d08d1407a",
//         "data": "0x832fbb2...",
//         "nonce": 24,
//         "from": "0x79ea2d536b5b7144a3eabdc6a7e43130199291c0",
//         "to": "0x6ede7f3c26975aad32a475e1021d8f6f39c89d82"
//     },
//     "network": "rinkeby",
//     "blockchain": "ETHEREUM"
// }
```

That's all in this section.
