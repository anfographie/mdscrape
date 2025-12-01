---
title: "onDemandEntries"
source: "https://nextjs.org/docs/15/pages/api-reference/config/next-config-js/onDemandEntries"
---

# onDemandEntries

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Configuration](/docs/15/pages/api-reference/config)[next.config.js Options](/docs/15/pages/api-reference/config/next-config-js)onDemandEntries

You are currently viewing the Pages Router documentation for version 15 of Next.js.

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
