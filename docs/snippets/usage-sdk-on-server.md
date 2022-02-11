## Usage SDK on the server (backend)

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
