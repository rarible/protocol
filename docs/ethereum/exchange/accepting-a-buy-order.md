# Accepting a Buy Order

To buy an item or accept a bid user should send transaction to [Exchange](https://rinkeby.etherscan.io/address/0x43162023c187662684abaf0b211dccb96fa4ed8a) contract's matchOrders function.


Example for sending matchOrders is [here](https://github.com/evgenynacu/sign-typed-data/blob/ropsten/src/order/script.ts#L82).

matchOrders function defined in [ExchangeV2Core](https://github.com/rarible/protocol-contracts/blob/master/exchange-v2/contracts/ExchangeV2Core.sol) has 4 parameters:

1. left order.
2. left order signature
3. right order
4. right order signature 

More about order structure can be found [here - Order Structure](https://docs.rarible.org/ethereum/exchange/exchange-overview/#order-structure)

### Pay ETH for ERC721

**You can only fill an ETH order if your side of the order is providing the ETH**. Otherwise you would have to use WETH which has the transferFrom capability.

Encoded order

```text
{
  "maker": "0x744222844bfecc77156297a6427b5876a6769e19",
  "makeAsset": { "assetType": { "assetClass": "0xaaaebeba", "data": "0x" }, "value": "100000000000000000" },
  "taker": "0x0000000000000000000000000000000000000000",
  "takeAsset": {
    "assetType": {
      "assetClass": "0x73ad2146",
      "data": "0x000000000000000000000000cfa14f6dc737b8f9e0fc39f05bf3d903ac5d45750000000000000000000000000000000000000000000000000000000000000005"
    },
    "value": "1"
  },
  "salt": "0",
  "start": "0",
  "end": "0",
  "dataType": "0x4c234266",
  "data": "0x0000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"
}
```

[Example transaction](https://rinkeby.etherscan.io/tx/0x2d01b1869b556629acf7304b53d2f77fd927a2c3c9daea02aa093ba8ba41b4c6) that has both a signed sell order and an unsigned buy order, submitted by the buyer.

## Bid Orders

A bid is just an unmatched buy order. The bidder submits the order to the indexer, like shown in 

**Creating a sell order**. The seller accepts it by creating a matched order.

