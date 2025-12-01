---
title: "transpilePackages"
source: "https://nextjs.org/docs/13/pages/api-reference/next-config-js/transpilePackages"
---

# transpilePackages

Menu

Pages Router 13

Using Pages Router

Features available in /pages

Version 13

13.5.11

[API Reference](/docs/13/pages/api-reference)[next.config.js Options](/docs/13/pages/api-reference/next-config-js)transpilePackages

You are currently viewing the Pages Router documentation for version 13 of Next.js.

# transpilePackages

Next.js can automatically transpile and bundle dependencies from local packages (like monorepos) or from external dependencies (`node_modules`). This replaces the `next-transpile-modules` package.

next.config.js

```
/** @type {import('next').NextConfig} */
const nextConfig = {
  transpilePackages: ['@acme/ui', 'lodash-es'],
}
 
module.exports = nextConfig
```

## [Version History](#version-history)

VersionChanges`v13.0.0``transpilePackages` added.

Was this helpful?

supported.

Send
