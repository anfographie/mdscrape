---
title: "Partial Prerendering (experimental)"
source: "https://nextjs.org/docs/14/app/api-reference/next-config-js/partial-prerendering"
---

# Partial Prerendering (experimental)

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[next.config.js Options](/docs/14/app/api-reference/next-config-js)Partial Prerendering (experimental)

You are currently viewing documentation for version 14 of Next.js.

# Partial Prerendering (experimental)

> **Warning**: Partial Prerendering is an experimental feature and is currently **not suitable for production environments**.

Partial Prerendering is an experimental feature that allows static portions of a route to be prerendered and served from the cache with dynamic holes streamed in, all in a single HTTP request.

Partial Prerendering is available in `next@canary`:

Terminal

```
npm install next@canary
```

You can enable Partial Prerendering by setting the experimental `ppr` flag:

next.config.js

```
/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    ppr: true,
  },
}
 
module.exports = nextConfig
```

> **Good to know:**
> 
> - Partial Prerendering does not yet apply to client-side navigations. We are actively working on this.
> - Partial Prerendering is designed for the [Node.js runtime](/docs/14/app/building-your-application/rendering/edge-and-nodejs-runtimes) only. Using the subset of the Node.js runtime is not needed when you can instantly serve the static shell.

Learn more about Partial Prerendering in the [Next.js Learn course](/learn/dashboard-app/partial-prerendering).

Was this helpful?

supported.

Send
