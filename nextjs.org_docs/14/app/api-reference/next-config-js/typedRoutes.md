---
title: "typedRoutes (experimental)"
source: "https://nextjs.org/docs/14/app/api-reference/next-config-js/typedRoutes"
---

# typedRoutes (experimental)

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[next.config.js Options](/docs/14/app/api-reference/next-config-js)typedRoutes

You are currently viewing documentation for version 14 of Next.js.

# typedRoutes (experimental)

Experimental support for [statically typed links](/docs/14/app/building-your-application/configuring/typescript#statically-typed-links). This feature requires using the App Router as well as TypeScript in your project.

next.config.js

```
/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    typedRoutes: true,
  },
}
 
module.exports = nextConfig
```

Was this helpful?

supported.

Send
