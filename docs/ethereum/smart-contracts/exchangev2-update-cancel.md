---
title: ExchangeV2 Update and Cancel
description: The main information about Update and Cancel in Rarible Smart Contracts
---

# ExchangeV2 Update and Cancel

## Update

To update the order:

1. Make changes.
2. Send a request to the API (see [Sell Order](exchangev2-sell-bid.md#sell-order)).

New orders check the: start, end, take, make and value fields.

The price can only be reduced. You will need to cancel the order and create a new one to increase the price. Since if the user has already signed a message with a lower price, someone could save this message and signature. You can't cancel it without contacting the contract.

## Cancel

To cancel the order, call the cancellation method in the ExchangeV2 contract.

```
function cancel(LibOrder.Order memory order) public {
 require(_msgSender() == order.maker, "not a maker");
 bytes32 orderKeyHash = LibOrder.hashKey(order);
 fills[orderKeyHash] = UINT256_MAX;
 emit Cancel(orderKeyHash);
}
```

An error will be returned when matching such an order.

Orders makers can only call this function. It marks orders that cannot be filled.
