---
title: "incrementalCacheHandlerPath"
source: "https://nextjs.org/docs/13/app/api-reference/next-config-js/incrementalCacheHandlerPath"
---

# incrementalCacheHandlerPath

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[next.config.js Options](/docs/13/app/api-reference/next-config-js)incrementalCacheHandlerPath

You are currently viewing documentation for version 13 of Next.js.

# incrementalCacheHandlerPath

In Next.js, the [default cache handler](/docs/13/app/building-your-application/data-fetching/fetching-caching-and-revalidating) uses the filesystem cache. This requires no configuration, however, you can customize the cache handler by using the `incrementalCacheHandlerPath` field in `next.config.js`.

next.config.js

```
module.exports = {
  experimental: {
    incrementalCacheHandlerPath: require.resolve('./cache-handler.js'),
  },
}
```

Here's an example of a custom cache handler:

cache-handler.js

```
const cache = new Map()
 
module.exports = class CacheHandler {
  constructor(options) {
    this.options = options
    this.cache = {}
  }
 
  async get(key) {
    return cache.get(key)
  }
 
  async set(key, data) {
    cache.set(key, {
      value: data,
      lastModified: Date.now(),
    })
  }
}
```

## [API Reference](#api-reference)

The cache handler can implement the following methods: `get`, `set`, and `revalidateTag`.

### [`get()`](#get)

ParameterTypeDescription`key``string`The key to the cached value.

Returns the cached value or `null` if not found.

### [`set()`](#set)

ParameterTypeDescription`key``string`The key to store the data under.`data`Data or `null`The data to be cached.

Returns `Promise<void>`.

### [`revalidateTag()`](#revalidatetag)

ParameterTypeDescription`tag``string`The cache tag to revalidate.

Returns `Promise<void>`. Learn more about [revalidating data](/docs/13/app/building-your-application/data-fetching/fetching-caching-and-revalidating) or the [`revalidateTag()`](/docs/13/app/api-reference/functions/revalidateTag) function.

Was this helpful?

supported.

Send
