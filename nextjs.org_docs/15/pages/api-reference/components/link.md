---
title: "Link"
source: "https://nextjs.org/docs/15/pages/api-reference/components/link"
---

# Link

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[API Reference](/docs/15/pages/api-reference)[Components](/docs/15/pages/api-reference/components)Link

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# Link

`<Link>` is a React component that extends the HTML `<a>` element to provide [prefetching](/docs/15/app/getting-started/linking-and-navigating#prefetching) and client-side navigation between routes. It is the primary way to navigate between routes in Next.js.

Basic usage:

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Home() {
  return <Link href="/dashboard">Dashboard</Link>
}
```

## [Reference](#reference)

The following props can be passed to the `<Link>` component:

PropExampleTypeRequired[`href`](#href-required)`href="/dashboard"`String or ObjectYes[`as`](#as)`as="/post/abc"`String or Object-[`replace`](#replace)`replace={false}`Boolean-[`scroll`](#scroll)`scroll={false}`Boolean-[`prefetch`](#prefetch)`prefetch={false}`Boolean-[`legacyBehavior`](#legacybehavior)`legacyBehavior={true}`Boolean-[`passHref`](#passhref)`passHref={true}`Boolean-[`shallow`](#shallow)`shallow={false}`Boolean-[`locale`](#locale)`locale="fr"`String or Boolean-[`onNavigate`](#onnavigate)`onNavigate={(e) => {}}`Function-

> **Good to know**: `<a>` tag attributes such as `className` or `target="_blank"` can be added to `<Link>` as props and will be passed to the underlying `<a>` element.

### [`href` (required)](#href-required)

The path or URL to navigate to.

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
// Navigate to /about?name=test
export default function Home() {
  return (
    <Link
      href={{
        pathname: '/about',
        query: { name: 'test' },
      }}
    >
      About
    </Link>
  )
}
```

### [`replace`](#replace)

**Defaults to `false`.** When `true`, `next/link` will replace the current history state instead of adding a new URL into the [browser's history](https://developer.mozilla.org/docs/Web/API/History_API) stack.

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Home() {
  return (
    <Link href="/dashboard" replace>
      Dashboard
    </Link>
  )
}
```

### [`scroll`](#scroll)

**Defaults to `true`.** The default scrolling behavior of `<Link>` in Next.js **is to maintain scroll position**, similar to how browsers handle back and forwards navigation. When you navigate to a new [Page](/docs/15/app/api-reference/file-conventions/page), scroll position will stay the same as long as the Page is visible in the viewport. However, if the Page is not visible in the viewport, Next.js will scroll to the top of the first Page element.

When `scroll = {false}`, Next.js will not attempt to scroll to the first Page element.

> **Good to know**: Next.js checks if `scroll: false` before managing scroll behavior. If scrolling is enabled, it identifies the relevant DOM node for navigation and inspects each top-level element. All non-scrollable elements and those without rendered HTML are bypassed, this includes sticky or fixed positioned elements, and non-visible elements such as those calculated with `getBoundingClientRect`. Next.js then continues through siblings until it identifies a scrollable element that is visible in the viewport.

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Home() {
  return (
    <Link href="/dashboard" scroll={false}>
      Dashboard
    </Link>
  )
}
```

### [`prefetch`](#prefetch)

Prefetching happens when a `<Link />` component enters the user's viewport (initially or through scroll). Next.js prefetches and loads the linked route (denoted by the `href`) and data in the background to improve the performance of client-side navigation's. **Prefetching is only enabled in production**.

The following values can be passed to the `prefetch` prop:

- **`true` (default)**: The full route and its data will be prefetched.
- `false`: Prefetching will not happen when entering the viewport, but will happen on hover. If you want to completely remove fetching on hover as well, consider using an `<a>` tag or [incrementally adopting](/docs/15/app/guides/migrating/app-router-migration) the App Router, which enables disabling prefetching on hover too.

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Home() {
  return (
    <Link href="/dashboard" prefetch={false}>
      Dashboard
    </Link>
  )
}
```

### [`legacyBehavior`](#legacybehavior)

> **Warning**: The `legacyBehavior` prop will be removed in Next.js v16. To adopt the new `<Link>` behavior, remove any `<a>` tags used as children of `<Link>`. A [codemod is available](/docs/15/app/guides/upgrading/codemods#new-link) to help you automatically upgrade your codebase.

Since version 13, an `<a>` element is no longer required as a child of the `<Link>` component. If you still need the old behavior for compatibility reasons, you can add the `legacyBehavior` prop.

> **Good to know**: when `legacyBehavior` is not set to `true`, all [`anchor`](https://developer.mozilla.org/docs/Web/HTML/Element/a) tag properties can be passed to `next/link` as well such as, `className`, `onClick`, etc.

### [`passHref`](#passhref)

Forces `Link` to send the `href` property to its child. Defaults to `false`. See the [passing a functional component](#nesting-a-functional-component) example for more information.

### [`shallow`](#shallow)

Update the path of the current page without rerunning [`getStaticProps`](/docs/15/pages/building-your-application/data-fetching/get-static-props), [`getServerSideProps`](/docs/15/pages/building-your-application/data-fetching/get-server-side-props) or [`getInitialProps`](/docs/15/pages/api-reference/functions/get-initial-props). Defaults to `false`.

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Home() {
  return (
    <Link href="/dashboard" shallow={false}>
      Dashboard
    </Link>
  )
}
```

### [`locale`](#locale)

The active locale is automatically prepended. `locale` allows for providing a different locale. When `false` `href` has to include the locale as the default behavior is disabled.

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Home() {
  return (
    <>
      {/* Default behavior: locale is prepended */}
      <Link href="/dashboard">Dashboard (with locale)</Link>
 
      {/* Disable locale prepending */}
      <Link href="/dashboard" locale={false}>
        Dashboard (without locale)
      </Link>
 
      {/* Specify a different locale */}
      <Link href="/dashboard" locale="fr">
        Dashboard (French)
      </Link>
    </>
  )
}
```

### [`as`](#as)

Optional decorator for the path that will be shown in the browser URL bar. Before Next.js 9.5.3 this was used for dynamic routes, check our [previous docs](https://github.com/vercel/next.js/blob/v9.5.2/docs/api-reference/next/link.md#dynamic-routes) to see how it worked.

When this path differs from the one provided in `href` the previous `href`/`as` behavior is used as shown in the [previous docs](https://github.com/vercel/next.js/blob/v9.5.2/docs/api-reference/next/link.md#dynamic-routes).

### [`onNavigate`](#onnavigate)

An event handler called during client-side navigation. The handler receives an event object that includes a `preventDefault()` method, allowing you to cancel the navigation if needed.

app/page.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Page() {
  return (
    <Link
      href="/dashboard"
      onNavigate={(e) => {
        // Only executes during SPA navigation
        console.log('Navigating...')
 
        // Optionally prevent navigation
        // e.preventDefault()
      }}
    >
      Dashboard
    </Link>
  )
}
```

> **Good to know**: While `onClick` and `onNavigate` may seem similar, they serve different purposes. `onClick` executes for all click events, while `onNavigate` only runs during client-side navigation. Some key differences:
> 
> - When using modifier keys (`Ctrl`/`Cmd` + Click), `onClick` executes but `onNavigate` doesn't since Next.js prevents default navigation for new tabs.
> - External URLs won't trigger `onNavigate` since it's only for client-side and same-origin navigations.
> - Links with the `download` attribute will work with `onClick` but not `onNavigate` since the browser will treat the linked URL as a download.

## [Examples](#examples)

The following examples demonstrate how to use the `<Link>` component in different scenarios.

### [Linking to dynamic route segments](#linking-to-dynamic-route-segments-1)

For [dynamic route segments](/docs/15/pages/building-your-application/routing/dynamic-routes#convention), it can be handy to use template literals to create the link's path.

For example, you can generate a list of links to the dynamic route `pages/blog/[slug].js`

pages/blog/index.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
function Posts({ posts }) {
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

### [Scrolling to an `id`](#scrolling-to-an-id)

If you'd like to scroll to a specific `id` on navigation, you can append your URL with a `#` hash link or just pass a hash link to the `href` prop. This is possible since `<Link>` renders to an `<a>` element.

```
<Link href="/dashboard#settings">Settings</Link>
 
// Output
<a href="/dashboard#settings">Settings</a>
```

### [If the child is a custom component that wraps an `<a>` tag](#if-the-child-is-a-custom-component-that-wraps-an-a-tag)

If the child of `Link` is a custom component that wraps an `<a>` tag, you must add `passHref` to `Link`. This is necessary if you’re using libraries like [styled-components](https://styled-components.com/). Without this, the `<a>` tag will not have the `href` attribute, which hurts your site's accessibility and might affect SEO. If you're using [ESLint](/docs/15/pages/api-reference/config/eslint), there is a built-in rule `next/link-passhref` to ensure correct usage of `passHref`.

components/nav-link.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
import styled from 'styled-components'
 
// This creates a custom component that wraps an <a> tag
const RedLink = styled.a`
  color: red;
`
 
function NavLink({ href, name }) {
  return (
    <Link href={href} passHref legacyBehavior>
      <RedLink>{name}</RedLink>
    </Link>
  )
}
 
export default NavLink
```

- If you’re using [emotion](https://emotion.sh/)’s JSX pragma feature (`@jsx jsx`), you must use `passHref` even if you use an `<a>` tag directly.
- The component should support `onClick` property to trigger navigation correctly.

### [Nesting a functional component](#nesting-a-functional-component)

If the child of `Link` is a functional component, in addition to using `passHref` and `legacyBehavior`, you must wrap the component in [`React.forwardRef`](https://react.dev/reference/react/forwardRef):

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
import React from 'react'
 
// Define the props type for MyButton
interface MyButtonProps {
  onClick?: React.MouseEventHandler<HTMLAnchorElement>
  href?: string
}
 
// Use React.ForwardRefRenderFunction to properly type the forwarded ref
const MyButton: React.ForwardRefRenderFunction<
  HTMLAnchorElement,
  MyButtonProps
> = ({ onClick, href }, ref) => {
  return (
    <a href={href} onClick={onClick} ref={ref}>
      Click Me
    </a>
  )
}
 
// Use React.forwardRef to wrap the component
const ForwardedMyButton = React.forwardRef(MyButton)
 
export default function Home() {
  return (
    <Link href="/about" passHref legacyBehavior>
      <ForwardedMyButton />
    </Link>
  )
}
```

### [Passing a URL Object](#passing-a-url-object)

`Link` can also receive a URL object and it will automatically format it to create the URL string:

pages/index.ts

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
function Home() {
  return (
    <ul>
      <li>
        <Link
          href={{
            pathname: '/about',
            query: { name: 'test' },
          }}
        >
          About us
        </Link>
      </li>
      <li>
        <Link
          href={{
            pathname: '/blog/[slug]',
            query: { slug: 'my-post' },
          }}
        >
          Blog Post
        </Link>
      </li>
    </ul>
  )
}
 
export default Home
```

The above example has a link to:

- A predefined route: `/about?name=test`
- A [dynamic route](/docs/15/pages/building-your-application/routing/dynamic-routes#convention): `/blog/my-post`

You can use every property as defined in the [Node.js URL module documentation](https://nodejs.org/api/url.html#url_url_strings_and_url_objects).

### [Replace the URL instead of push](#replace-the-url-instead-of-push)

The default behavior of the `Link` component is to `push` a new URL into the `history` stack. You can use the `replace` prop to prevent adding a new entry, as in the following example:

pages/index.js

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Home() {
  return (
    <Link href="/about" replace>
      About us
    </Link>
  )
}
```

### [Disable scrolling to the top of the page](#disable-scrolling-to-the-top-of-the-page)

The default behavior of `Link` is to scroll to the top of the page. When there is a hash defined it will scroll to the specific id, like a normal `<a>` tag. To prevent scrolling to the top / hash `scroll={false}` can be added to `Link`:

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Home() {
  return (
    <Link href="/#hashid" scroll={false}>
      Disables scrolling to the top
    </Link>
  )
}
```

### [Prefetching links in Middleware](#prefetching-links-in-middleware)

It's common to use [Middleware](/docs/15/app/api-reference/file-conventions/middleware) for authentication or other purposes that involve rewriting the user to a different page. In order for the `<Link />` component to properly prefetch links with rewrites via Middleware, you need to tell Next.js both the URL to display and the URL to prefetch. This is required to avoid un-necessary fetches to middleware to know the correct route to prefetch.

For example, if you want to serve a `/dashboard` route that has authenticated and visitor views, you can add the following in your Middleware to redirect the user to the correct page:

middleware.ts

TypeScript

JavaScriptTypeScript

```
import { NextResponse } from 'next/server'
 
export function middleware(request: Request) {
  const nextUrl = request.nextUrl
  if (nextUrl.pathname === '/dashboard') {
    if (request.cookies.authToken) {
      return NextResponse.rewrite(new URL('/auth/dashboard', request.url))
    } else {
      return NextResponse.rewrite(new URL('/public/dashboard', request.url))
    }
  }
}
```

In this case, you would want to use the following code in your `<Link />` component:

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
'use client'
 
import Link from 'next/link'
import useIsAuthed from './hooks/useIsAuthed' // Your auth hook
 
export default function Home() {
  const isAuthed = useIsAuthed()
  const path = isAuthed ? '/auth/dashboard' : '/public/dashboard'
  return (
    <Link as="/dashboard" href={path}>
      Dashboard
    </Link>
  )
}
```

> **Good to know**: If you're using [Dynamic Routes](/docs/15/pages/building-your-application/routing/dynamic-routes#convention), you'll need to adapt your `as` and `href` props. For example, if you have a Dynamic Route like `/dashboard/authed/[user]` that you want to present differently via middleware, you would write: `<Link href={{ pathname: '/dashboard/authed/[user]', query: { user: username } }} as="/dashboard/[user]">Profile</Link>`.

## [Version history](#version-history)

VersionChanges`v15.4.0`Add `auto` as an alias to the default `prefetch` behavior.`v15.3.0`Add `onNavigate` API`v13.0.0`No longer requires a child `<a>` tag. A [codemod](/docs/15/app/guides/upgrading/codemods#remove-a-tags-from-link-components) is provided to automatically update your codebase.`v10.0.0``href` props pointing to a dynamic route are automatically resolved and no longer require an `as` prop.`v8.0.0`Improved prefetching performance.`v1.0.0``next/link` introduced.

Was this helpful?

supported.

Send
