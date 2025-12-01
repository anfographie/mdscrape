---
title: "StaleTimes (experimental)"
source: "https://nextjs.org/docs/14/app/api-reference/next-config-js/staleTimes"
---

# StaleTimes (experimental)

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[next.config.js Options](/docs/14/app/api-reference/next-config-js)StaleTimes (experimental)

You are currently viewing documentation for version 14 of Next.js.

# StaleTimes (experimental)

> **Warning**: The `staleTimes` configuration is an experimental feature. This configuration strategy will likely change in the future.

`staleTimes` is an experimental feature that allows configuring the [invalidation period](/docs/14/app/building-your-application/caching#duration-3) of the client router cache.

This configuration option is available as of v14.2.0-canary.53.

You can enable this experimental feature & provide custom revalidation times by setting the experimental `staleTimes` flag:

next.config.js

```
/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    staleTimes: {
      dynamic: 30,
      static: 180,
    },
  },
}
 
module.exports = nextConfig
```

The `static` and `dynamic` properties correspond with the time period (in seconds) based on different types of [link prefetching](/docs/14/app/api-reference/components/link#prefetch).

- The `dynamic` property is used when the page is neither statically generated nor fully prefetched (i.e., with prefetch=).
  
  - Default: 0 seconds (not cached)
- The `static` property is used for statically generated pages, or when the `prefetch` prop on `Link` is set to `true`, or when calling [`router.prefetch`](/docs/14/app/building-your-application/caching#routerprefetch).
  
  - Default: 5 minutes

> **Good to know:**
> 
> - [Loading boundaries](/docs/14/app/api-reference/file-conventions/loading) are considered reusable for the `static` period defined in this configuration.
> - This doesn't affect [partial rendering](/docs/14/app/building-your-application/routing/linking-and-navigating#4-partial-rendering), **meaning shared layouts won't automatically be refetched on every navigation, only the page segment that changes.**
> - This doesn't change [back/forward caching](/docs/14/app/building-your-application/caching#client-side-router-cache) behavior to prevent layout shift and to prevent losing the browser scroll position.

You can learn more about the Client Router Cache [here](/docs/14/app/building-your-application/caching#client-side-router-cache).

### [Version History](#version-history)

VersionChanges`v14.2.0`experimental `staleTimes` introduced

Was this helpful?

supported.

Send
