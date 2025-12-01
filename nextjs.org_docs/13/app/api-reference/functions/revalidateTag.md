---
title: "revalidateTag"
source: "https://nextjs.org/docs/13/app/api-reference/functions/revalidateTag"
---

# revalidateTag

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[Functions](/docs/13/app/api-reference/functions)revalidateTag

You are currently viewing documentation for version 13 of Next.js.

# revalidateTag

`revalidateTag` allows you to purge [cached data](/docs/13/app/building-your-application/caching) on-demand for a specific cache tag.

> **Good to know**:
> 
> - `revalidateTag` is available in both [Node.js and Edge runtimes](/docs/13/app/building-your-application/rendering/edge-and-nodejs-runtimes).
> - `revalidateTag` only invalidates the cache when the path is next visited. This means calling `revalidateTag` with a dynamic route segment will not immediately trigger many revalidations at once. The invalidation only happens when the path is next visited.

## [Parameters](#parameters)

```
revalidateTag(tag: string): void;
```

- `tag`: A string representing the cache tag associated with the data you want to revalidate. Must be less than or equal to 256 characters.

You can add tags to `fetch` as follows:

```
fetch(url, { next: { tags: [...] } });
```

## [Returns](#returns)

`revalidateTag` does not return any value.

## [Examples](#examples)

### [Server Action](#server-action)

app/actions.ts

TypeScript

JavaScriptTypeScript

```
'use server'
 
import { revalidateTag } from 'next/cache'
 
export default async function submit() {
  await addPost()
  revalidateTag('posts')
}
```

### [Route Handler](#route-handler)

app/api/revalidate/route.ts

TypeScript

JavaScriptTypeScript

```
import { NextRequest } from 'next/server'
import { revalidateTag } from 'next/cache'
 
export async function GET(request: NextRequest) {
  const tag = request.nextUrl.searchParams.get('tag')
  revalidateTag(tag)
  return Response.json({ revalidated: true, now: Date.now() })
}
```

Was this helpful?

supported.

Send
