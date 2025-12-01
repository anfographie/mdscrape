---
title: "typedRoutes (experimental)"
source: "https://nextjs.org/docs/13/app/api-reference/next-config-js/typedRoutes"
---

# typedRoutes (experimental)

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[next.config.js Options](/docs/13/app/api-reference/next-config-js)typedRoutes

You are currently viewing documentation for version 13 of Next.js.

# typedRoutes (experimental)

Experimental support for [statically typed links](/docs/13/app/building-your-application/configuring/typescript#statically-typed-links). This feature requires using the App Router as well as TypeScript in your project.

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
