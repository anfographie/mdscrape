---
title: "Routing Fundamentals"
source: "https://nextjs.org/docs/13/app/building-your-application/routing"
---

# Routing Fundamentals

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[App Router](/docs/13/app)[Building Your Application](/docs/13/app/building-your-application)Routing

You are currently viewing documentation for version 13 of Next.js.

# Routing Fundamentals

The skeleton of every application is routing. This page will introduce you to the **fundamental concepts** of routing for the web and how to handle routing in Next.js.

## [Terminology](#terminology)

First, you will see these terms being used throughout the documentation. Here's a quick reference:

![Terminology for Component Tree](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fterminology-component-tree.png&w=3840&q=75)![Terminology for Component Tree](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fterminology-component-tree.png&w=3840&q=75)

- **Tree:** A convention for visualizing a hierarchical structure. For example, a component tree with parent and children components, a folder structure, etc.
- **Subtree:** Part of a tree, starting at a new root (first) and ending at the leaves (last).
- **Root**: The first node in a tree or subtree, such as a root layout.
- **Leaf:** Nodes in a subtree that have no children, such as the last segment in a URL path.

<!--THE END-->

![Terminology for URL Anatomy](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fterminology-url-anatomy.png&w=3840&q=75)![Terminology for URL Anatomy](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fterminology-url-anatomy.png&w=3840&q=75)

- **URL Segment:** Part of the URL path delimited by slashes.
- **URL Path:** Part of the URL that comes after the domain (composed of segments).

## [The `app` Router](#the-app-router)

In version 13, Next.js introduced a new **App Router** built on [React Server Components](/docs/13/app/building-your-application/rendering/server-components), which supports shared layouts, nested routing, loading states, error handling, and more.

The App Router works in a new directory named `app`. The `app` directory works alongside the `pages` directory to allow for incremental adoption. This allows you to opt some routes of your application into the new behavior while keeping other routes in the `pages` directory for previous behavior. If your application uses the `pages` directory, please also see the [Pages Router](/docs/13/pages/building-your-application/routing) documentation.

> **Good to know**: The App Router takes priority over the Pages Router. Routes across directories should not resolve to the same URL path and will cause a build-time error to prevent a conflict.

![Next.js App Directory](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fnext-router-directories.png&w=3840&q=75)![Next.js App Directory](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fnext-router-directories.png&w=3840&q=75)

By default, components inside `app` are [React Server Components](/docs/13/app/building-your-application/rendering/server-components). This is a performance optimization and allows you to easily adopt them, and you can also use [Client Components](/docs/13/app/building-your-application/rendering/client-components).

> **Recommendation:** Check out the [Server](/docs/13/app/building-your-application/rendering/server-components) page if you're new to Server Components.

## [Roles of Folders and Files](#roles-of-folders-and-files)

Next.js uses a file-system based router where:

- **Folders** are used to define routes. A route is a single path of nested folders, following the file-system hierarchy from the **root folder** down to a final **leaf folder** that includes a `page.js` file. See [Defining Routes](/docs/13/app/building-your-application/routing/defining-routes).
- **Files** are used to create UI that is shown for a route segment. See [special files](#file-conventions).

## [Route Segments](#route-segments)

Each folder in a route represents a **route segment**. Each route segment is mapped to a corresponding **segment** in a **URL path**.

![How Route Segments Map to URL Segments](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Froute-segments-to-path-segments.png&w=3840&q=75)![How Route Segments Map to URL Segments](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Froute-segments-to-path-segments.png&w=3840&q=75)

## [Nested Routes](#nested-routes)

To create a nested route, you can nest folders inside each other. For example, you can add a new `/dashboard/settings` route by nesting two new folders in the `app` directory.

The `/dashboard/settings` route is composed of three segments:

- `/` (Root segment)
- `dashboard` (Segment)
- `settings` (Leaf segment)

## [File Conventions](#file-conventions)

Next.js provides a set of special files to create UI with specific behavior in nested routes:

[`layout`](/docs/13/app/building-your-application/routing/pages-and-layouts#layouts)Shared UI for a segment and its children[`page`](/docs/13/app/building-your-application/routing/pages-and-layouts#pages)Unique UI of a route and make routes publicly accessible[`loading`](/docs/13/app/building-your-application/routing/loading-ui-and-streaming)Loading UI for a segment and its children[`not-found`](/docs/13/app/api-reference/file-conventions/not-found)Not found UI for a segment and its children[`error`](/docs/13/app/building-your-application/routing/error-handling)Error UI for a segment and its children[`global-error`](/docs/13/app/building-your-application/routing/error-handling)Global Error UI[`route`](/docs/13/app/building-your-application/routing/route-handlers)Server-side API endpoint[`template`](/docs/13/app/building-your-application/routing/pages-and-layouts#templates)Specialized re-rendered Layout UI[`default`](/docs/13/app/api-reference/file-conventions/default)Fallback UI for [Parallel Routes](/docs/13/app/building-your-application/routing/parallel-routes)

> **Good to know**: `.js`, `.jsx`, or `.tsx` file extensions can be used for special files.

## [Component Hierarchy](#component-hierarchy)

The React components defined in special files of a route segment are rendered in a specific hierarchy:

- `layout.js`
- `template.js`
- `error.js` (React error boundary)
- `loading.js` (React suspense boundary)
- `not-found.js` (React error boundary)
- `page.js` or nested `layout.js`

![Component Hierarchy for File Conventions](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Ffile-conventions-component-hierarchy.png&w=3840&q=75)![Component Hierarchy for File Conventions](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Ffile-conventions-component-hierarchy.png&w=3840&q=75)

In a nested route, the components of a segment will be nested **inside** the components of its parent segment.

![Nested File Conventions Component Hierarchy](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fnested-file-conventions-component-hierarchy.png&w=3840&q=75)![Nested File Conventions Component Hierarchy](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fnested-file-conventions-component-hierarchy.png&w=3840&q=75)

## [Colocation](#colocation)

In addition to special files, you have the option to colocate your own files (e.g. components, styles, tests, etc) inside folders in the `app` directory.

This is because while folders define routes, only the contents returned by `page.js` or `route.js` are publicly addressable.

![An example folder structure with colocated files](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fproject-organization-colocation.png&w=3840&q=75)![An example folder structure with colocated files](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fproject-organization-colocation.png&w=3840&q=75)

Learn more about [Project Organization and Colocation](/docs/13/app/building-your-application/routing/colocation).

## [Advanced Routing Patterns](#advanced-routing-patterns)

The App Router also provides a set of conventions to help you implement more advanced routing patterns. These include:

- [Parallel Routes](/docs/13/app/building-your-application/routing/parallel-routes): Allow you to simultaneously show two or more pages in the same view that can be navigated independently. You can use them for split views that have their own sub-navigation. E.g. Dashboards.
- [Intercepting Routes](/docs/13/app/building-your-application/routing/intercepting-routes): Allow you to intercept a route and show it in the context of another route. You can use these when keeping the context for the current page is important. E.g. Seeing all tasks while editing one task or expanding a photo in a feed.

These patterns allow you to build richer and more complex UIs, democratizing features that were historically complex for small teams and individual developers to implement.

## [Next Steps](#next-steps)

Now that you understand the fundamentals of routing in Next.js, follow the links below to create your first routes:

[**Defining Routes**  
\
Learn how to create your first route in Next.js.](/docs/13/app/building-your-application/routing/defining-routes)

[**Pages and Layouts**  
\
Create your first page and shared layout with the App Router.](/docs/13/app/building-your-application/routing/pages-and-layouts)

[**Linking and Navigating**  
\
Learn how navigation works in Next.js, and how to use the Link Component and \`useRouter\` hook.](/docs/13/app/building-your-application/routing/linking-and-navigating)

[**Route Groups**  
\
Route Groups can be used to partition your Next.js application into different sections.](/docs/13/app/building-your-application/routing/route-groups)

[**Dynamic Routes**  
\
Dynamic Routes can be used to programmatically generate route segments from dynamic data.](/docs/13/app/building-your-application/routing/dynamic-routes)

[**Loading UI and Streaming**  
\
Built on top of Suspense, Loading UI allows you to create a fallback for specific route segments, and automatically stream content as it becomes ready.](/docs/13/app/building-your-application/routing/loading-ui-and-streaming)

[**Error Handling**  
\
Handle runtime errors by automatically wrapping route segments and their nested children in a React Error Boundary.](/docs/13/app/building-your-application/routing/error-handling)

[**Parallel Routes**  
\
Simultaneously render one or more pages in the same view that can be navigated independently. A pattern for highly dynamic applications.](/docs/13/app/building-your-application/routing/parallel-routes)

[**Intercepting Routes**  
\
Use intercepting routes to load a new route within the current layout while masking the browser URL, useful for advanced routing patterns such as modals.](/docs/13/app/building-your-application/routing/intercepting-routes)

[**Route Handlers**  
\
Create custom request handlers for a given route using the Web's Request and Response APIs.](/docs/13/app/building-your-application/routing/route-handlers)

[**Middleware**  
\
Learn how to use Middleware to run code before a request is completed.](/docs/13/app/building-your-application/routing/middleware)

[**Project Organization**  
\
Learn how to organize your Next.js project and colocate files.](/docs/13/app/building-your-application/routing/colocation)

[**Internationalization**  
\
Add support for multiple languages with internationalized routing and localized content.](/docs/13/app/building-your-application/routing/internationalization)

Was this helpful?

supported.

Send
