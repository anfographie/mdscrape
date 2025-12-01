---
title: "template.js"
source: "https://nextjs.org/docs/14/app/api-reference/file-conventions/template"
---

# template.js

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[File Conventions](/docs/14/app/api-reference/file-conventions)template.js

You are currently viewing documentation for version 14 of Next.js.

# template.js

A **template** file is similar to a [layout](/docs/14/app/building-your-application/routing/pages-and-layouts#layouts) in that it wraps each child layout or page. Unlike layouts that persist across routes and maintain state, templates create a new instance for each of their children on navigation.

app/template.tsx

TypeScript

JavaScriptTypeScript

```
export default function Template({ children }: { children: React.ReactNode }) {
  return <div>{children}</div>
}
```

![template.js special file](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Ftemplate-special-file.png&w=3840&q=75)![template.js special file](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Ftemplate-special-file.png&w=3840&q=75)

While less common, you might choose a template over a layout if you want:

- Features that rely on `useEffect` (e.g logging page views) and `useState` (e.g a per-page feedback form).
- To change the default framework behavior. For example, Suspense Boundaries inside layouts only show the fallback the first time the Layout is loaded and not when switching pages. For templates, the fallback is shown on each navigation.

## [Props](#props)

### [`children` (required)](#children-required)

Template components should accept and use a `children` prop. `template` is rendered between a [layout](/docs/14/app/api-reference/file-conventions/layout) and its children. For example:

Output

```
<Layout>
  {/* Note that the template is given a unique key. */}
  <Template key={routeParam}>{children}</Template>
</Layout>
```

> **Good to know**:
> 
> - By default, `template` is a [Server Component](/docs/14/app/building-your-application/rendering/server-components), but can also be used as a [Client Component](/docs/14/app/building-your-application/rendering/client-components) through the `"use client"` directive.
> - When a user navigates between routes that share a `template`, a new instance of the component is mounted, DOM elements are recreated, state is **not** preserved, and effects are re-synchronized.

## [Version History](#version-history)

VersionChanges`v13.0.0``template` introduced.

Was this helpful?

supported.

Send
