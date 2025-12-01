---
title: "Route Handlers"
source: "https://nextjs.org/docs/14/app/building-your-application/routing/route-handlers"
---

# Route Handlers

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[Building Your Application](/docs/14/app/building-your-application)[Routing](/docs/14/app/building-your-application/routing)Route Handlers

You are currently viewing documentation for version 14 of Next.js.

# Route Handlers

Route Handlers allow you to create custom request handlers for a given route using the Web [Request](https://developer.mozilla.org/docs/Web/API/Request) and [Response](https://developer.mozilla.org/docs/Web/API/Response) APIs.

![Route.js Special File](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Froute-special-file.png&w=3840&q=75)![Route.js Special File](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Froute-special-file.png&w=3840&q=75)

> **Good to know**: Route Handlers are only available inside the `app` directory. They are the equivalent of [API Routes](/docs/14/pages/building-your-application/routing/api-routes) inside the `pages` directory meaning you **do not** need to use API Routes and Route Handlers together.

## [Convention](#convention)

Route Handlers are defined in a [`route.js|ts` file](/docs/14/app/api-reference/file-conventions/route) inside the `app` directory:

app/api/route.ts

TypeScript

JavaScriptTypeScript

```
export const dynamic = 'force-dynamic' // defaults to auto
export async function GET(request: Request) {}
```

Route Handlers can be nested inside the `app` directory, similar to `page.js` and `layout.js`. But there **cannot** be a `route.js` file at the same route segment level as `page.js`.

### [Supported HTTP Methods](#supported-http-methods)

The following [HTTP methods](https://developer.mozilla.org/docs/Web/HTTP/Methods) are supported: `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD`, and `OPTIONS`. If an unsupported method is called, Next.js will return a `405 Method Not Allowed` response.

### [Extended `NextRequest` and `NextResponse` APIs](#extended-nextrequest-and-nextresponse-apis)

In addition to supporting native [Request](https://developer.mozilla.org/docs/Web/API/Request) and [Response](https://developer.mozilla.org/docs/Web/API/Response). Next.js extends them with [`NextRequest`](/docs/14/app/api-reference/functions/next-request) and [`NextResponse`](/docs/14/app/api-reference/functions/next-response) to provide convenient helpers for advanced use cases.

## [Behavior](#behavior)

### [Caching](#caching)

Route Handlers are cached by default when using the `GET` method with the `Response` object.

app/items/route.ts

TypeScript

JavaScriptTypeScript

```
export async function GET() {
  const res = await fetch('https://data.mongodb-api.com/...', {
    headers: {
      'Content-Type': 'application/json',
      'API-Key': process.env.DATA_API_KEY,
    },
  })
  const data = await res.json()
 
  return Response.json({ data })
}
```

> **TypeScript Warning:** `Response.json()` is only valid from TypeScript 5.2. If you use a lower TypeScript version, you can use [`NextResponse.json()`](/docs/14/app/api-reference/functions/next-response#json) for typed responses instead.

### [Opting out of caching](#opting-out-of-caching)

You can opt out of caching by:

- Using the `Request` object with the `GET` method.
- Using any of the other HTTP methods.
- Using [Dynamic Functions](#dynamic-functions) like `cookies` and `headers`.
- The [Segment Config Options](#segment-config-options) manually specifies dynamic mode.

For example:

app/products/api/route.ts

TypeScript

JavaScriptTypeScript

```
export async function GET(request: Request) {
  const { searchParams } = new URL(request.url)
  const id = searchParams.get('id')
  const res = await fetch(`https://data.mongodb-api.com/product/${id}`, {
    headers: {
      'Content-Type': 'application/json',
      'API-Key': process.env.DATA_API_KEY!,
    },
  })
  const product = await res.json()
 
  return Response.json({ product })
}
```

Similarly, the `POST` method will cause the Route Handler to be evaluated dynamically.

app/items/route.ts

TypeScript

JavaScriptTypeScript

```
export async function POST() {
  const res = await fetch('https://data.mongodb-api.com/...', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'API-Key': process.env.DATA_API_KEY!,
    },
    body: JSON.stringify({ time: new Date().toISOString() }),
  })
 
  const data = await res.json()
 
  return Response.json(data)
}
```

> **Good to know**: Like API Routes, Route Handlers can be used for cases like handling form submissions. A new abstraction for [handling forms and mutations](/docs/14/app/building-your-application/data-fetching/server-actions-and-mutations) that integrates deeply with React is being worked on.

### [Route Resolution](#route-resolution)

You can consider a `route` the lowest level routing primitive.

- They **do not** participate in layouts or client-side navigations like `page`.
- There **cannot** be a `route.js` file at the same route as `page.js`.

PageRouteResult`app/page.js``app/route.js` Conflict`app/page.js``app/api/route.js` Valid`app/[user]/page.js``app/api/route.js` Valid

Each `route.js` or `page.js` file takes over all HTTP verbs for that route.

app/page.js

```
export default function Page() {
  return <h1>Hello, Next.js!</h1>
}
 
// ❌ Conflict
// `app/route.js`
export async function POST(request) {}
```

## [Examples](#examples)

The following examples show how to combine Route Handlers with other Next.js APIs and features.

### [Revalidating Cached Data](#revalidating-cached-data)

You can [revalidate cached data](/docs/14/app/building-your-application/data-fetching/fetching-caching-and-revalidating#revalidating-data) using the [`next.revalidate`](/docs/14/app/building-your-application/data-fetching/fetching-caching-and-revalidating#revalidating-data) option:

app/items/route.ts

TypeScript

JavaScriptTypeScript

```
export async function GET() {
  const res = await fetch('https://data.mongodb-api.com/...', {
    next: { revalidate: 60 }, // Revalidate every 60 seconds
  })
  const data = await res.json()
 
  return Response.json(data)
}
```

Alternatively, you can use the [`revalidate` segment config option](/docs/14/app/api-reference/file-conventions/route-segment-config#revalidate):

```
export const revalidate = 60
```

### [Dynamic Functions](#dynamic-functions)

Route Handlers can be used with dynamic functions from Next.js, like [`cookies`](/docs/14/app/api-reference/functions/cookies) and [`headers`](/docs/14/app/api-reference/functions/headers).

#### [Cookies](#cookies)

You can read or set cookies with [`cookies`](/docs/14/app/api-reference/functions/cookies) from `next/headers`. This server function can be called directly in a Route Handler, or nested inside of another function.

Alternatively, you can return a new `Response` using the [`Set-Cookie`](https://developer.mozilla.org/docs/Web/HTTP/Headers/Set-Cookie) header.

app/api/route.ts

TypeScript

JavaScriptTypeScript

```
import { cookies } from 'next/headers'
 
export async function GET(request: Request) {
  const cookieStore = cookies()
  const token = cookieStore.get('token')
 
  return new Response('Hello, Next.js!', {
    status: 200,
    headers: { 'Set-Cookie': `token=${token.value}` },
  })
}
```

You can also use the underlying Web APIs to read cookies from the request ([`NextRequest`](/docs/14/app/api-reference/functions/next-request)):

app/api/route.ts

TypeScript

JavaScriptTypeScript

```
import { type NextRequest } from 'next/server'
 
export async function GET(request: NextRequest) {
  const token = request.cookies.get('token')
}
```

#### [Headers](#headers)

You can read headers with [`headers`](/docs/14/app/api-reference/functions/headers) from `next/headers`. This server function can be called directly in a Route Handler, or nested inside of another function.

This `headers` instance is read-only. To set headers, you need to return a new `Response` with new `headers`.

app/api/route.ts

TypeScript

JavaScriptTypeScript

```
import { headers } from 'next/headers'
 
export async function GET(request: Request) {
  const headersList = headers()
  const referer = headersList.get('referer')
 
  return new Response('Hello, Next.js!', {
    status: 200,
    headers: { referer: referer },
  })
}
```

You can also use the underlying Web APIs to read headers from the request ([`NextRequest`](/docs/14/app/api-reference/functions/next-request)):

app/api/route.ts

TypeScript

JavaScriptTypeScript

```
import { type NextRequest } from 'next/server'
 
export async function GET(request: NextRequest) {
  const requestHeaders = new Headers(request.headers)
}
```

### [Redirects](#redirects)

app/api/route.ts

TypeScript

JavaScriptTypeScript

```
import { redirect } from 'next/navigation'
 
export async function GET(request: Request) {
  redirect('https://nextjs.org/')
}
```

### [Dynamic Route Segments](#dynamic-route-segments)

> We recommend reading the [Defining Routes](/docs/14/app/building-your-application/routing/defining-routes) page before continuing.

Route Handlers can use [Dynamic Segments](/docs/14/app/building-your-application/routing/dynamic-routes) to create request handlers from dynamic data.

app/items/\[slug]/route.ts

TypeScript

JavaScriptTypeScript

```
export async function GET(
  request: Request,
  { params }: { params: { slug: string } }
) {
  const slug = params.slug // 'a', 'b', or 'c'
}
```

RouteExample URL`params``app/items/[slug]/route.js``/items/a``{ slug: 'a' }``app/items/[slug]/route.js``/items/b``{ slug: 'b' }``app/items/[slug]/route.js``/items/c``{ slug: 'c' }`

### [URL Query Parameters](#url-query-parameters)

The request object passed to the Route Handler is a `NextRequest` instance, which has [some additional convenience methods](/docs/14/app/api-reference/functions/next-request#nexturl), including for more easily handling query parameters.

app/api/search/route.ts

TypeScript

JavaScriptTypeScript

```
import { type NextRequest } from 'next/server'
 
export function GET(request: NextRequest) {
  const searchParams = request.nextUrl.searchParams
  const query = searchParams.get('query')
  // query is "hello" for /api/search?query=hello
}
```

### [Streaming](#streaming)

Streaming is commonly used in combination with Large Language Models (LLMs), such as OpenAI, for AI-generated content. Learn more about the [AI SDK](https://sdk.vercel.ai/docs).

app/api/chat/route.ts

TypeScript

JavaScriptTypeScript

```
import OpenAI from 'openai'
import { OpenAIStream, StreamingTextResponse } from 'ai'
 
const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY,
})
 
export const runtime = 'edge'
 
export async function POST(req: Request) {
  const { messages } = await req.json()
  const response = await openai.chat.completions.create({
    model: 'gpt-3.5-turbo',
    stream: true,
    messages,
  })
 
  const stream = OpenAIStream(response)
 
  return new StreamingTextResponse(stream)
}
```

These abstractions use the Web APIs to create a stream. You can also use the underlying Web APIs directly.

app/api/route.ts

TypeScript

JavaScriptTypeScript

```
// https://developer.mozilla.org/docs/Web/API/ReadableStream#convert_async_iterator_to_stream
function iteratorToStream(iterator: any) {
  return new ReadableStream({
    async pull(controller) {
      const { value, done } = await iterator.next()
 
      if (done) {
        controller.close()
      } else {
        controller.enqueue(value)
      }
    },
  })
}
 
function sleep(time: number) {
  return new Promise((resolve) => {
    setTimeout(resolve, time)
  })
}
 
const encoder = new TextEncoder()
 
async function* makeIterator() {
  yield encoder.encode('<p>One</p>')
  await sleep(200)
  yield encoder.encode('<p>Two</p>')
  await sleep(200)
  yield encoder.encode('<p>Three</p>')
}
 
export async function GET() {
  const iterator = makeIterator()
  const stream = iteratorToStream(iterator)
 
  return new Response(stream)
}
```

### [Request Body](#request-body)

You can read the `Request` body using the standard Web API methods:

app/items/route.ts

TypeScript

JavaScriptTypeScript

```
export async function POST(request: Request) {
  const res = await request.json()
  return Response.json({ res })
}
```

### [Request Body FormData](#request-body-formdata)

You can read the `FormData` using the `request.formData()` function:

app/items/route.ts

TypeScript

JavaScriptTypeScript

```
export async function POST(request: Request) {
  const formData = await request.formData()
  const name = formData.get('name')
  const email = formData.get('email')
  return Response.json({ name, email })
}
```

Since `formData` data are all strings, you may want to use [`zod-form-data`](https://www.npmjs.com/zod-form-data) to validate the request and retrieve data in the format you prefer (e.g. `number`).

### [CORS](#cors)

You can set CORS headers for a specific Route Handler using the standard Web API methods:

app/api/route.ts

TypeScript

JavaScriptTypeScript

```
export const dynamic = 'force-dynamic' // defaults to auto
 
export async function GET(request: Request) {
  return new Response('Hello, Next.js!', {
    status: 200,
    headers: {
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
      'Access-Control-Allow-Headers': 'Content-Type, Authorization',
    },
  })
}
```

> **Good to know**:
> 
> - To add CORS headers to multiple Route Handlers, you can use [Middleware](/docs/14/app/building-your-application/routing/middleware#cors) or the [`next.config.js` file](/docs/14/app/api-reference/next-config-js/headers#cors).
> - Alternatively, see our [CORS example](https://github.com/vercel/examples/blob/main/edge-functions/cors/lib/cors.ts) package.

### [Webhooks](#webhooks)

You can use a Route Handler to receive webhooks from third-party services:

app/api/route.ts

TypeScript

JavaScriptTypeScript

```
export async function POST(request: Request) {
  try {
    const text = await request.text()
    // Process the webhook payload
  } catch (error) {
    return new Response(`Webhook error: ${error.message}`, {
      status: 400,
    })
  }
 
  return new Response('Success!', {
    status: 200,
  })
}
```

Notably, unlike API Routes with the Pages Router, you do not need to use `bodyParser` to use any additional configuration.

### [Edge and Node.js Runtimes](#edge-and-nodejs-runtimes)

Route Handlers have an isomorphic Web API to support both Edge and Node.js runtimes seamlessly, including support for streaming. Since Route Handlers use the same [route segment configuration](/docs/14/app/api-reference/file-conventions/route-segment-config) as Pages and Layouts, they support long-awaited features like general-purpose [statically regenerated](/docs/14/app/building-your-application/data-fetching/fetching-caching-and-revalidating#revalidating-data) Route Handlers.

You can use the `runtime` segment config option to specify the runtime:

```
export const runtime = 'edge' // 'nodejs' is the default
```

### [Non-UI Responses](#non-ui-responses)

You can use Route Handlers to return non-UI content. Note that [`sitemap.xml`](/docs/14/app/api-reference/file-conventions/metadata/sitemap#generating-a-sitemap-using-code-js-ts), [`robots.txt`](/docs/14/app/api-reference/file-conventions/metadata/robots#generate-a-robots-file), [`app icons`](/docs/14/app/api-reference/file-conventions/metadata/app-icons#generate-icons-using-code-js-ts-tsx), and [open graph images](/docs/14/app/api-reference/file-conventions/metadata/opengraph-image) all have built-in support.

app/rss.xml/route.ts

TypeScript

JavaScriptTypeScript

```
export const dynamic = 'force-dynamic' // defaults to auto
 
export async function GET() {
  return new Response(
    `<?xml version="1.0" encoding="UTF-8" ?>
<rss version="2.0">
 
<channel>
  <title>Next.js Documentation</title>
  <link>https://nextjs.org/docs</link>
  <description>The React Framework for the Web</description>
</channel>
 
</rss>`,
    {
      headers: {
        'Content-Type': 'text/xml',
      },
    }
  )
}
```

### [Segment Config Options](#segment-config-options)

Route Handlers use the same [route segment configuration](/docs/14/app/api-reference/file-conventions/route-segment-config) as pages and layouts.

app/items/route.ts

TypeScript

JavaScriptTypeScript

```
export const dynamic = 'auto'
export const dynamicParams = true
export const revalidate = false
export const fetchCache = 'auto'
export const runtime = 'nodejs'
export const preferredRegion = 'auto'
```

See the [API reference](/docs/14/app/api-reference/file-conventions/route-segment-config) for more details.

## API Reference

Learn more about the route.js file.

[Introduction  
\
...  
\
File Conventions  
\
**route.js**  
\
API reference for the route.js special file.](/docs/14/app/api-reference/file-conventions/route)

Was this helpful?

supported.

Send
