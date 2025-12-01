---
title: "Custom Next.js Cache Handler"
source: "https://nextjs.org/docs/14/app/api-reference/next-config-js/incrementalCacheHandlerPath"
---

# Custom Next.js Cache Handler

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[next.config.js Options](/docs/14/app/api-reference/next-config-js)cacheHandler

You are currently viewing documentation for version 14 of Next.js.

# Custom Next.js Cache Handler

In Next.js, the [default cache handler](/docs/14/app/building-your-application/data-fetching/fetching-caching-and-revalidating) for the Pages and App Router uses the filesystem cache. This requires no configuration, however, you can customize the cache handler by using the `cacheHandler` field in `next.config.js`.

next.config.js

```
module.exports = {
  cacheHandler: require.resolve('./cache-handler.js'),
  cacheMaxMemorySize: 0, // disable default in-memory caching
}
```

View an example of a [custom cache handler](/docs/14/app/building-your-application/deploying#configuring-caching) and learn more about implementation.

## [API Reference](#api-reference)

The cache handler can implement the following methods: `get`, `set`, and `revalidateTag`.

### [`get()`](#get)

ParameterTypeDescription`key``string`The key to the cached value.

Returns the cached value or `null` if not found.

### [`set()`](#set)

ParameterTypeDescription`key``string`The key to store the data under.`data`Data or `null`The data to be cached.`ctx``{ tags: [] }`The cache tags provided.

Returns `Promise<void>`.

### [`revalidateTag()`](#revalidatetag)

ParameterTypeDescription`tag``string`The cache tag to revalidate.

Returns `Promise<void>`. Learn more about [revalidating data](/docs/14/app/building-your-application/data-fetching/fetching-caching-and-revalidating) or the [`revalidateTag()`](/docs/14/app/api-reference/functions/revalidateTag) function.

**Good to know:**

- `revalidatePath` is a convenience layer on top of cache tags. Calling `revalidatePath` will call your `revalidateTag` function, which you can then choose if you want to tag cache keys based on the path.

## [Version History](#version-history)

VersionChanges`v14.1.0`Renamed `cacheHandler` is stable.`v13.4.0``incrementalCacheHandlerPath` (experimental) supports `revalidateTag`.`v13.4.0``incrementalCacheHandlerPath` (experimental) supports standalone output.`v12.2.0``incrementalCacheHandlerPath` (experimental) is added.

Was this helpful?

supported.

Send
