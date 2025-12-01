---
title: "logging"
source: "https://nextjs.org/docs/14/app/api-reference/next-config-js/logging"
---

# logging

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[next.config.js Options](/docs/14/app/api-reference/next-config-js)logging

You are currently viewing documentation for version 14 of Next.js.

# logging

You can configure the logging level and whether the full URL is logged to the console when running Next.js in development mode.

Currently, `logging` only applies to data fetching using the `fetch` API. It does not yet apply to other logs inside of Next.js.

next.config.js

```
module.exports = {
  logging: {
    fetches: {
      fullUrl: true,
    },
  },
}
```

Was this helpful?

supported.

Send
