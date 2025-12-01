---
title: "<Link>"
source: "https://nextjs.org/docs/13/app/api-reference/components/link"
---

# <Link>

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[Components](/docs/13/app/api-reference/components)&lt;Link&gt;

You are currently viewing documentation for version 13 of Next.js.

# &lt;Link&gt;

Examples

- [Hello World](https://github.com/vercel/next.js/tree/canary/examples/hello-world)
- [Active className on Link](https://github.com/vercel/next.js/tree/canary/examples/active-class-name)

`<Link>` is a React component that extends the HTML `<a>` element to provide [prefetching](/docs/13/app/building-your-application/routing/linking-and-navigating#1-prefetching) and client-side navigation between routes. It is the primary way to navigate between routes in Next.js.

app/page.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Page() {
  return <Link href="/dashboard">Dashboard</Link>
}
```

## [Props](#props)

Here's a summary of the props available for the Link Component:

PropExampleTypeRequired[`href`](#href-required)`href="/dashboard"`String or ObjectYes[`replace`](#replace)`replace={false}`Boolean-[`scroll`](#scroll)`scroll={false}`Boolean-[`prefetch`](#prefetch)`prefetch={false}`Boolean-

> **Good to know**: `<a>` tag attributes such as `className` or `target="_blank"` can be added to `<Link>` as props and will be passed to the underlying `<a>` element.

### [`href` (required)](#href-required)

The path or URL to navigate to.

```
<Link href="/dashboard">Dashboard</Link>
```

`href` can also accept an object, for example:

```
// Navigate to /about?name=test
<Link
  href={{
    pathname: '/about',
    query: { name: 'test' },
  }}
>
  About
</Link>
```

### [`replace`](#replace)

**Defaults to `false`.** When `true`, `next/link` will replace the current history state instead of adding a new URL into the [browser’s history](https://developer.mozilla.org/docs/Web/API/History_API) stack.

app/page.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Page() {
  return (
    <Link href="/dashboard" replace>
      Dashboard
    </Link>
  )
}
```

### [`scroll`](#scroll)

**Defaults to `true`.** The default behavior of `<Link>` is to scroll to the top of a new route or to maintain the scroll position for backwards and forwards navigation. When `false`, `next/link` will *not* scroll to the top of the page after a navigation.

app/page.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Page() {
  return (
    <Link href="/dashboard" scroll={false}>
      Dashboard
    </Link>
  )
}
```

### [`prefetch`](#prefetch)

**Defaults to `true`.** When `true`, `next/link` will prefetch the page (denoted by the `href`) in the background. This is useful for improving the performance of client-side navigations. Any `<Link />` in the viewport (initially or through scroll) will be preloaded.

Prefetch can be disabled by passing `prefetch={false}`. Prefetching is only enabled in production.

app/page.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Page() {
  return (
    <Link href="/dashboard" prefetch={false}>
      Dashboard
    </Link>
  )
}
```

## [Examples](#examples)

### [Linking to Dynamic Routes](#linking-to-dynamic-routes)

For dynamic routes, it can be handy to use template literals to create the link's path.

For example, you can generate a list of links to the dynamic route `app/blog/[slug]/page.js`:

app/blog/page.js

```
import Link from 'next/link'
 
function Page({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>
          <Link href={`/blog/${post.slug}`}>{post.title}</Link>
        </li>
      ))}
    </ul>
  )
}
```

### [Middleware](#middleware)

It's common to use [Middleware](/docs/13/app/building-your-application/routing/middleware) for authentication or other purposes that involve rewriting the user to a different page. In order for the `<Link />` component to properly prefetch links with rewrites via Middleware, you need to tell Next.js both the URL to display and the URL to prefetch. This is required to avoid un-necessary fetches to middleware to know the correct route to prefetch.

For example, if you want to serve a `/dashboard` route that has authenticated and visitor views, you may add something similar to the following in your Middleware to redirect the user to the correct page:

middleware.js

```
export function middleware(req) {
  const nextUrl = req.nextUrl
  if (nextUrl.pathname === '/dashboard') {
    if (req.cookies.authToken) {
      return NextResponse.rewrite(new URL('/auth/dashboard', req.url))
    } else {
      return NextResponse.rewrite(new URL('/public/dashboard', req.url))
    }
  }
}
```

In this case, you would want to use the following code in your `<Link />` component:

```
import Link from 'next/link'
import useIsAuthed from './hooks/useIsAuthed'
 
export default function Page() {
  const isAuthed = useIsAuthed()
  const path = isAuthed ? '/auth/dashboard' : '/dashboard'
  return (
    <Link as="/dashboard" href={path}>
      Dashboard
    </Link>
  )
}
```

## [Version History](#version-history)

VersionChanges`v13.0.0`No longer requires a child `<a>` tag. A [codemod](/docs/13/app/building-your-application/upgrading/codemods#remove-a-tags-from-link-components) is provided to automatically update your codebase.`v10.0.0``href` props pointing to a dynamic route are automatically resolved and no longer require an `as` prop.`v8.0.0`Improved prefetching performance.`v1.0.0``next/link` introduced.

Was this helpful?

supported.

Send
