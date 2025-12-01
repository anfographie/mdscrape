---
title: "permanentRedirect"
source: "https://nextjs.org/docs/13/app/api-reference/functions/permanentRedirect"
---

# permanentRedirect

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[Functions](/docs/13/app/api-reference/functions)permanentRedirect

You are currently viewing documentation for version 13 of Next.js.

# permanentRedirect

The `permanentRedirect` function allows you to redirect the user to another URL. `permanentRedirect` can be used in Server Components, Client Components, [Route Handlers](/docs/13/app/building-your-application/routing/route-handlers), and [Server Actions](/docs/13/app/building-your-application/data-fetching/forms-and-mutations).

When used in a streaming context, this will insert a meta tag to emit the redirect on the client side. Otherwise, it will serve a 308 (Permanent) HTTP redirect response to the caller.

If a resource doesn't exist, you can use the [`notFound` function](/docs/13/app/api-reference/functions/not-found) instead.

> **Good to know**: If you prefer to return a 307 (Temporary) HTTP redirect instead of 308 (Permanent), you can use the [`redirect` function](/docs/13/app/api-reference/functions/redirect) instead.

## [Parameters](#parameters)

The `permanentRedirect` function accepts two arguments:

```
permanentRedirect(path, type)
```

ParameterTypeDescription`path``string`The URL to redirect to. Can be a relative or absolute path.`type``'replace'` (default) or `'push'` (default in Server Actions)The type of redirect to perform.

By default, `permanentRedirect` will use `push` (adding a new entry to the browser history stack) in [Server Actions](/docs/13/app/building-your-application/data-fetching/forms-and-mutations) and `replace` (replacing the current URL in the browser history stack) everywhere else. You can override this behavior by specifying the `type` parameter.

The `type` parameter has no effect when used in Server Components.

## [Returns](#returns)

`permanentRedirect` does not return any value.

## [Example](#example)

Invoking the `permanentRedirect()` function throws a `NEXT_REDIRECT` error and terminates rendering of the route segment in which it was thrown.

app/team/\[id]/page.js

```
import { permanentRedirect } from 'next/navigation'
 
async function fetchTeam(id) {
  const res = await fetch('https://...')
  if (!res.ok) return undefined
  return res.json()
}
 
export default async function Profile({ params }) {
  const team = await fetchTeam(params.id)
  if (!team) {
    permanentRedirect('/login')
  }
 
  // ...
}
```

> **Good to know**: `permanentRedirect` does not require you to use `return permanentRedirect()` as it uses the TypeScript [`never`](https://www.typescriptlang.org/docs/handbook/2/functions.html#never) type.

Was this helpful?

supported.

Send
