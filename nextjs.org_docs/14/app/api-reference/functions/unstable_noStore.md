---
title: "unstable_noStore"
source: "https://nextjs.org/docs/14/app/api-reference/functions/unstable_noStore"
---

# unstable_noStore

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[Functions](/docs/14/app/api-reference/functions)unstable\_noStore

You are currently viewing documentation for version 14 of Next.js.

# unstable\_noStore

`unstable_noStore` can be used to declaratively opt out of static rendering and indicate a particular component should not be cached.

```
import { unstable_noStore as noStore } from 'next/cache';
 
export default async function Component() {
  noStore();
  const result = await db.query(...);
  ...
}
```

> **Good to know**:
> 
> - `unstable_noStore` is equivalent to `cache: 'no-store'` on a `fetch`
> - `unstable_noStore` is preferred over `export const dynamic = 'force-dynamic'` as it is more granular and can be used on a per-component basis
> 
> <!--THE END-->

- Using `unstable_noStore` inside [`unstable_cache`](/docs/14/app/api-reference/functions/unstable_cache) will not opt out of static generation. Instead, it will defer to the cache configuration to determine whether to cache the result or not.

## [Usage](#usage)

If you prefer not to pass additional options to `fetch`, like `cache: 'no-store'` or `next: { revalidate: 0 }`, you can use `noStore()` as a replacement for all of these use cases.

```
import { unstable_noStore as noStore } from 'next/cache';
 
export default async function Component() {
  noStore();
  const result = await db.query(...);
  ...
}
```

## [Version History](#version-history)

VersionChanges`v14.0.0``unstable_noStore` introduced.

Was this helpful?

supported.

Send
