## Usage SDK on the server (backend)

For working with SDK on the server, add the next dependencies in the beginning:

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
