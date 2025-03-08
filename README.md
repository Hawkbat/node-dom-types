# node-dom-types

TypeScript definitions for the subset of DOM APIs supported in both Node.js and the browser.

This is useful for writing cross-platform libraries in TypeScript that .

In the future, this could possibly be extracted directly from `lib.dom.d.ts` instead of hand-copied and edited.

## Usage

In your project's `package.json` file, add this package under the name `@typescript/lib-dom`:

```json
{
  "devDependencies": {
    "@typescript/lib-dom": "npm:node-dom-types@23.9.0"
  }
}
```

In your `tsconfig.json` file, set your `lib` array to include `DOM` and explicitly enable [libReplacement](https://www.typescriptlang.org/tsconfig/#libReplacement) for future-proofing:

```json
{
    "compilerOptions": {
        "lib": ["ESNext", "DOM"],
        "libReplacement": true
    }
}
```

Replace `"ESNext"` with your preferred core lib target.

If everything is set up properly, your TypeScript code should only have access to the options listed below instead of the full DOM API.

Note that it is _painfully_ easy to still include `@types/node` or `lib.dom.d.ts` indirectly by importing another module which depends on one or the other. This will cause all of the corresponding types to be present in the environment, defeating the purpose of this package. See [Issue #37053](https://github.com/microsoft/TypeScript/issues/37053) and [Issue #50424](https://github.com/microsoft/TypeScript/issues/50424) in the TypeScript repository for related issues.

## Versions

This version of the type definitions was created using these Node.js and lib.dom.ts versions:

- Node.js v23.9.0
- TypeScript 5.8.2

## Available Types

Globals implemented in Node.js as of the version above:

### Classes

- AbortController
- AbortSignal
- Blob
- ByteLengthQueuingStrategy
- BroadcastChannel
- CloseEvent
- CompressionStream
- CountQueuingStrategy
- CryptoKey
- CustomEvent
- DecompressionStream
- DOMException
- Event
- EventSource 🦄
- EventTarget ⚠️
  - Some quirks due to being decoupled from the DOM, see [EventTarget and Event API](https://nodejs.org/docs/latest/api/events.html#eventtarget-and-event-api)
- File ⚠️
  - Minor; `webkitRelativePath` field is missing
- FormData ⚠️
  - No support for tying instances to a `HTMLFormElement`
- Headers
- MessageChannel
- MessageEvent
- MessagePort
- ReadableByteStreamController
- ReadableStream
- ReadableStreamBYOBReader
- ReadableStreamBYOBRequest
- ReadableStreamDefaultController
- ReadableStreamDefaultReader
- Request
- Response
- TextDecoder
- TextDecoderStream
- TextEncoder
- TextEncoderStream
- TransformStream
- TransformStreamDefaultController
- URL
- URLSearchParams
- WebSocket
- WritableStream
- WritableStreamDefaultController
- WritableStreamDefaultWriter

### Namespaces

- WebAssembly
- console.*
- crypto.*
- localStorage.* 🦄
- navigator.* ⚠️
  - Only a few common fields available
- performance.* ⚠️
  - DOM-specific fields are not available
- sessionStorage.* 🦄

### Functions

- fetch()
- setInterval()/clearInterval() ⚠️
  - Handle type is object intead of number
- setTimeout()/clearTimeout() ⚠️
  - Handle type is object intead of number
- structuredClone()

⚠️: Node.js's implementation is incomplete or incompatible

🦄: Partially implemented behind a Node CLI flag, not available via this package yet
