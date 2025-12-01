---
title: "reactStrictMode"
source: "https://nextjs.org/docs/14/pages/api-reference/next-config-js/reactStrictMode"
---

# reactStrictMode

Menu

Pages Router 14

Using Pages Router

Features available in /pages

Version 14

14.2.33

[API Reference](/docs/14/pages/api-reference)[next.config.js Options](/docs/14/pages/api-reference/next-config-js)reactStrictMode

You are currently viewing the Pages Router documentation for version 14 of Next.js.

# reactStrictMode

> **Good to know**: Since Next.js 13.4, Strict Mode is `true` by default with `app` router, so the above configuration is only necessary for `pages`. You can still disable Strict Mode by setting `reactStrictMode: false`.

> **Suggested**: We strongly suggest you enable Strict Mode in your Next.js application to better prepare your application for the future of React.

React's [Strict Mode](https://react.dev/reference/react/StrictMode) is a development mode only feature for highlighting potential problems in an application. It helps to identify unsafe lifecycles, legacy API usage, and a number of other features.

The Next.js runtime is Strict Mode-compliant. To opt-in to Strict Mode, configure the following option in your `next.config.js`:

next.config.js

```
module.exports = {
  reactStrictMode: true,
}
```

If you or your team are not ready to use Strict Mode in your entire application, that's OK! You can incrementally migrate on a page-by-page basis using `<React.StrictMode>`.

Was this helpful?

supported.

Send
