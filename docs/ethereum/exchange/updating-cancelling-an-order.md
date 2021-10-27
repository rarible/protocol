# Updating/Canceling an Order

## Updating an Order

To update an order we need to make the changes and send a POST request to the API this can be found on the [Creating A Sell Order page](creating-a-sell-order.md#creating-an-order).

New Orders check the Start, End, taker, make and value. If any of these are invalid you will receive a 400 response code from the API.

{% hint style="danger" %}
The price can only be lowered and not increased, to increase the price you will need to cancel the order and create a new one.
{% endhint %}

## Canceling an Order

Canceling an order needs to be done on-chain by calling the cancel method on the [exchange contract](exchangev2.md).

```text
function cancel(LibOrder.Order memory order) public {
 require(_msgSender() == order.maker, "not a maker");
 bytes32 orderKeyHash = LibOrder.hashKey(order);
 fills[orderKeyHash] = UINT256_MAX;
 emit Cancel(orderKeyHash);
}
```



