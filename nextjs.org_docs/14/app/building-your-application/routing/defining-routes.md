---
title: "Defining Routes"
source: "https://nextjs.org/docs/14/app/building-your-application/routing/defining-routes"
---

# Defining Routes

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[Building Your Application](/docs/14/app/building-your-application)[Routing](/docs/14/app/building-your-application/routing)Defining Routes

You are currently viewing documentation for version 14 of Next.js.

# Defining Routes

> We recommend reading the [Routing Fundamentals](/docs/14/app/building-your-application/routing) page before continuing.

This page will guide you through how to define and organize routes in your Next.js application.

## [Creating Routes](#creating-routes)

Next.js uses a file-system based router where **folders** are used to define routes.

Each folder represents a [**route** segment](/docs/14/app/building-your-application/routing#route-segments) that maps to a **URL** segment. To create a [nested route](/docs/14/app/building-your-application/routing#nested-routes), you can nest folders inside each other.

![Route segments to path segments](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Froute-segments-to-path-segments.png&w=3840&q=75)![Route segments to path segments](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Froute-segments-to-path-segments.png&w=3840&q=75)

A special [`page.js` file](/docs/14/app/building-your-application/routing/pages-and-layouts#pages) is used to make route segments publicly accessible.

![Defining Routes](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fdefining-routes.png&w=3840&q=75)![Defining Routes](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fdefining-routes.png&w=3840&q=75)

In this example, the `/dashboard/analytics` URL path is *not* publicly accessible because it does not have a corresponding `page.js` file. This folder could be used to store components, stylesheets, images, or other colocated files.

> **Good to know**: `.js`, `.jsx`, or `.tsx` file extensions can be used for special files.

## [Creating UI](#creating-ui)

[Special file conventions](/docs/14/app/building-your-application/routing#file-conventions) are used to create UI for each route segment. The most common are [pages](/docs/14/app/building-your-application/routing/pages-and-layouts#pages) to show UI unique to a route, and [layouts](/docs/14/app/building-your-application/routing/pages-and-layouts#layouts) to show UI that is shared across multiple routes.

For example, to create your first page, add a `page.js` file inside the `app` directory and export a React component:

app/page.tsx

TypeScript

JavaScriptTypeScript

```
export default function Page() {
  return <h1>Hello, Next.js!</h1>
}
```

## Next Steps

Learn more about creating pages and layouts.

[Introduction  
\
...  
\
Routing  
\
**Pages and Layouts**  
\
Create your first page and shared layout with the App Router.](/docs/14/app/building-your-application/routing/pages-and-layouts)

Was this helpful?

supported.

Send
