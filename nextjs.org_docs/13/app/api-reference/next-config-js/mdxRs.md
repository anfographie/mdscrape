---
title: "mdxRs"
source: "https://nextjs.org/docs/13/app/api-reference/next-config-js/mdxRs"
---

# mdxRs

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[next.config.js Options](/docs/13/app/api-reference/next-config-js)mdxRs

You are currently viewing documentation for version 13 of Next.js.

# mdxRs

For use with `@next/mdx`. Compile MDX files using the new Rust compiler.

next.config.js

```
const withMDX = require('@next/mdx')()
 
/** @type {import('next').NextConfig} */
const nextConfig = {
  pageExtensions: ['ts', 'tsx', 'mdx'],
  experimental: {
    mdxRs: true,
  },
}
 
module.exports = withMDX(nextConfig)
```

Was this helpful?

supported.

Send
