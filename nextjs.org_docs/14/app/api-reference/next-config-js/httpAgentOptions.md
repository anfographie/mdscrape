---
title: "httpAgentOptions"
source: "https://nextjs.org/docs/14/app/api-reference/next-config-js/httpAgentOptions"
---

# httpAgentOptions

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[next.config.js Options](/docs/14/app/api-reference/next-config-js)httpAgentOptions

You are currently viewing documentation for version 14 of Next.js.

# httpAgentOptions

In Node.js versions prior to 18, Next.js automatically polyfills `fetch()` with [undici](/docs/14/architecture/supported-browsers#polyfills) and enables [HTTP Keep-Alive](https://developer.mozilla.org/docs/Web/HTTP/Headers/Keep-Alive) by default.

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
