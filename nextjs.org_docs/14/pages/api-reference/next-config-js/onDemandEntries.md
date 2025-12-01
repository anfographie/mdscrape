---
title: "onDemandEntries"
source: "https://nextjs.org/docs/14/pages/api-reference/next-config-js/onDemandEntries"
---

# onDemandEntries

Menu

Pages Router 14

Using Pages Router

Features available in /pages

Version 14

14.2.33

[API Reference](/docs/14/pages/api-reference)[next.config.js Options](/docs/14/pages/api-reference/next-config-js)onDemandEntries

You are currently viewing the Pages Router documentation for version 14 of Next.js.

# onDemandEntries

Next.js exposes some options that give you some control over how the server will dispose or keep in memory built pages in development.

To change the defaults, open `next.config.js` and add the `onDemandEntries` config:

next.config.js

```
module.exports = {
  onDemandEntries: {
    // period (in ms) where the server will keep pages in the buffer
    maxInactiveAge: 25 * 1000,
    // number of pages that should be kept simultaneously without being disposed
    pagesBufferLength: 2,
  },
}
```

Was this helpful?

supported.

Send
