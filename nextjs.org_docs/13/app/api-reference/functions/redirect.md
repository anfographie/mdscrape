---
title: "redirect"
source: "https://nextjs.org/docs/13/app/api-reference/functions/redirect"
---

# redirect

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[Functions](/docs/13/app/api-reference/functions)redirect

You are currently viewing documentation for version 13 of Next.js.

# redirect

The `redirect` function allows you to redirect the user to another URL. `redirect` can be used in Server Components, Client Components, [Route Handlers](/docs/13/app/building-your-application/routing/route-handlers), and [Server Actions](/docs/13/app/building-your-application/data-fetching/forms-and-mutations).

When used in a [streaming context](/docs/13/app/building-your-application/routing/loading-ui-and-streaming#what-is-streaming), this will insert a meta tag to emit the redirect on the client side. Otherwise, it will serve a 307 HTTP redirect response to the caller.

If a resource doesn't exist, you can use the [`notFound` function](/docs/13/app/api-reference/functions/not-found) instead.

> **Good to know**: If you prefer to return a 308 (Permanent) HTTP redirect instead of 307 (Temporary), you can use the [`permanentRedirect` function](/docs/13/app/api-reference/functions/permanentRedirect) instead.

## [Parameters](#parameters)

The `redirect` function accepts two arguments:

```
redirect(path, type)
```

ParameterTypeDescription`path``string`The URL to redirect to. Can be a relative or absolute path.`type``'replace'` (default) or `'push'` (default in Server Actions)The type of redirect to perform.

By default, `redirect` will use `push` (adding a new entry to the browser history stack) in [Server Actions](/docs/13/app/building-your-application/data-fetching/forms-and-mutations) and `replace` (replacing the current URL in the browser history stack) everywhere else. You can override this behavior by specifying the `type` parameter.

The `type` parameter has no effect when used in Server Components.

## [Returns](#returns)

`redirect` does not return any value.

## [Example](#example)

Invoking the `redirect()` function throws a `NEXT_REDIRECT` error and terminates rendering of the route segment in which it was thrown.

app/team/\[id]/page.js

```
import { redirect } from 'next/navigation'
 
async function fetchTeam(id) {
  const res = await fetch('https://...')
  if (!res.ok) return undefined
  return res.json()
}
 
export default async function Profile({ params }) {
  const team = await fetchTeam(params.id)
  if (!team) {
    redirect('/login')
  }
 
  // ...
}
```

> **Good to know**: `redirect` does not require you to use `return redirect()` as it uses the TypeScript [`never`](https://www.typescriptlang.org/docs/handbook/2/functions.html#never) type.

VersionChanges`v13.0.0``redirect` introduced.

Was this helpful?

supported.

Send
