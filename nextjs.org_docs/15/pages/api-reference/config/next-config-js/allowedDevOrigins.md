---
title: "allowedDevOrigins"
source: "https://nextjs.org/docs/15/pages/api-reference/config/next-config-js/allowedDevOrigins"
---

# allowedDevOrigins

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Configuration](/docs/15/pages/api-reference/config)[next.config.js Options](/docs/15/pages/api-reference/config/next-config-js)allowedDevOrigins

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# allowedDevOrigins

Next.js does not automatically block cross-origin requests during development, but will block by default in a future major version of Next.js to prevent unauthorized requesting of internal assets/endpoints that are available in development mode.

To configure a Next.js application to allow requests from origins other than the hostname the server was initialized with (`localhost` by default) you can use the `allowedDevOrigins` config option.

`allowedDevOrigins` allows you to set additional origins that can be used in development mode. For example, to use `local-origin.dev` instead of only `localhost`, open `next.config.js` and add the `allowedDevOrigins` config:

next.config.js

```
module.exports = {
  allowedDevOrigins: ['local-origin.dev', '*.local-origin.dev'],
}
```

Was this helpful?

supported.

Send
