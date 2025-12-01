---
title: "usePathname"
source: "https://nextjs.org/docs/13/app/api-reference/functions/use-pathname"
---

# usePathname

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[Functions](/docs/13/app/api-reference/functions)usePathname

You are currently viewing documentation for version 13 of Next.js.

# usePathname

`usePathname` is a **Client Component** hook that lets you read the current URL's **pathname**.

app/example-client-component.tsx

TypeScript

JavaScriptTypeScript

```
'use client'
 
import { usePathname } from 'next/navigation'
 
export default function ExampleClientComponent() {
  const pathname = usePathname()
  return <p>Current pathname: {pathname}</p>
}
```

`usePathname` intentionally requires using a [Client Component](/docs/13/app/building-your-application/rendering/client-components). It's important to note Client Components are not a de-optimization. They are an integral part of the [Server Components](/docs/13/app/building-your-application/rendering/server-components) architecture.

For example, a Client Component with `usePathname` will be rendered into HTML on the initial page load. When navigating to a new route, this component does not need to be re-fetched. Instead, the component is downloaded once (in the client JavaScript bundle), and re-renders based on the current state.

> **Good to know**:
> 
> - Reading the current URL from a [Server Component](/docs/13/app/building-your-application/rendering/server-components) is not supported. This design is intentional to support layout state being preserved across page navigations.
> - Compatibility mode:
>   
>   - `usePathname` can return `null` when a [fallback route](/docs/13/pages/api-reference/functions/get-static-paths#fallback-true) is being rendered or when a `pages` directory page has been [automatically statically optimized](/docs/13/pages/building-your-application/rendering/automatic-static-optimization) by Next.js and the router is not ready.
>   - Next.js will automatically update your types if it detects both an `app` and `pages` directory in your project.

## [Parameters](#parameters)

```
const pathname = usePathname()
```

`usePathname` does not take any parameters.

## [Returns](#returns)

`usePathname` returns a string of the current URL's pathname. For example:

URLReturned value`/``'/'``/dashboard``'/dashboard'``/dashboard?v=2``'/dashboard'``/blog/hello-world``'/blog/hello-world'`

## [Examples](#examples)

### [Do something in response to a route change](#do-something-in-response-to-a-route-change)

app/example-client-component.tsx

TypeScript

JavaScriptTypeScript

```
'use client'
 
import { usePathname, useSearchParams } from 'next/navigation'
 
function ExampleClientComponent() {
  const pathname = usePathname()
  const searchParams = useSearchParams()
  useEffect(() => {
    // Do something here...
  }, [pathname, searchParams])
}
```

VersionChanges`v13.0.0``usePathname` introduced.

Was this helpful?

supported.

Send
