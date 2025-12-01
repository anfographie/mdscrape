---
title: "devIndicators"
source: "https://nextjs.org/docs/14/pages/api-reference/next-config-js/devIndicators"
---

# devIndicators

Menu

Pages Router 14

Using Pages Router

Features available in /pages

Version 14

14.2.33

[API Reference](/docs/14/pages/api-reference)[next.config.js Options](/docs/14/pages/api-reference/next-config-js)devIndicators

You are currently viewing the Pages Router documentation for version 14 of Next.js.

# devIndicators

> **Good to know**: This indicator was removed in Next.js version 10.0.1. We recommend upgrading to the latest version of Next.js.

When a page qualifies for [Automatic Static Optimization](/docs/14/pages/building-your-application/rendering/automatic-static-optimization) we show an indicator to let you know.

This is helpful since automatic static optimization can be very beneficial and knowing immediately in development if the page qualifies can be useful.

In some cases this indicator might not be useful, like when working on electron applications. To remove it open `next.config.js` and disable the `autoPrerender` config in `devIndicators`:

next.config.js

```
module.exports = {
  devIndicators: {
    autoPrerender: false,
  },
}
```

Was this helpful?

supported.

Send
