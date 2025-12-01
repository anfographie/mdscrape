---
title: "Forms and Mutations"
source: "https://nextjs.org/docs/13/pages/building-your-application/data-fetching/forms-and-mutations"
---

# Forms and Mutations

Menu

Pages Router 13

Using Pages Router

Features available in /pages

Version 13

13.5.11

[Building Your Application](/docs/13/pages/building-your-application)[Data Fetching](/docs/13/pages/building-your-application/data-fetching)Forms and Mutations

You are currently viewing the Pages Router documentation for version 13 of Next.js.

# Forms and Mutations

Forms enable you to create and update data in web applications. Next.js provides a powerful way to handle form submissions and data mutations using **API Routes**.

> **Good to know:**
> 
> - We will soon recommend [incrementally adopting](/docs/13/app/building-your-application/upgrading/app-router-migration) the App Router and using [Server Actions](/docs/13/app/building-your-application/data-fetching/forms-and-mutations#how-server-actions-work) for handling form submissions and data mutations. Server Actions allow you to define asynchronous server functions that can be called directly from your components, without needing to manually create an API Route.
> - API Routes [do not specify CORS headers](https://developer.mozilla.org/docs/Web/HTTP/CORS), meaning they are same-origin only by default.
> - Since API Routes run on the server, we're able to use sensitive values (like API keys) through [Environment Variables](/docs/13/pages/building-your-application/configuring/environment-variables) without exposing them to the client. This is critical for the security of your application.

## [Examples](#examples)

### [Server-only Forms](#server-only-forms)

With the Pages Router, you need to manually create API endpoints to handle securely mutating data on the server.

pages/api/submit.ts

TypeScript

JavaScriptTypeScript

```
import type { NextApiRequest, NextApiResponse } from 'next'
 
export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  const data = req.body
  const id = await createItem(data)
  res.status(200).json({ id })
}
```

Then, call the API Route from the client with an event handler:

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
import { FormEvent } from 'react'
 
export default function Page() {
  async function onSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault()
 
    const formData = new FormData(event.currentTarget)
    const response = await fetch('/api/submit', {
      method: 'POST',
      body: formData,
    })
 
    // Handle response if necessary
    const data = await response.json()
    // ...
  }
 
  return (
    <form onSubmit={onSubmit}>
      <input type="text" name="name" />
      <button type="submit">Submit</button>
    </form>
  )
}
```

### [Redirecting](#redirecting)

If you would like to redirect the user to a different route after a mutation, you can [`redirect`](/docs/13/pages/building-your-application/routing/api-routes#response-helpers) to any absolute or relative URL:

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

### [Form Validation](#form-validation)

We recommend using HTML validation like `required` and `type="email"` for basic form validation.

For more advanced server-side validation, use a schema validation library like [zod](https://zod.dev/) to validate the structure of the parsed form data:

pages/api/submit.ts

TypeScript

JavaScriptTypeScript

```
import type { NextApiRequest, NextApiResponse } from 'next'
import { z } from 'zod'
 
const schema = z.object({
  // ...
})
 
export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  const parsed = schema.parse(req.body)
  // ...
}
```

### [Displaying Loading State](#displaying-loading-state)

You can use React state to show a loading state when a form is submitting on the server:

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
import React, { useState, FormEvent } from 'react'
 
export default function Page() {
  const [isLoading, setIsLoading] = useState<boolean>(false)
 
  async function onSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault()
    setIsLoading(true) // Set loading to true when the request starts
 
    try {
      const formData = new FormData(event.currentTarget)
      const response = await fetch('/api/submit', {
        method: 'POST',
        body: formData,
      })
 
      // Handle response if necessary
      const data = await response.json()
      // ...
    } catch (error) {
      // Handle error if necessary
      console.error(error)
    } finally {
      setIsLoading(false) // Set loading to false when the request completes
    }
  }
 
  return (
    <form onSubmit={onSubmit}>
      <input type="text" name="name" />
      <button type="submit" disabled={isLoading}>
        {isLoading ? 'Loading...' : 'Submit'}
      </button>
    </form>
  )
}
```

### [Error Handling](#error-handling)

You can use React state to show an error message when a form submission fails:

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
import React, { useState, FormEvent } from 'react'
 
export default function Page() {
  const [isLoading, setIsLoading] = useState<boolean>(false)
  const [error, setError] = useState<string | null>(null)
 
  async function onSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault()
    setIsLoading(true)
    setError(null) // Clear previous errors when a new request starts
 
    try {
      const formData = new FormData(event.currentTarget)
      const response = await fetch('/api/submit', {
        method: 'POST',
        body: formData,
      })
 
      if (!response.ok) {
        throw new Error('Failed to submit the data. Please try again.')
      }
 
      // Handle response if necessary
      const data = await response.json()
      // ...
    } catch (error) {
      // Capture the error message to display to the user
      setError(error.message)
      console.error(error)
    } finally {
      setIsLoading(false)
    }
  }
 
  return (
    <div>
      {error && <div style={{ color: 'red' }}>{error}</div>}
      <form onSubmit={onSubmit}>
        <input type="text" name="name" />
        <button type="submit" disabled={isLoading}>
          {isLoading ? 'Loading...' : 'Submit'}
        </button>
      </form>
    </div>
  )
}
```

### [Setting Cookies](#setting-cookies)

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

### [Reading Cookies](#reading-cookies)

You can read cookies inside an API Route using the [`cookies`](/docs/13/pages/building-your-application/routing/api-routes#request-helpers) request helper:

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

### [Deleting Cookies](#deleting-cookies)

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
