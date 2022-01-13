# API Usage with SDK

You can find all available endpoints here:
https://api.rarible.org/v0.1/doc

API is pretty easy when it comes to sdk, you can use it with SDK like this:

```typescript
const response = await sdk.apis.order. (function you want to invoke)
```

When it comes to the API the most important thing is to remember that there are different endpoints for different environments.

While changing environments, you would need to change endpoints accordingly, because different APIs function in different chains e.g. there're different endpoints for Rinkeby than for the Ropsten. SDK is taking full care for managing that.

Mainnet environments

- eth: mainnet
- tezos: mainnet
- flow: mainnet
- solana: mainnet

Testnet environments

- eth: rinkeby
- tezos: hangzhou
- flow: devnet
- solana: testnet

The best documentation here is just explore SDK by holding CTRL / CMD and left button to see the available endpoints and needed parameters.
