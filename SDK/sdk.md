# SDK

Protocol SDK in available on GitHub: [https://github.com/rarible/sdk](https://github.com/rarible/sdk)

There is several main types of activities in Rarible protocol.

## NFT activities types

- [Mint](mint.md)
- Transfer
- Burn

## Order activities types

- Sell
- Bid
- Fill
- Cancel

Swap ?
List ?

## Basic scenario

1. Call the function (mint, sell, bid, etc.).
2. The result of the `PrepareResponse` is returned. It has everything you need to display the form. For example, for Sell, there will be a description of which currencies can be used for sale.
3. Form display. For example, for Sell, you need to fill in the fields: how much you want to sell, price.
4. Form confirmation.
5. Sending data using `submit` from `PrepareResponse`.

![](img/sdk1.png)
