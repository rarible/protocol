# Fees

[RaribleTransferManager](https://github.com/rarible/protocol-contracts/blob/master/exchange-v2/contracts/RaribleTransferManager.md) supports the following types of fees:

* Protocol fees — are charged on both sides of the transaction.
* Origin fees — set for each order. It may differ for two orders.
* Royalties — the author of the work will receive a part of each sale.

## Algorithm

The transfer of assets takes place inside the `doTransfers`. The following parameters are used as arguments:

* `LibAsset.AssetType` `makeMatch` — `AssetType` on the make-side order
* `LibAsset.AssetType` `takeMatch` — `AssetType` on the take-side order
* `LibFill.FillResult` `fill` — values on both sides that will be passed by match
* `LibOrder.Order` `leftOrder` — left order data
* `LibOrder.Order` `rightOrder` — right order data

In this method, the following actions are performed.

### How do we calculate the commission side of the transaction?

1. Use `LibFeeSide.getFeeSide`. It takes as arguments `assetClasses` of both sides (for example, `ETH` and `ERC20`).
2. `LibFeeSide.getFeeSide` tries to determine side to pay fees:

![](../img/eth_5.png)

* If there is ETH on any side of the transaction, it is used.
* If there is no ETH, we check if there is an ERC-20 and use it.
* If there is no ERC-20, check if there is an ERC-1155 and use it.
* Otherwise, no fee will be charged. (e.g. if two ERC-721 are involved in the transaction)

### Transfer

1. If the make-side pays fees:
    * calling `doTransfersWithFees` for the make-side
    * calling `transferPayouts` for the take-side
2. If the take-side pays fees:
    * calling `doTransfersWithFees` for the take-side
    * calling `transferPayouts` for the make-side
3. If the side for the payment of fees are not defined:
    * call `transferPayouts` for both sides

When computing the total amount of the asset:

* The protocol fee is added on top of the filled amount.
* The fee for sending the buyer's order is also added on top.

If the buyer uses the ERC-20 token for payment, he must approve the calculated number of tokens.

If the buyer uses ETH, they must send the calculated amount to ETH along with the transaction.

For more information about fees, see the page [RaribleTransferManager](https://github.com/rarible/protocol-contracts/blob/master/exchange-v2/contracts/RaribleTransferManager.md) on GitHub.
