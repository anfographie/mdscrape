---
title: "cookies"
source: "https://nextjs.org/docs/13/app/api-reference/functions/cookies"
---

# cookies

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[Functions](/docs/13/app/api-reference/functions)cookies

You are currently viewing documentation for version 13 of Next.js.

# cookies

The `cookies` function allows you to read the HTTP incoming request cookies from a [Server Component](/docs/13/app/building-your-application/rendering/server-components) or write outgoing request cookies in a [Server Action](/docs/13/app/building-your-application/data-fetching/forms-and-mutations) or [Route Handler](/docs/13/app/building-your-application/routing/route-handlers).

> **Good to know**: `cookies()` is a [**Dynamic Function**](/docs/13/app/building-your-application/rendering/server-components#server-rendering-strategies%23dynamic-functions) whose returned values cannot be known ahead of time. Using it in a layout or page will opt a route into [**dynamic rendering**](/docs/13/app/building-your-application/rendering/server-components#dynamic-rendering) at request time.

## [`cookies().get(name)`](#cookiesgetname)

A method that takes a cookie name and returns an object with name and value. If a cookie with `name` isn't found, it returns `undefined`. If multiple cookies match, it will only return the first match.

app/page.js

```
import { cookies } from 'next/headers'
 
export default function Page() {
  const cookieStore = cookies()
  const theme = cookieStore.get('theme')
  return '...'
}
```

## [`cookies().getAll()`](#cookiesgetall)

A method that is similar to `get`, but returns a list of all the cookies with a matching `name`. If `name` is unspecified, it returns all the available cookies.

app/page.js

```
import { cookies } from 'next/headers'
 
export default function Page() {
  const cookieStore = cookies()
  return cookieStore.getAll().map((cookie) => (
    <div key={cookie.name}>
      <p>Name: {cookie.name}</p>
      <p>Value: {cookie.value}</p>
    </div>
  ))
}
```

## [`cookies().has(name)`](#cookieshasname)

A method that takes a cookie name and returns a `boolean` based on if the cookie exists (`true`) or not (`false`).

app/page.js

```
import { cookies } from 'next/headers'
 
export default function Page() {
  const cookiesList = cookies()
  const hasCookie = cookiesList.has('theme')
  return '...'
}
```

## [`cookies().set(name, value, options)`](#cookiessetname-value-options)

A method that takes a cookie name, value, and options and sets the outgoing request cookie.

> **Good to know**: HTTP does not allow setting cookies after streaming starts, so you must use `.set()` in a [Server Action](/docs/13/app/building-your-application/data-fetching/forms-and-mutations) or [Route Handler](/docs/13/app/building-your-application/routing/route-handlers).

app/actions.js

```
'use server'
 
import { cookies } from 'next/headers'
 
async function create(data) {
  cookies().set('name', 'lee')
  // or
  cookies().set('name', 'lee', { secure: true })
  // or
  cookies().set({
    name: 'name',
    value: 'lee',
    httpOnly: true,
    path: '/',
  })
}
```

## [Deleting cookies](#deleting-cookies)

> **Good to know**: You can only delete cookies in a [Server Action](/docs/13/app/building-your-application/data-fetching/forms-and-mutations) or [Route Handler](/docs/13/app/building-your-application/routing/route-handlers).

There are several options for deleting a cookie:

### [`cookies().delete(name)`](#cookiesdeletename)

You can explicitly delete a cookie with a given name.

app/actions.js

```
'use server'
 
import { cookies } from 'next/headers'
 
async function create(data) {
  cookies().delete('name')
}
```

### [`cookies().set(name, '')`](#cookiessetname-)

Alternatively, you can set a new cookie with the same name and an empty value.

app/actions.js

```
'use server'
 
import { cookies } from 'next/headers'
 
async function create(data) {
  cookies().set('name', '')
}
```

> **Good to know**: `.set()` is only available in a [Server Action](/docs/13/app/building-your-application/data-fetching/forms-and-mutations) or [Route Handler](/docs/13/app/building-your-application/routing/route-handlers).

### [`cookies().set(name, value, { maxAge: 0 })`](#cookiessetname-value--maxage-0-)

Setting `maxAge` to 0 will immediately expire a cookie.

app/actions.js

```
'use server'
 
import { cookies } from 'next/headers'
 
async function create(data) {
  cookies().set('name', 'value', { maxAge: 0 })
}
```

### [`cookies().set(name, value, { expires: timestamp })`](#cookiessetname-value--expires-timestamp-)

Setting `expires` to any value in the past will immediately expire a cookie.

app/actions.js

```
'use server'
 
import { cookies } from 'next/headers'
 
async function create(data) {
  const oneDay = 24 * 60 * 60 * 1000
  cookies().set('name', 'value', { expires: Date.now() - oneDay })
}
```

> **Good to know**: You can only delete cookies that belong to the same domain from which `.set()` is called. Additionally, the code must be executed on the same protocol (HTTP or HTTPS) as the cookie you want to delete.

## [Version History](#version-history)

VersionChanges`v13.0.0``cookies` introduced.

## Next Steps

For more information on what to do next, we recommend the following sections

[Introduction  
\
...  
\
Data Fetching  
\
**Forms and Mutations**  
\
Learn how to handle form submissions and data mutations with Next.js.](/docs/13/app/building-your-application/data-fetching/forms-and-mutations)

Was this helpful?

supported.

Send
