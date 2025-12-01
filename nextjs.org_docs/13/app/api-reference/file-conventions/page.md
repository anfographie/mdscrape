---
title: "page.js"
source: "https://nextjs.org/docs/13/app/api-reference/file-conventions/page"
---

# page.js

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[File Conventions](/docs/13/app/api-reference/file-conventions)page.js

You are currently viewing documentation for version 13 of Next.js.

# page.js

A **page** is UI that is unique to a route.

app/blog/\[slug]/page.tsx

TypeScript

JavaScriptTypeScript

```
export default function Page({
  params,
  searchParams,
}: {
  params: { slug: string }
  searchParams: { [key: string]: string | string[] | undefined }
}) {
  return <h1>My Page</h1>
}
```

## [Props](#props)

### [`params` (optional)](#params-optional)

An object containing the [dynamic route parameters](/docs/13/app/building-your-application/routing/dynamic-routes) from the root segment down to that page. For example:

ExampleURL`params``app/shop/[slug]/page.js``/shop/1``{ slug: '1' }``app/shop/[category]/[item]/page.js``/shop/1/2``{ category: '1', item: '2' }``app/shop/[...slug]/page.js``/shop/1/2``{ slug: ['1', '2'] }`

### [`searchParams` (optional)](#searchparams-optional)

An object containing the [search parameters](https://developer.mozilla.org/docs/Learn/Common_questions/What_is_a_URL#parameters) of the current URL. For example:

URL`searchParams``/shop?a=1``{ a: '1' }``/shop?a=1&b=2``{ a: '1', b: '2' }``/shop?a=1&a=2``{ a: ['1', '2'] }`

> **Good to know**:
> 
> - `searchParams` is a [**Dynamic API**](/docs/13/app/building-your-application/rendering/server-components#server-rendering-strategies%23dynamic-functions) whose values cannot be known ahead of time. Using it will opt the page into [**dynamic rendering**](/docs/13/app/building-your-application/rendering/server-components#dynamic-rendering) at request time.
> - `searchParams` returns a plain JavaScript object and not a `URLSearchParams` instance.

## [Version History](#version-history)

VersionChanges`v13.0.0``page` introduced.

Was this helpful?

supported.

Send
