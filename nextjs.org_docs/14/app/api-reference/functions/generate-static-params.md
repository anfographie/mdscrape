---
title: "generateStaticParams"
source: "https://nextjs.org/docs/14/app/api-reference/functions/generate-static-params"
---

# generateStaticParams

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[Functions](/docs/14/app/api-reference/functions)generateStaticParams

You are currently viewing documentation for version 14 of Next.js.

# generateStaticParams

The `generateStaticParams` function can be used in combination with [dynamic route segments](/docs/14/app/building-your-application/routing/dynamic-routes) to [**statically generate**](/docs/14/app/building-your-application/rendering/server-components#static-rendering-default) routes at build time instead of on-demand at request time.

app/blog/\[slug]/page.js

```
// Return a list of `params` to populate the [slug] dynamic segment
export async function generateStaticParams() {
  const posts = await fetch('https://.../posts').then((res) => res.json())
 
  return posts.map((post) => ({
    slug: post.slug,
  }))
}
 
// Multiple versions of this page will be statically generated
// using the `params` returned by `generateStaticParams`
export default function Page({ params }) {
  const { slug } = params
  // ...
}
```

> **Good to know**
> 
> - You can use the [`dynamicParams`](/docs/14/app/api-reference/file-conventions/route-segment-config#dynamicparams) segment config option to control what happens when a dynamic segment is visited that was not generated with `generateStaticParams`.
> - During `next dev`, `generateStaticParams` will be called when you navigate to a route.
> - During `next build`, `generateStaticParams` runs before the corresponding Layouts or Pages are generated.
> - During revalidation (ISR), `generateStaticParams` will not be called again.
> - `generateStaticParams` replaces the [`getStaticPaths`](/docs/14/pages/api-reference/functions/get-static-paths) function in the Pages Router.

## [Parameters](#parameters)

`options.params` (optional)

If multiple dynamic segments in a route use `generateStaticParams`, the child `generateStaticParams` function is executed once for each set of `params` the parent generates.

The `params` object contains the populated `params` from the parent `generateStaticParams`, which can be used to [generate the `params` in a child segment](#multiple-dynamic-segments-in-a-route).

## [Returns](#returns)

`generateStaticParams` should return an array of objects where each object represents the populated dynamic segments of a single route.

- Each property in the object is a dynamic segment to be filled in for the route.
- The properties name is the segment's name, and the properties value is what that segment should be filled in with.

Example Route`generateStaticParams` Return Type`/product/[id]``{ id: string }[]``/products/[category]/[product]``{ category: string, product: string }[]``/products/[...slug]``{ slug: string[] }[]`

## [Single Dynamic Segment](#single-dynamic-segment)

app/product/\[id]/page.tsx

TypeScript

JavaScriptTypeScript

```
export function generateStaticParams() {
  return [{ id: '1' }, { id: '2' }, { id: '3' }]
}
 
// Three versions of this page will be statically generated
// using the `params` returned by `generateStaticParams`
// - /product/1
// - /product/2
// - /product/3
export default function Page({ params }: { params: { id: string } }) {
  const { id } = params
  // ...
}
```

## [Multiple Dynamic Segments](#multiple-dynamic-segments)

app/products/\[category]/\[product]/page.tsx

TypeScript

JavaScriptTypeScript

```
export function generateStaticParams() {
  return [
    { category: 'a', product: '1' },
    { category: 'b', product: '2' },
    { category: 'c', product: '3' },
  ]
}
 
// Three versions of this page will be statically generated
// using the `params` returned by `generateStaticParams`
// - /products/a/1
// - /products/b/2
// - /products/c/3
export default function Page({
  params,
}: {
  params: { category: string; product: string }
}) {
  const { category, product } = params
  // ...
}
```

## [Catch-all Dynamic Segment](#catch-all-dynamic-segment)

app/product/\[...slug]/page.tsx

TypeScript

JavaScriptTypeScript

```
export function generateStaticParams() {
  return [{ slug: ['a', '1'] }, { slug: ['b', '2'] }, { slug: ['c', '3'] }]
}
 
// Three versions of this page will be statically generated
// using the `params` returned by `generateStaticParams`
// - /product/a/1
// - /product/b/2
// - /product/c/3
export default function Page({ params }: { params: { slug: string[] } }) {
  const { slug } = params
  // ...
}
```

## [Examples](#examples)

### [Multiple Dynamic Segments in a Route](#multiple-dynamic-segments-in-a-route)

You can generate params for dynamic segments above the current layout or page, but **not below**. For example, given the `app/products/[category]/[product]` route:

- `app/products/[category]/[product]/page.js` can generate params for **both** `[category]` and `[product]`.
- `app/products/[category]/layout.js` can **only** generate params for `[category]`.

There are two approaches to generating params for a route with multiple dynamic segments:

### [Generate params from the bottom up](#generate-params-from-the-bottom-up)

Generate multiple dynamic segments from the child route segment.

app/products/\[category]/\[product]/page.tsx

TypeScript

JavaScriptTypeScript

```
// Generate segments for both [category] and [product]
export async function generateStaticParams() {
  const products = await fetch('https://.../products').then((res) => res.json())
 
  return products.map((product) => ({
    category: product.category.slug,
    product: product.id,
  }))
}
 
export default function Page({
  params,
}: {
  params: { category: string; product: string }
}) {
  // ...
}
```

### [Generate params from the top down](#generate-params-from-the-top-down)

Generate the parent segments first and use the result to generate the child segments.

app/products/\[category]/layout.tsx

TypeScript

JavaScriptTypeScript

```
// Generate segments for [category]
export async function generateStaticParams() {
  const products = await fetch('https://.../products').then((res) => res.json())
 
  return products.map((product) => ({
    category: product.category.slug,
  }))
}
 
export default function Layout({ params }: { params: { category: string } }) {
  // ...
}
```

A child route segment's `generateStaticParams` function is executed once for each segment a parent `generateStaticParams` generates.

The child `generateStaticParams` function can use the `params` returned from the parent `generateStaticParams` function to dynamically generate its own segments.

app/products/\[category]/\[product]/page.tsx

TypeScript

JavaScriptTypeScript

```
// Generate segments for [product] using the `params` passed from
// the parent segment's `generateStaticParams` function
export async function generateStaticParams({
  params: { category },
}: {
  params: { category: string }
}) {
  const products = await fetch(
    `https://.../products?category=${category}`
  ).then((res) => res.json())
 
  return products.map((product) => ({
    product: product.id,
  }))
}
 
export default function Page({
  params,
}: {
  params: { category: string; product: string }
}) {
  // ...
}
```

> **Good to know**: `fetch` requests are automatically [memoized](/docs/14/app/building-your-application/caching#request-memoization) for the same data across all `generate`-prefixed functions, Layouts, Pages, and Server Components. React [`cache` can be used](/docs/14/app/building-your-application/caching#request-memoization) if `fetch` is unavailable.

### [Generate only a subset of params](#generate-only-a-subset-of-params)

You can generate a subset of params for a route by returning an array of objects with only the dynamic segments you want to generate. Then, by using the [`dynamicParams`](/docs/14/app/api-reference/file-conventions/route-segment-config#dynamicparams) segment config option, you can control what happens when a dynamic segment is visited that was not generated with `generateStaticParams`.

app/blog/\[slug]/page.js

```
// All posts besides the top 10 will be a 404
export const dynamicParams = false
 
export async function generateStaticParams() {
  const posts = await fetch('https://.../posts').then((res) => res.json())
  const topPosts = posts.slice(0, 10)
 
  return topPosts.map((post) => ({
    slug: post.slug,
  }))
}
```

## [Version History](#version-history)

VersionChanges`v13.0.0``generateStaticParams` introduced.

Was this helpful?

supported.

Send
