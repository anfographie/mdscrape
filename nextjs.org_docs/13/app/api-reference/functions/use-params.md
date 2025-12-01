---
title: "useParams"
source: "https://nextjs.org/docs/13/app/api-reference/functions/use-params"
---

# useParams

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[Functions](/docs/13/app/api-reference/functions)useParams

You are currently viewing documentation for version 13 of Next.js.

# useParams

`useParams` is a **Client Component** hook that lets you read a route's [dynamic params](/docs/13/app/building-your-application/routing/dynamic-routes) filled in by the current URL.

app/example-client-component.tsx

TypeScript

JavaScriptTypeScript

```
'use client'
 
import { useParams } from 'next/navigation'
 
export default function ExampleClientComponent() {
  const params = useParams()
 
  // Route -> /shop/[tag]/[item]
  // URL -> /shop/shoes/nike-air-max-97
  // `params` -> { tag: 'shoes', item: 'nike-air-max-97' }
  console.log(params)
 
  return <></>
}
```

## [Parameters](#parameters)

```
const params = useParams()
```

`useParams` does not take any parameters.

## [Returns](#returns)

`useParams` returns an object containing the current route's filled in [dynamic parameters](/docs/13/app/building-your-application/routing/dynamic-routes).

- Each property in the object is an active dynamic segment.
- The properties name is the segment's name, and the properties value is what the segment is filled in with.
- The properties value will either be a `string` or array of `string`'s depending on the [type of dynamic segment](/docs/13/app/building-your-application/routing/dynamic-routes).
- If the route contains no dynamic parameters, `useParams` returns an empty object.
- If used in `pages`, `useParams` will return `null`.

For example:

RouteURL`useParams()``app/shop/page.js``/shop``null``app/shop/[slug]/page.js``/shop/1``{ slug: '1' }``app/shop/[tag]/[item]/page.js``/shop/1/2``{ tag: '1', item: '2' }``app/shop/[...slug]/page.js``/shop/1/2``{ slug: ['1', '2'] }`

## [Version History](#version-history)

VersionChanges`v13.3.0``useParams` introduced.

Was this helpful?

supported.

Send
