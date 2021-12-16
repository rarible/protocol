# API Usage with SDK

You can find all available endpoints here:
https://api-reference.rarible.com/

When it comes to API usage there's really no sense in showing it in code.
What is worth noting is why API is pretty helpful.

Because you work on a few different blockchains e.g. Mainnet, Rinkeby etc. you would have to have a different endpoint for everytime you change a network. When using Rarible SDK, it is taking care of that.

You can use api like that

```typescript
const response = await sdk.apis.order. function you want to invoke
```

The best documentation here is just explore SDK by holding CTRL / CMD and left button to see available endpoints and needed parameters.
