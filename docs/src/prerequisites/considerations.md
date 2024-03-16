# nodejs

Currently, the npm modules that `wasm-pack` generates must have the [fetch] polyfill as a dependency.

If you encounter errors regarding global `Headers`, `Request`, `Response` and `fetch` Web APIs not being defined in a module built with `wasm-pack build --target nodejs` you may need to make changes so that these values are defined.

## Common errors:

Examples of this category of error:

```js
ReqwestError(reqwest::Error { kind: Builder, source: "JsValue(ReferenceError: Headers is not defined
ReqwestError(reqwest::Error { kind: Builder, source: "JsValue(ReferenceError: Request is not defined

    var ret = getObject(arg0) instanceof Response;
ReferenceError: Response is not defined
```

## Workaround
Import or declare fetch and objects: Headers, Request, Response

```ts
// CommonJS
const fetch = require('node-fetch');

// ES Module
import fetch from 'node-fetch';

// @ts-ignore
global.fetch = fetch;
// @ts-ignore
global.Headers = fetch.Headers;
// @ts-ignore
global.Request = fetch.Request;
// @ts-ignore
global.Response = fetch.Response;
```

[fetch]: https://github.com/node-fetch/node-fetch

