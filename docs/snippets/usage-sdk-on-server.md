## Using SDK on server application

The SDK was designed for use on the frontend side. To use the SDK on the server side (backend):

1. Install packages:

    ```shell
    yarn add tslib@2.3.1
    yarn add form-data
    yarn add node-fetch
    ```

2. Add dependencies:

    ```typescript
    global.FormData = require("form-data")
    global.window = {
      fetch: require("node-fetch"),
      dispatchEvent: () => {
      },
    }
    global.CustomEvent = function CustomEvent() {
      return
    }
    ```

3. Try our [example](https://github.com/rarible/sdk/blob/master/packages/sdk/example/backend/buy.ts) to buy Ethereum NFT item on Rinkeby network.

    Pass private key, node RPC URL, network ID, item ID for buyout and start:

    ```shell
    ETH_PRIVATE_KEY="0x..." \
    ETHEREUM_RPC_URL="https://rinkeby.infura.io/..." \
    ETHEREUM_NETWORK_ID="4" \
    BUYOUT_ITEM_ID="0x1AF7A7555263F275433c6Bb0b8FdCD231F89B1D7:102581254137174039089845694331937600507918590364933200920056519678660477714440" \
    ts-node packages/sdk/example/backend/buy.ts
    ```
