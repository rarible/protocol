# Matching Orders

## Overview

In the [Exchange Contract](../exchange/exchange-overview.md), there is the matchOrders function. This function takes two sides of order \(The Seller Order & Buy order\) and attempts to match them. The Matching Algorithm can be extended by using a custom IAssetMatcher.

The Matching Algorithm can be divided into several steps listed below:

* **Order Validation** - This is checks the order parameters are valid and the caller is authorized to execute the order.
* **Asset Matching** - This checks that the assets from left and right order match and then extracts the matching assets.
* **Calculating The Fill** - This checks and finds out what exact values should be filled. Orders can also be matched partly, this occurs if one of the sides doesn't want to fill other orders completely.
* **Order Execution** - This executes the transfers \(Swap\) of the assets and will save the fill of the order if needed.

## Order Validation

1. If the `msg.sender` matches the address which placed the order we do not check for validation.
2. Verifying the signatures, if the request is submitted via a contract we validate the signature via EIP-1271
3. If verification is not successful, then we need to validate the order in an external contract, this is done on-chain via an external contract \(Possibly a custom IAssetMatcher\).

## Asset Matching

1. The opposite sides of the order must match at least one side of the order, this is done within the contract for simple assets. Complex asset swaps are done via our registry within which custom matching contracts are registered and controlled.
2. Next, we emit stating the order was successfully matched.

## Calculating The Fill

This is how long the order takes to be executed, we save this for orders that are not sent by the `msg.sender` to prevent wasting gas.

## Order Execution

This is where we determine which assets need to be transferred from each party. Our external contract considers the transfer list. Below is the structure of the transfer list

* **Asset -** Assets to be Swapped.
* **Amount** - Amount of Ether/ERC20/ERC721/ERC1155 token to be swapped.
* **From** - Address the Buy Order is sending assets from.
* **To** - Address the Sell Order is sending assets from.
* **Type** - Type can be one of several items like "protocol" \| "fee" \| "royalty" \| "maker" \| "taker" - can be expanded. This will be done in bytes32.

#### Translations & Event Emits

The transfer events are emitted through the proxy register, this makes it so custom transfers are possible.



