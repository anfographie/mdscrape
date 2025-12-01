---
title: "default.js"
source: "https://nextjs.org/docs/14/app/api-reference/file-conventions/default"
---

# default.js

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[File Conventions](/docs/14/app/api-reference/file-conventions)default.js

You are currently viewing documentation for version 14 of Next.js.

# default.js

The `default.js` file is used to render a fallback within [Parallel Routes](/docs/14/app/building-your-application/routing/parallel-routes) when Next.js cannot recover a [slot's](/docs/14/app/building-your-application/routing/parallel-routes#slots) active state after a full-page load.

During [soft navigation](/docs/14/app/building-your-application/routing/linking-and-navigating#5-soft-navigation), Next.js keeps track of the active *state* (subpage) for each slot. However, for hard navigations (full-page load), Next.js cannot recover the active state. In this case, a `default.js` file can be rendered for subpages that don't match the current URL.

Consider the following folder structure. The `@team` slot has a `settings` page, but `@analytics` does not.

![Parallel Routes unmatched routes](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes-unmatched-routes.png&w=3840&q=75)![Parallel Routes unmatched routes](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-unmatched-routes.png&w=3840&q=75)

When navigating to `/settings`, the `@team` slot will render the `settings` page while maintaining the currently active page for the `@analytics` slot.

On refresh, Next.js will render a `default.js` for `@analytics`. If `default.js` doesn't exist, a `404` is rendered instead.

Additionally, since `children` is an implicit slot, you also need to create a `default.js` file to render a fallback for `children` when Next.js cannot recover the active state of the parent page.

## [Props](#props)

### [`params` (optional)](#params-optional)

An object containing the [dynamic route parameters](/docs/14/app/building-your-application/routing/dynamic-routes) from the root segment down to the slot's subpages. For example:

ExampleURL`params``app/@sidebar/[artist]/default.js``/zack``{ artist: 'zack' }``app/@sidebar/[artist]/[album]/default.js``/zack/next``{ artist: 'zack', album: 'next' }`

## Learn more about Parallel Routes

[Introduction  
\
...  
\
Routing  
\
**Parallel Routes**  
\
Simultaneously render one or more pages in the same view that can be navigated independently. A pattern for highly dynamic applications.](/docs/14/app/building-your-application/routing/parallel-routes)

Was this helpful?

supported.

Send
