# API Usage with SDK

You can find all available endpoints here:
https://api-reference.rarible.com/

When it comes to the API usage there's really no sense in showing it in code.
What is worth noting is why API is pretty helpful.

While changing environments, you would need to change endpoints accordingly, because different APIs function in different chains e.g. there're different endpoints for Rinkeby than for the Ropsten. SDK is taking full care for managing that.

You can use an api with SDK like this:

```typescript
const response = await sdk.apis.order. (function you want to invoke)
```

The best documentation here is just explore SDK by holding CTRL / CMD and left button to see the available endpoints and needed parameters.
