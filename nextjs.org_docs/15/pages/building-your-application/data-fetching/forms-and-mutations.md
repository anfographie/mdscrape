---
title: "Forms and Mutations"
source: "https://nextjs.org/docs/15/pages/building-your-application/data-fetching/forms-and-mutations"
---

# Forms and Mutations

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Building Your Application](/docs/15/pages/building-your-application)[Data Fetching](/docs/15/pages/building-your-application/data-fetching)Forms and Mutations

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# Forms and Mutations

Forms enable you to create and update data in web applications. Next.js provides a powerful way to handle form submissions and data mutations using **API Routes**.

> **Good to know:**
> 
> - We will soon recommend [incrementally adopting](/docs/15/app/guides/migrating/app-router-migration) the App Router and using [Server Actions](/docs/15/app/getting-started/updating-data) for handling form submissions and data mutations. Server Actions allow you to define asynchronous server functions that can be called directly from your components, without needing to manually create an API Route.
> - API Routes [do not specify CORS headers](https://developer.mozilla.org/docs/Web/HTTP/CORS), meaning they are same-origin only by default.
> - Since API Routes run on the server, we're able to use sensitive values (like API keys) through [Environment Variables](/docs/15/pages/guides/environment-variables) without exposing them to the client. This is critical for the security of your application.

## [Examples](#examples)

### [Redirecting](#redirecting)

If you would like to redirect the user to a different route after a mutation, you can [`redirect`](/docs/15/pages/building-your-application/routing/api-routes#response-helpers) to any absolute or relative URL:

pages/api/submit.ts

TypeScript

JavaScriptTypeScript

```
import type { NextApiRequest, NextApiResponse } from 'next'
 
export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  const id = await addPost()
  res.redirect(307, `/post/${id}`)
}
```

### [Setting cookies](#setting-cookies)

You can set cookies inside an API Route using the `setHeader` method on the response:

pages/api/cookie.ts

TypeScript

JavaScriptTypeScript

```
import type { NextApiRequest, NextApiResponse } from 'next'
 
export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  res.setHeader('Set-Cookie', 'username=lee; Path=/; HttpOnly')
  res.status(200).send('Cookie has been set.')
}
```

### [Reading cookies](#reading-cookies)

You can read cookies inside an API Route using the [`cookies`](/docs/15/pages/building-your-application/routing/api-routes#request-helpers) request helper:

pages/api/cookie.ts

TypeScript

JavaScriptTypeScript

```
import type { NextApiRequest, NextApiResponse } from 'next'
 
export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  const auth = req.cookies.authorization
  // ...
}
```

### [Deleting cookies](#deleting-cookies)

You can delete cookies inside an API Route using the `setHeader` method on the response:

pages/api/cookie.ts

TypeScript

JavaScriptTypeScript

```
import type { NextApiRequest, NextApiResponse } from 'next'
 
export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  res.setHeader('Set-Cookie', 'username=; Path=/; HttpOnly; Max-Age=0')
  res.status(200).send('Cookie has been deleted.')
}
```

Was this helpful?

supported.

Send
