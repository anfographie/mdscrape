---
title: "loading.js"
source: "https://nextjs.org/docs/14/app/api-reference/file-conventions/loading"
---

# loading.js

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[File Conventions](/docs/14/app/api-reference/file-conventions)loading.js

You are currently viewing documentation for version 14 of Next.js.

# loading.js

A **loading** file can create instant loading states built on [Suspense](/docs/14/app/building-your-application/routing/loading-ui-and-streaming).

By default, this file is a [Server Component](/docs/14/app/building-your-application/rendering/server-components) - but can also be used as a Client Component through the `"use client"` directive.

app/feed/loading.tsx

TypeScript

JavaScriptTypeScript

```
export default function Loading() {
  // Or a custom loading skeleton component
  return <p>Loading...</p>
}
```

Loading UI components do not accept any parameters.

> **Good to know**
> 
> - While designing loading UI, you may find it helpful to use the [React Developer Tools](https://react.dev/learn/react-developer-tools) to manually toggle Suspense boundaries.

## [Version History](#version-history)

VersionChanges`v13.0.0``loading` introduced.

Was this helpful?

supported.

Send
