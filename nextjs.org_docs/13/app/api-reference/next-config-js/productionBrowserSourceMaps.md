---
title: "productionBrowserSourceMaps"
source: "https://nextjs.org/docs/13/app/api-reference/next-config-js/productionBrowserSourceMaps"
---

# productionBrowserSourceMaps

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[next.config.js Options](/docs/13/app/api-reference/next-config-js)productionBrowserSourceMaps

You are currently viewing documentation for version 13 of Next.js.

# productionBrowserSourceMaps

Source Maps are enabled by default during development. During production builds, they are disabled to prevent you leaking your source on the client, unless you specifically opt-in with the configuration flag.

Next.js provides a configuration flag you can use to enable browser source map generation during the production build:

next.config.js

```
module.exports = {
  productionBrowserSourceMaps: true,
}
```

When the `productionBrowserSourceMaps` option is enabled, the source maps will be output in the same directory as the JavaScript files. Next.js will automatically serve these files when requested.

- Adding source maps can increase `next build` time
- Increases memory usage during `next build`

Was this helpful?

supported.

Send
