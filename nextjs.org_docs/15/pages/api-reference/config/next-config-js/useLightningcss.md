---
title: "useLightningcss"
source: "https://nextjs.org/docs/15/pages/api-reference/config/next-config-js/useLightningcss"
---

# useLightningcss

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Configuration](/docs/15/pages/api-reference/config)[next.config.js Options](/docs/15/pages/api-reference/config/next-config-js)useLightningcss

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# useLightningcss

This feature is currently experimental and subject to change, it's not recommended for production. Try it out and share your feedback on [GitHub](https://github.com/vercel/next.js/issues).

Experimental support for using [Lightning CSS](https://lightningcss.dev), a fast CSS bundler and minifier, written in Rust.

next.config.ts

TypeScript

JavaScriptTypeScript

```
import type { NextConfig } from 'next'
 
const nextConfig: NextConfig = {
  experimental: {
    useLightningcss: true,
  },
}
 
export default nextConfig
```

Was this helpful?

supported.

Send
