---
title: "httpAgentOptions"
source: "https://nextjs.org/docs/13/app/api-reference/next-config-js/httpAgentOptions"
---

# httpAgentOptions

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[next.config.js Options](/docs/13/app/api-reference/next-config-js)httpAgentOptions

You are currently viewing documentation for version 13 of Next.js.

# httpAgentOptions

In Node.js versions prior to 18, Next.js automatically polyfills `fetch()` with [undici](/docs/13/architecture/supported-browsers#polyfills) and enables [HTTP Keep-Alive](https://developer.mozilla.org/docs/Web/HTTP/Headers/Keep-Alive) by default.

To disable HTTP Keep-Alive for all `fetch()` calls on the server-side, open `next.config.js` and add the `httpAgentOptions` config:

next.config.js

```
module.exports = {
  httpAgentOptions: {
    keepAlive: false,
  },
}
```

Was this helpful?

supported.

Send
