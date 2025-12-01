---
title: "mdxRs"
source: "https://nextjs.org/docs/14/app/api-reference/next-config-js/mdxRs"
---

# mdxRs

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[next.config.js Options](/docs/14/app/api-reference/next-config-js)mdxRs

You are currently viewing documentation for version 14 of Next.js.

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
