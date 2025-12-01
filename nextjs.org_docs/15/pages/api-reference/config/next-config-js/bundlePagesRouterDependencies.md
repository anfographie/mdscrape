---
title: "bundlePagesRouterDependencies"
source: "https://nextjs.org/docs/15/pages/api-reference/config/next-config-js/bundlePagesRouterDependencies"
---

# bundlePagesRouterDependencies

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Configuration](/docs/15/pages/api-reference/config)[next.config.js Options](/docs/15/pages/api-reference/config/next-config-js)bundlePagesRouterDependencies

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# bundlePagesRouterDependencies

Enable automatic server-side dependency bundling for Pages Router applications. Matches the automatic dependency bundling in App Router.

next.config.js

```
/** @type {import('next').NextConfig} */
const nextConfig = {
  bundlePagesRouterDependencies: true,
}
 
module.exports = nextConfig
```

Explicitly opt-out certain packages from being bundled using the [`serverExternalPackages`](/docs/15/pages/api-reference/config/next-config-js/serverExternalPackages) option.

## [Version History](#version-history)

VersionChanges`v15.0.0`Moved from experimental to stable. Renamed from `bundlePagesExternals` to `bundlePagesRouterDependencies`

Was this helpful?

supported.

Send
