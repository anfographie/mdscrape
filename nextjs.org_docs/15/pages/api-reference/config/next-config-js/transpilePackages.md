---
title: "transpilePackages"
source: "https://nextjs.org/docs/15/pages/api-reference/config/next-config-js/transpilePackages"
---

# transpilePackages

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Configuration](/docs/15/pages/api-reference/config)[next.config.js Options](/docs/15/pages/api-reference/config/next-config-js)transpilePackages

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# transpilePackages

Next.js can automatically transpile and bundle dependencies from local packages (like monorepos) or from external dependencies (`node_modules`). This replaces the `next-transpile-modules` package.

next.config.js

```
/** @type {import('next').NextConfig} */
const nextConfig = {
  transpilePackages: ['package-name'],
}
 
module.exports = nextConfig
```

## [Version History](#version-history)

VersionChanges`v13.0.0``transpilePackages` added.

Was this helpful?

supported.

Send
