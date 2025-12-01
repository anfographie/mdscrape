---
title: "Dynamic Routes"
source: "https://nextjs.org/docs/14/app/building-your-application/routing/dynamic-routes"
---

# Dynamic Routes

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[Building Your Application](/docs/14/app/building-your-application)[Routing](/docs/14/app/building-your-application/routing)Dynamic Routes

You are currently viewing documentation for version 14 of Next.js.

# Dynamic Routes

When you don't know the exact segment names ahead of time and want to create routes from dynamic data, you can use Dynamic Segments that are filled in at request time or [prerendered](#generating-static-params) at build time.

## [Convention](#convention)

A Dynamic Segment can be created by wrapping a folder's name in square brackets: `[folderName]`. For example, `[id]` or `[slug]`.

Dynamic Segments are passed as the `params` prop to [`layout`](/docs/14/app/api-reference/file-conventions/layout), [`page`](/docs/14/app/api-reference/file-conventions/page), [`route`](/docs/14/app/building-your-application/routing/route-handlers), and [`generateMetadata`](/docs/14/app/api-reference/functions/generate-metadata#generatemetadata-function) functions.

## [Example](#example)

For example, a blog could include the following route `app/blog/[slug]/page.js` where `[slug]` is the Dynamic Segment for blog posts.

app/blog/\[slug]/page.tsx

TypeScript

JavaScriptTypeScript

```
export default function Page({ params }: { params: { slug: string } }) {
  return <div>My Post: {params.slug}</div>
}
```

RouteExample URL`params``app/blog/[slug]/page.js``/blog/a``{ slug: 'a' }``app/blog/[slug]/page.js``/blog/b``{ slug: 'b' }``app/blog/[slug]/page.js``/blog/c``{ slug: 'c' }`

See the [generateStaticParams()](#generating-static-params) page to learn how to generate the params for the segment.

> **Good to know**: Dynamic Segments are equivalent to [Dynamic Routes](/docs/14/app/building-your-application/routing/dynamic-routes) in the `pages` directory.

## [Generating Static Params](#generating-static-params)

The `generateStaticParams` function can be used in combination with [dynamic route segments](/docs/14/app/building-your-application/routing/dynamic-routes) to [**statically generate**](/docs/14/app/building-your-application/rendering/server-components#static-rendering-default) routes at build time instead of on-demand at request time.

app/blog/\[slug]/page.tsx

TypeScript

JavaScriptTypeScript

```
export async function generateStaticParams() {
  const posts = await fetch('https://.../posts').then((res) => res.json())
 
  return posts.map((post) => ({
    slug: post.slug,
  }))
}
```

The primary benefit of the `generateStaticParams` function is its smart retrieval of data. If content is fetched within the `generateStaticParams` function using a `fetch` request, the requests are [automatically memoized](/docs/14/app/building-your-application/caching#request-memoization). This means a `fetch` request with the same arguments across multiple `generateStaticParams`, Layouts, and Pages will only be made once, which decreases build times.

Use the [migration guide](/docs/14/app/building-your-application/upgrading/app-router-migration#dynamic-paths-getstaticpaths) if you are migrating from the `pages` directory.

See [`generateStaticParams` server function documentation](/docs/14/app/api-reference/functions/generate-static-params) for more information and advanced use cases.

## [Catch-all Segments](#catch-all-segments)

Dynamic Segments can be extended to **catch-all** subsequent segments by adding an ellipsis inside the brackets `[...folderName]`.

For example, `app/shop/[...slug]/page.js` will match `/shop/clothes`, but also `/shop/clothes/tops`, `/shop/clothes/tops/t-shirts`, and so on.

RouteExample URL`params``app/shop/[...slug]/page.js``/shop/a``{ slug: ['a'] }``app/shop/[...slug]/page.js``/shop/a/b``{ slug: ['a', 'b'] }``app/shop/[...slug]/page.js``/shop/a/b/c``{ slug: ['a', 'b', 'c'] }`

## [Optional Catch-all Segments](#optional-catch-all-segments)

Catch-all Segments can be made **optional** by including the parameter in double square brackets: `[[...folderName]]`.

For example, `app/shop/[[...slug]]/page.js` will **also** match `/shop`, in addition to `/shop/clothes`, `/shop/clothes/tops`, `/shop/clothes/tops/t-shirts`.

The difference between **catch-all** and **optional catch-all** segments is that with optional, the route without the parameter is also matched (`/shop` in the example above).

RouteExample URL`params``app/shop/[[...slug]]/page.js``/shop``{}``app/shop/[[...slug]]/page.js``/shop/a``{ slug: ['a'] }``app/shop/[[...slug]]/page.js``/shop/a/b``{ slug: ['a', 'b'] }``app/shop/[[...slug]]/page.js``/shop/a/b/c``{ slug: ['a', 'b', 'c'] }`

## [TypeScript](#typescript)

When using TypeScript, you can add types for `params` depending on your configured route segment.

app/blog/\[slug]/page.tsx

TypeScript

JavaScriptTypeScript

```
export default function Page({ params }: { params: { slug: string } }) {
  return <h1>My Page</h1>
}
```

Route`params` Type Definition`app/blog/[slug]/page.js``{ slug: string }``app/shop/[...slug]/page.js``{ slug: string[] }``app/shop/[[...slug]]/page.js``{ slug?: string[] }``app/[categoryId]/[itemId]/page.js``{ categoryId: string, itemId: string }`

> **Good to know**: This may be done automatically by the [TypeScript plugin](/docs/14/app/building-your-application/configuring/typescript#typescript-plugin) in the future.

## Next Steps

For more information on what to do next, we recommend the following sections

[Introduction  
\
...  
\
Routing  
\
**Linking and Navigating**  
\
Learn how navigation works in Next.js, and how to use the Link Component and \`useRouter\` hook.](/docs/14/app/building-your-application/routing/linking-and-navigating)

[Introduction  
\
...  
\
Functions  
\
**generateStaticParams**  
\
API reference for the generateStaticParams function.](/docs/14/app/api-reference/functions/generate-static-params)

Was this helpful?

supported.

Send
