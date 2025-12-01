---
title: "Parallel Routes"
source: "https://nextjs.org/docs/14/app/building-your-application/routing/parallel-routes"
---

# Parallel Routes

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[Building Your Application](/docs/14/app/building-your-application)[Routing](/docs/14/app/building-your-application/routing)Parallel Routes

You are currently viewing documentation for version 14 of Next.js.

# Parallel Routes

Parallel Routes allows you to simultaneously or conditionally render one or more pages within the same layout. They are useful for highly dynamic sections of an app, such as dashboards and feeds on social sites.

For example, considering a dashboard, you can use parallel routes to simultaneously render the `team` and `analytics` pages:

![Parallel Routes Diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes.png&w=3840&q=75)![Parallel Routes Diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes.png&w=3840&q=75)

## [Slots](#slots)

Parallel routes are created using named **slots**. Slots are defined with the `@folder` convention. For example, the following file structure defines two slots: `@analytics` and `@team`:

![Parallel Routes File-system Structure](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes-file-system.png&w=3840&q=75)![Parallel Routes File-system Structure](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-file-system.png&w=3840&q=75)

Slots are passed as props to the shared parent layout. For the example above, the component in `app/layout.js` now accepts the `@analytics` and `@team` slots props, and can render them in parallel alongside the `children` prop:

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
export default function Layout({
  children,
  team,
  analytics,
}: {
  children: React.ReactNode
  analytics: React.ReactNode
  team: React.ReactNode
}) {
  return (
    <>
      {children}
      {team}
      {analytics}
    </>
  )
}
```

However, slots are **not** [route segments](/docs/14/app/building-your-application/routing#route-segments) and do not affect the URL structure. For example, for `/@analytics/views`, the URL will be `/views` since `@analytics` is a slot.

> **Good to know**:
> 
> - The `children` prop is an implicit slot that does not need to be mapped to a folder. This means `app/page.js` is equivalent to `app/@children/page.js`.

## [Active state and navigation](#active-state-and-navigation)

By default, Next.js keeps track of the active *state* (or subpage) for each slot. However, the content rendered within a slot will depend on the type of navigation:

- [**Soft Navigation**](/docs/14/app/building-your-application/routing/linking-and-navigating#5-soft-navigation): During client-side navigation, Next.js will perform a [partial render](/docs/14/app/building-your-application/routing/linking-and-navigating#4-partial-rendering), changing the subpage within the slot, while maintaining the other slot's active subpages, even if they don't match the current URL.
- **Hard Navigation**: After a full-page load (browser refresh), Next.js cannot determine the active state for the slots that don't match the current URL. Instead, it will render a [`default.js`](#defaultjs) file for the unmatched slots, or `404` if `default.js` doesn't exist.

> **Good to know**:
> 
> - The `404` for unmatched routes helps ensure that you don't accidentally render a parallel route on a page that it was not intended for.

### [`default.js`](#defaultjs)

You can define a `default.js` file to render as a fallback for unmatched slots during the initial load or full-page reload.

Consider the following folder structure. The `@team` slot has a `/settings` page, but `@analytics` does not.

![Parallel Routes unmatched routes](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes-unmatched-routes.png&w=3840&q=75)![Parallel Routes unmatched routes](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-unmatched-routes.png&w=3840&q=75)

When navigating to `/settings`, the `@team` slot will render the `/settings` page while maintaining the currently active page for the `@analytics` slot.

On refresh, Next.js will render a `default.js` for `@analytics`. If `default.js` doesn't exist, a `404` is rendered instead.

Additionally, since `children` is an implicit slot, you also need to create a `default.js` file to render a fallback for `children` when Next.js cannot recover the active state of the parent page.

### [`useSelectedLayoutSegment(s)`](#useselectedlayoutsegments)

Both [`useSelectedLayoutSegment`](/docs/14/app/api-reference/functions/use-selected-layout-segment) and [`useSelectedLayoutSegments`](/docs/14/app/api-reference/functions/use-selected-layout-segments) accept a `parallelRoutesKey` parameter, which allows you to read the active route segment within a slot.

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
'use client'
 
import { useSelectedLayoutSegment } from 'next/navigation'
 
export default function Layout({ auth }: { auth: React.ReactNode }) {
  const loginSegment = useSelectedLayoutSegment('auth')
  // ...
}
```

When a user navigates to `app/@auth/login` (or `/login` in the URL bar), `loginSegment` will be equal to the string `"login"`.

## [Examples](#examples)

### [Conditional Routes](#conditional-routes)

You can use Parallel Routes to conditionally render routes based on certain conditions, such as user role. For example, to render a different dashboard page for the `/admin` or `/user` roles:

![Conditional routes diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fconditional-routes-ui.png&w=3840&q=75)![Conditional routes diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fconditional-routes-ui.png&w=3840&q=75)

app/dashboard/layout.tsx

TypeScript

JavaScriptTypeScript

```
import { checkUserRole } from '@/lib/auth'
 
export default function Layout({
  user,
  admin,
}: {
  user: React.ReactNode
  admin: React.ReactNode
}) {
  const role = checkUserRole()
  return <>{role === 'admin' ? admin : user}</>
}
```

### [Tab Groups](#tab-groups)

You can add a `layout` inside a slot to allow users to navigate the slot independently. This is useful for creating tabs.

For example, the `@analytics` slot has two subpages: `/page-views` and `/visitors`.

![Analytics slot with two subpages and a layout](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes-tab-groups.png&w=3840&q=75)![Analytics slot with two subpages and a layout](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-tab-groups.png&w=3840&q=75)

Within `@analytics`, create a [`layout`](/docs/14/app/building-your-application/routing/pages-and-layouts) file to share the tabs between the two pages:

app/@analytics/layout.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <>
      <nav>
        <Link href="/page-views">Page Views</Link>
        <Link href="/visitors">Visitors</Link>
      </nav>
      <div>{children}</div>
    </>
  )
}
```

### [Modals](#modals)

Parallel Routes can be used together with [Intercepting Routes](/docs/14/app/building-your-application/routing/intercepting-routes) to create modals. This allows you to solve common challenges when building modals, such as:

- Making the modal content **shareable through a URL**.
- **Preserving context** when the page is refreshed, instead of closing the modal.
- **Closing the modal on backwards navigation** rather than going to the previous route.
- **Reopening the modal on forwards navigation**.

Consider the following UI pattern, where a user can open a login modal from a layout using client-side navigation, or access a separate `/login` page:

![Parallel Routes Diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes-auth-modal.png&w=3840&q=75)![Parallel Routes Diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-auth-modal.png&w=3840&q=75)

To implement this pattern, start by creating a `/login` route that renders your **main** login page.

![Parallel Routes Diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes-modal-login-page.png&w=3840&q=75)![Parallel Routes Diagram](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-modal-login-page.png&w=3840&q=75)

app/login/page.tsx

TypeScript

JavaScriptTypeScript

```
import { Login } from '@/app/ui/login'
 
export default function Page() {
  return <Login />
}
```

Then, inside the `@auth` slot, add [`default.js`](/docs/14/app/api-reference/file-conventions/default) file that returns `null`. This ensures that the modal is not rendered when it's not active.

app/@auth/default.tsx

TypeScript

JavaScriptTypeScript

```
export default function Default() {
  return null
}
```

Inside your `@auth` slot, intercept the `/login` route by updating the `/(.)login` folder. Import the `<Modal>` component and its children into the `/(.)login/page.tsx` file:

app/@auth/(.)login/page.tsx

TypeScript

JavaScriptTypeScript

```
import { Modal } from '@/app/ui/modal'
import { Login } from '@/app/ui/login'
 
export default function Page() {
  return (
    <Modal>
      <Login />
    </Modal>
  )
}
```

> **Good to know:**
> 
> - The convention used to intercept the route, e.g. `(.)`, depends on your file-system structure. See [Intercepting Routes convention](/docs/14/app/building-your-application/routing/intercepting-routes#convention).
> - By separating the `<Modal>` functionality from the modal content (`<Login>`), you can ensure any content inside the modal, e.g. [forms](/docs/14/app/building-your-application/data-fetching/server-actions-and-mutations#forms), are Server Components. See [Interleaving Client and Server Components](/docs/14/app/building-your-application/rendering/composition-patterns#supported-pattern-passing-server-components-to-client-components-as-props) for more information.

#### [Opening the modal](#opening-the-modal)

Now, you can leverage the Next.js router to open and close the modal. This ensures the URL is correctly updated when the modal is open, and when navigating backwards and forwards.

To open the modal, pass the `@auth` slot as a prop to the parent layout and render it alongside the `children` prop.

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Layout({
  auth,
  children,
}: {
  auth: React.ReactNode
  children: React.ReactNode
}) {
  return (
    <>
      <nav>
        <Link href="/login">Open modal</Link>
      </nav>
      <div>{auth}</div>
      <div>{children}</div>
    </>
  )
}
```

When the user clicks the `<Link>`, the modal will open instead of navigating to the `/login` page. However, on refresh or initial load, navigating to `/login` will take the user to the main login page.

#### [Closing the modal](#closing-the-modal)

You can close the modal by calling `router.back()` or by using the `Link` component.

app/ui/modal.tsx

TypeScript

JavaScriptTypeScript

```
'use client'
 
import { useRouter } from 'next/navigation'
 
export function Modal({ children }: { children: React.ReactNode }) {
  const router = useRouter()
 
  return (
    <>
      <button
        onClick={() => {
          router.back()
        }}
      >
        Close modal
      </button>
      <div>{children}</div>
    </>
  )
}
```

When using the `Link` component to navigate away from a page that shouldn't render the `@auth` slot anymore, we use a catch-all route that returns `null`.

app/ui/modal.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export function Modal({ children }: { children: React.ReactNode }) {
  return (
    <>
      <Link href="/">Close modal</Link>
      <div>{children}</div>
    </>
  )
}
```

app/@auth/\[...catchAll]/page.tsx

TypeScript

JavaScriptTypeScript

```
export default function CatchAll() {
  return null
}
```

> **Good to know:**
> 
> - We use a catch-all route in our `@auth` slot to close the modal because of the behavior described in [Active state and navigation](#active-state-and-navigation). Since client-side navigations to a route that no longer match the slot will remain visible, we need to match the slot to a route that returns `null` to close the modal.
> - Other examples could include opening a photo modal in a gallery while also having a dedicated `/photo/[id]` page, or opening a shopping cart in a side modal.
> - [View an example](https://github.com/vercel-labs/nextgram) of modals with Intercepted and Parallel Routes.

### [Loading and Error UI](#loading-and-error-ui)

Parallel Routes can be streamed independently, allowing you to define independent error and loading states for each route:

![Parallel routes enable custom error and loading states](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Fparallel-routes-cinematic-universe.png&w=3840&q=75)![Parallel routes enable custom error and loading states](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-cinematic-universe.png&w=3840&q=75)

See the [Loading UI](/docs/14/app/building-your-application/routing/loading-ui-and-streaming) and [Error Handling](/docs/14/app/building-your-application/routing/error-handling) documentation for more information.

## Next Steps

[Introduction  
\
...  
\
File Conventions  
\
**default.js**  
\
API Reference for the default.js file.](/docs/14/app/api-reference/file-conventions/default)

Was this helpful?

supported.

Send
