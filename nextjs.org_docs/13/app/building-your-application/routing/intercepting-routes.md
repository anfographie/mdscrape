---
title: "Intercepting Routes"
source: "https://nextjs.org/docs/13/app/building-your-application/routing/intercepting-routes"
---

# Intercepting Routes

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[Building Your Application](/docs/13/app/building-your-application)[Routing](/docs/13/app/building-your-application/routing)Intercepting Routes

You are currently viewing documentation for version 13 of Next.js.

# Intercepting Routes

Intercepting routes allows you to load a route from another part of your application within the current layout. This routing paradigm can be useful when you want to display the content of a route without the user switching to a different context.

For example, when clicking on a photo in a feed, you can display the photo in a modal, overlaying the feed. In this case, Next.js intercepts the `/photo/123` route, masks the URL, and overlays it over `/feed`.

![Intercepting routes soft navigation](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fintercepting-routes-soft-navigate.png&w=3840&q=75)![Intercepting routes soft navigation](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fintercepting-routes-soft-navigate.png&w=3840&q=75)

However, when navigating to the photo by clicking a shareable URL or by refreshing the page, the entire photo page should render instead of the modal. No route interception should occur.

![Intercepting routes hard navigation](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fintercepting-routes-hard-navigate.png&w=3840&q=75)![Intercepting routes hard navigation](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fintercepting-routes-hard-navigate.png&w=3840&q=75)

## [Convention](#convention)

Intercepting routes can be defined with the `(..)` convention, which is similar to relative path convention `../` but for segments.

You can use:

- `(.)` to match segments on the **same level**
- `(..)` to match segments **one level above**
- `(..)(..)` to match segments **two levels above**
- `(...)` to match segments from the **root** `app` directory

For example, you can intercept the `photo` segment from within the `feed` segment by creating a `(..)photo` directory.

![Intercepting routes folder structure](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fintercepted-routes-files.png&w=3840&q=75)![Intercepting routes folder structure](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fintercepted-routes-files.png&w=3840&q=75)

> Note that the `(..)` convention is based on *route segments*, not the file-system.

## [Examples](#examples)

### [Modals](#modals)

Intercepting Routes can be used together with [Parallel Routes](/docs/13/app/building-your-application/routing/parallel-routes) to create modals.

Using this pattern to create modals overcomes some common challenges when working with modals, by allowing you to:

- Make the modal content **shareable through a URL**
- **Preserve context** when the page is refreshed, instead of closing the modal
- **Close the modal on backwards navigation** rather than going to the previous route
- **Reopen the modal on forwards navigation**

![Intercepting routes modal example](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fintercepted-routes-modal-example.png&w=3840&q=75)![Intercepting routes modal example](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fintercepted-routes-modal-example.png&w=3840&q=75)

> In the above example, the path to the `photo` segment can use the `(..)` matcher since `@modal` is a *slot* and not a *segment*. This means that the `photo` route is only one *segment* level higher, despite being two *file-system* levels higher.

Other examples could include opening a login modal in a top navbar while also having a dedicated `/login` page, or opening a shopping cart in a side modal.

[View an example](https://github.com/vercel-labs/nextgram) of modals with Intercepted and Parallel Routes.

## Next Steps

Learn how to use modals with Intercepted and Parallel Routes.

[Introduction  
\
...  
\
Routing  
\
**Parallel Routes**  
\
Simultaneously render one or more pages in the same view that can be navigated independently. A pattern for highly dynamic applications.](/docs/13/app/building-your-application/routing/parallel-routes)

Was this helpful?

supported.

Send
