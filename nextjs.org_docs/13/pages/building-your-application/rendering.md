---
title: "Rendering"
source: "https://nextjs.org/docs/13/pages/building-your-application/rendering"
---

# Rendering

Menu

Pages Router 13

Using Pages Router

Features available in /pages

Version 13

13.5.11

[Pages Router](/docs/13/pages)[Building Your Application](/docs/13/pages/building-your-application)Rendering

You are currently viewing the Pages Router documentation for version 13 of Next.js.

# Rendering

By default, Next.js **pre-renders** every page. This means that Next.js generates HTML for each page in advance, instead of having it all done by client-side JavaScript. Pre-rendering can result in better performance and SEO.

Each generated HTML is associated with minimal JavaScript code necessary for that page. When a page is loaded by the browser, its JavaScript code runs and makes the page fully interactive (this process is called [hydration](https://react.dev/reference/react-dom/client/hydrateRoot) in React).

### [Pre-rendering](#pre-rendering)

Next.js has two forms of pre-rendering: **Static Generation** and **Server-side Rendering**. The difference is in **when** it generates the HTML for a page.

- Static Generation: The HTML is generated at **build time** and will be reused on each request.
- Server-side Rendering: The HTML is generated on **each request**.

Importantly, Next.js lets you choose which pre-rendering form you'd like to use for each page. You can create a "hybrid" Next.js app by using Static Generation for most pages and using Server-side Rendering for others.

We recommend using Static Generation over Server-side Rendering for performance reasons. Statically generated pages can be cached by CDN with no extra configuration to boost performance. However, in some cases, Server-side Rendering might be the only option.

You can also use client-side data fetching along with Static Generation or Server-side Rendering. That means some parts of a page can be rendered entirely by clientside JavaScript. To learn more, take a look at the [Data Fetching](/docs/13/pages/building-your-application/data-fetching/client-side) documentation.

[**Server-side Rendering (SSR)**  
\
Use Server-side Rendering to render pages on each request.](/docs/13/pages/building-your-application/rendering/server-side-rendering)

[**Static Site Generation (SSG)**  
\
Use Static Site Generation (SSG) to pre-render pages at build time.](/docs/13/pages/building-your-application/rendering/static-site-generation)

[**Incremental Static Regeneration (ISR)**  
\
Learn how to create or update static pages at runtime with Incremental Static Regeneration.](/docs/13/pages/building-your-application/rendering/incremental-static-regeneration)

[**Automatic Static Optimization**  
\
Next.js automatically optimizes your app to be static HTML whenever possible. Learn how it works here.](/docs/13/pages/building-your-application/rendering/automatic-static-optimization)

[**Client-side Rendering (CSR)**  
\
Learn how to implement client-side rendering in the Pages Router.](/docs/13/pages/building-your-application/rendering/client-side-rendering)

[**Edge and Node.js Runtimes**  
\
Learn more about the switchable runtimes (Edge and Node.js) in Next.js.](/docs/13/pages/building-your-application/rendering/edge-and-nodejs-runtimes)

Was this helpful?

supported.

Send
