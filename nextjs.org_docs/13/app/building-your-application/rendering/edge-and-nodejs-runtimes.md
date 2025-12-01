---
title: "Edge and Node.js Runtimes"
source: "https://nextjs.org/docs/13/app/building-your-application/rendering/edge-and-nodejs-runtimes"
---

# Edge and Node.js Runtimes

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[Building Your Application](/docs/13/app/building-your-application)[Rendering](/docs/13/app/building-your-application/rendering)Edge and Node.js Runtimes

You are currently viewing documentation for version 13 of Next.js.

# Edge and Node.js Runtimes

In the context of Next.js, runtime refers to the set of libraries, APIs, and general functionality available to your code during execution.

On the server, there are two runtimes where parts of your application code can be rendered:

- The **Node.js Runtime** (default) has access to all Node.js APIs and compatible packages from the ecosystem.
- The **Edge Runtime** is based on [Web APIs](/docs/13/app/api-reference/edge).

## [Runtime Differences](#runtime-differences)

There are many considerations to make when choosing a runtime. This table shows the major differences at a glance. If you want a more in-depth analysis of the differences, check out the sections below.

NodeServerlessEdge[Cold Boot](https://vercel.com/docs/concepts/get-started/compute#cold-and-hot-boots?utm_source=next-site&utm_medium=docs&utm_campaign=next-website)/~250msInstant[HTTP Streaming](/docs/13/app/building-your-application/routing/loading-ui-and-streaming)YesYesYesIOAllAll`fetch`Scalability/HighHighestSecurityNormalHighHighLatencyNormalLowLowestnpm PackagesAllAllA smaller subset[Static Rendering](/docs/13/app/building-your-application/rendering/server-components#static-rendering-default)YesYesNo[Dynamic Rendering](/docs/13/app/building-your-application/rendering/server-components#dynamic-rendering)YesYesYes[Data Revalidation w/ `fetch`](/docs/13/app/building-your-application/data-fetching/fetching-caching-and-revalidating#revalidating-data)YesYesYes

### [Edge Runtime](#edge-runtime)

In Next.js, the lightweight Edge Runtime is a subset of available Node.js APIs.

The Edge Runtime is ideal if you need to deliver dynamic, personalized content at low latency with small, simple functions. The Edge Runtime's speed comes from its minimal use of resources, but that can be limiting in many scenarios.

For example, code executed in the Edge Runtime [on Vercel cannot exceed between 1 MB and 4 MB](https://vercel.com/docs/concepts/limits/overview#edge-middleware-and-edge-functions-size), this limit includes imported packages, fonts and files, and will vary depending on your deployment infrastructure.

### [Node.js Runtime](#nodejs-runtime)

Using the Node.js runtime gives you access to all Node.js APIs, and all npm packages that rely on them. However, it's not as fast to start up as routes using the Edge runtime.

Deploying your Next.js application to a Node.js server will require managing, scaling, and configuring your infrastructure. Alternatively, you can consider deploying your Next.js application to a serverless platform like Vercel, which will handle this for you.

### [Serverless Node.js](#serverless-nodejs)

Serverless is ideal if you need a scalable solution that can handle more complex computational loads than the Edge Runtime. With Serverless Functions on Vercel, for example, your overall code size is [50MB](https://vercel.com/docs/concepts/limits/overview#serverless-function-size) including imported packages, fonts, and files.

The downside compared to routes using the [Edge](https://vercel.com/docs/concepts/functions/edge-functions) is that it can take hundreds of milliseconds for Serverless Functions to boot up before they begin processing requests. Depending on the amount of traffic your site receives, this could be a frequent occurrence as the functions are not frequently "warm".

## [Examples](#examples)

### [Segment Runtime Option](#segment-runtime-option)

You can specify a runtime for individual route segments in your Next.js application. To do so, [declare a variable called `runtime` and export it](/docs/13/app/api-reference/file-conventions/route-segment-config). The variable must be a string, and must have a value of either `'nodejs'` or `'edge'` runtime.

The following example demonstrates a page route segment that exports a `runtime` with a value of `'edge'`:

app/page.tsx

TypeScript

JavaScriptTypeScript

```
export const runtime = 'edge' // 'nodejs' (default) | 'edge'
```

You can also define `runtime` on a layout level, which will make all routes under the layout run on the edge runtime:

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
export const runtime = 'edge' // 'nodejs' (default) | 'edge'
```

If the segment runtime is *not* set, the default `nodejs` runtime will be used. You do not need to use the `runtime` option if you do not plan to change from the Node.js runtime.

> Please refer to the [Node.js Docs](https://nodejs.org/docs/latest/api/) and [Edge Docs](/docs/13/app/api-reference/edge) for the full list of available APIs. Both runtimes can also support [streaming](/docs/13/app/building-your-application/routing/loading-ui-and-streaming) depending on your deployment infrastructure.

Was this helpful?

supported.

Send
