---
title: "productionBrowserSourceMaps"
source: "https://nextjs.org/docs/14/pages/api-reference/next-config-js/productionBrowserSourceMaps"
---

# productionBrowserSourceMaps

Menu

Pages Router 14

Using Pages Router

Features available in /pages

Version 14

14.2.33

[API Reference](/docs/14/pages/api-reference)[next.config.js Options](/docs/14/pages/api-reference/next-config-js)productionBrowserSourceMaps

You are currently viewing the Pages Router documentation for version 14 of Next.js.

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
