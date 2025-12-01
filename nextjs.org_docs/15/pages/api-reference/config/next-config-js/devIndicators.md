---
title: "devIndicators"
source: "https://nextjs.org/docs/15/pages/api-reference/config/next-config-js/devIndicators"
---

# devIndicators

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Configuration](/docs/15/pages/api-reference/config)[next.config.js Options](/docs/15/pages/api-reference/config/next-config-js)devIndicators

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# devIndicators

`devIndicators` allows you to configure the on-screen indicator that gives context about the current route you're viewing during development.

Types

```
  devIndicators: false | {
    position?: 'bottom-right'
    | 'bottom-left'
    | 'top-right'
    | 'top-left', // defaults to 'bottom-left',
  },
```

Setting `devIndicators` to `false` will hide the indicator, however Next.js will continue to surface any build or runtime errors that were encountered.

## [Troubleshooting](#troubleshooting)

### [Indicator not marking a route as static](#indicator-not-marking-a-route-as-static)

If you expect a route to be static and the indicator has marked it as dynamic, it's likely the route has opted out of static rendering.

You can confirm if a route is [static](/docs/15/app/getting-started/partial-prerendering#static-rendering) or [dynamic](/docs/15/app/getting-started/partial-prerendering#dynamic-rendering) by building your application using `next build --debug`, and checking the output in your terminal. Static (or prerendered) routes will display a `○` symbol, whereas dynamic routes will display a `ƒ` symbol. For example:

Build Output

```
Route (app)                              Size     First Load JS
┌ ○ /_not-found                          0 B               0 kB
└ ƒ /products/[id]                       0 B               0 kB
 
○  (Static)   prerendered as static content
ƒ  (Dynamic)  server-rendered on demand
```

When exporting [`getServerSideProps`](/docs/15/pages/building-your-application/data-fetching/get-server-side-props) or [`getInitialProps`](/docs/15/pages/api-reference/functions/get-initial-props) from a page, it will be marked as dynamic.

## [Version History](#version-history)

VersionChanges`v15.2.0`Improved on-screen indicator with new `position` option. `appIsrStatus`, `buildActivity`, and `buildActivityPosition` options have been deprecated.`v15.0.0`Static on-screen indicator added with `appIsrStatus` option.

Was this helpful?

supported.

Send
