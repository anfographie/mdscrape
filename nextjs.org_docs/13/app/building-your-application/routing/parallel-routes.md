---
title: "Parallel Routes"
source: "https://nextjs.org/docs/13/app/building-your-application/routing/parallel-routes"
---

# Parallel Routes

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[Building Your Application](/docs/13/app/building-your-application)[Routing](/docs/13/app/building-your-application/routing)Parallel Routes

You are currently viewing documentation for version 13 of Next.js.

# Parallel Routes

Parallel Routing allows you to simultaneously or conditionally render one or more pages in the same layout. For highly dynamic sections of an app, such as dashboards and feeds on social sites, Parallel Routing can be used to implement complex routing patterns.

For example, you can simultaneously render the team and analytics pages.

![Parallel Routes Diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes.png&w=3840&q=75)![Parallel Routes Diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes.png&w=3840&q=75)

Parallel Routing allows you to define independent error and loading states for each route as they're being streamed in independently.

![Parallel routes enable custom error and loading states](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes-cinematic-universe.png&w=3840&q=75)![Parallel routes enable custom error and loading states](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-cinematic-universe.png&w=3840&q=75)

Parallel Routing also allows you to conditionally render a slot based on certain conditions, such as authentication state. This enables fully separated code on the same URL.

![Conditional routes diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fconditional-routes-ui.png&w=3840&q=75)![Conditional routes diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fconditional-routes-ui.png&w=3840&q=75)

## [Convention](#convention)

Parallel routes are created using named **slots**. Slots are defined with the `@folder` convention, and are passed to the same-level layout as props.

> Slots are *not* route segments and *do not affect the URL structure*. The file path `/@team/members` would be accessible at `/members`.

For example, the following file structure defines two explicit slots: `@analytics` and `@team`.

![Parallel Routes File-system Structure](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes-file-system.png&w=3840&q=75)![Parallel Routes File-system Structure](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-file-system.png&w=3840&q=75)

The folder structure above means that the component in `app/layout.js` now accepts the `@analytics` and `@team` slots props, and can render them in parallel alongside the `children` prop:

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
export default function Layout(props: {
  children: React.ReactNode
  analytics: React.ReactNode
  team: React.ReactNode
}) {
  return (
    <>
      {props.children}
      {props.team}
      {props.analytics}
    </>
  )
}
```

> **Good to know**: The `children` prop is an implicit slot that does not need to be mapped to a folder. This means `app/page.js` is equivalent to `app/@children/page.js`.

## [Unmatched Routes](#unmatched-routes)

By default, the content rendered within a slot will match the current URL.

In the case of an unmatched slot, the content that Next.js renders differs based on the routing technique and folder structure.

### [`default.js`](#defaultjs)

You can define a `default.js` file to render as a fallback when Next.js cannot recover a slot's active state based on the current URL.

Consider the following folder structure. The `@team` slot has a `settings` directory, but `@analytics` does not.

![Parallel Routes unmatched routes](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes-unmatched-routes.png&w=3840&q=75)![Parallel Routes unmatched routes](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-unmatched-routes.png&w=3840&q=75)

#### [Navigation](#navigation)

On navigation, Next.js will render the slot's previously active state, even if it doesn't match the current URL.

#### [Reload](#reload)

On reload, Next.js will first try to render the unmatched slot's `default.js` file. If that's not available, a 404 gets rendered.

> The 404 for unmatched routes helps ensure that you don't accidentally render a route that shouldn't be parallel rendered.

## [`useSelectedLayoutSegment(s)`](#useselectedlayoutsegments)

Both [`useSelectedLayoutSegment`](/docs/13/app/api-reference/functions/use-selected-layout-segment) and [`useSelectedLayoutSegments`](/docs/13/app/api-reference/functions/use-selected-layout-segments) accept a `parallelRoutesKey`, which allows you read the active route segment within that slot.

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
'use client'
 
import { useSelectedLayoutSegment } from 'next/navigation'
 
export default async function Layout(props: {
  //...
  auth: React.ReactNode
}) {
  const loginSegments = useSelectedLayoutSegment('auth')
  // ...
}
```

When a user navigates to `@auth/login`, or `/login` in the URL bar, `loginSegments` will be equal to the string `"login"`.

## [Examples](#examples)

### [Modals](#modals)

Parallel Routing can be used to render modals.

![Parallel Routes Diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes-auth-modal.png&w=3840&q=75)![Parallel Routes Diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-auth-modal.png&w=3840&q=75)

The `@auth` slot renders a `<Modal>` component that can be shown by navigating to a matching route, for example `/login`.

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
export default async function Layout(props: {
  // ...
  auth: React.ReactNode
}) {
  return (
    <>
      {/* ... */}
      {props.auth}
    </>
  )
}
```

app/@auth/login/page.tsx

TypeScript

JavaScriptTypeScript

```
import { Modal } from 'components/modal'
 
export default function Login() {
  return (
    <Modal>
      <h1>Login</h1>
      {/* ... */}
    </Modal>
  )
}
```

To ensure that the contents of the modal don't get rendered when it's not active, you can create a `default.js` file that returns `null`.

app/@auth/default.tsx

TypeScript

JavaScriptTypeScript

```
export default function Default() {
  return null
}
```

#### [Dismissing a modal](#dismissing-a-modal)

If a modal was initiated through client navigation, e.g. by using `<Link href="/login">`, you can dismiss the modal by calling `router.back()` or by using a `Link` component.

app/@auth/login/page.tsx

TypeScript

JavaScriptTypeScript

```
'use client'
import { useRouter } from 'next/navigation'
import { Modal } from 'components/modal'
 
export default async function Login() {
  const router = useRouter()
  return (
    <Modal>
      <span onClick={() => router.back()}>Close modal</span>
      <h1>Login</h1>
      ...
    </Modal>
  )
}
```

> More information on modals is covered in the [Intercepting Routes](/docs/13/app/building-your-application/routing/intercepting-routes) section.

If you want to navigate elsewhere and dismiss a modal, you can also use a catch-all route.

![Parallel Routes Diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes-catchall.png&w=3840&q=75)![Parallel Routes Diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-catchall.png&w=3840&q=75)

app/@auth/\[...catchAll]/page.tsx

TypeScript

JavaScriptTypeScript

```
export default function CatchAll() {
  return null
}
```

> Catch-all routes take precedence over `default.js`.

### [Conditional Routes](#conditional-routes)

Parallel Routes can be used to implement conditional routing. For example, you can render a `@dashboard` or `@login` route depending on the authentication state.

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
import { getUser } from '@/lib/auth'
 
export default function Layout({
  dashboard,
  login,
}: {
  dashboard: React.ReactNode
  login: React.ReactNode
}) {
  const isLoggedIn = getUser()
  return isLoggedIn ? dashboard : login
}
```

![Parallel routes authentication example](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fconditional-routes-ui.png&w=3840&q=75)![Parallel routes authentication example](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fconditional-routes-ui.png&w=3840&q=75)

Was this helpful?

supported.

Send
