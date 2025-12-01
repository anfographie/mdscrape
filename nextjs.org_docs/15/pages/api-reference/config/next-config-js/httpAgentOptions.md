---
title: "httpAgentOptions"
source: "https://nextjs.org/docs/15/pages/api-reference/config/next-config-js/httpAgentOptions"
---

# httpAgentOptions

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Configuration](/docs/15/pages/api-reference/config)[next.config.js Options](/docs/15/pages/api-reference/config/next-config-js)httpAgentOptions

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# httpAgentOptions

In Node.js versions prior to 18, Next.js automatically polyfills `fetch()` with [undici](/docs/15/architecture/supported-browsers#polyfills) and enables [HTTP Keep-Alive](https://developer.mozilla.org/docs/Web/HTTP/Headers/Keep-Alive) by default.

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
