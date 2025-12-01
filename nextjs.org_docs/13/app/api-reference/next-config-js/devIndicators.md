---
title: "devIndicators"
source: "https://nextjs.org/docs/13/app/api-reference/next-config-js/devIndicators"
---

# devIndicators

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[next.config.js Options](/docs/13/app/api-reference/next-config-js)devIndicators

You are currently viewing documentation for version 13 of Next.js.

# devIndicators

When you edit your code, and Next.js is compiling the application, a compilation indicator appears in the bottom right corner of the page.

> **Good to know**: This indicator is only present in development mode and will not appear when building and running the app in production mode.

In some cases this indicator can be misplaced on your page, for example, when conflicting with a chat launcher. To change its position, open `next.config.js` and set the `buildActivityPosition` in the `devIndicators` object to `bottom-right` (default), `bottom-left`, `top-right` or `top-left`:

next.config.js

```
module.exports = {
  devIndicators: {
    buildActivityPosition: 'bottom-right',
  },
}
```

In some cases this indicator might not be useful for you. To remove it, open `next.config.js` and disable the `buildActivity` config in `devIndicators` object:

next.config.js

```
module.exports = {
  devIndicators: {
    buildActivity: false,
  },
}
```

Was this helpful?

supported.

Send
