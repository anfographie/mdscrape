---
title: "TypeScript"
source: "https://nextjs.org/docs/15/pages/api-reference/config/typescript"
---

# TypeScript

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[API Reference](/docs/15/pages/api-reference)[Configuration](/docs/15/pages/api-reference/config)TypeScript

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# TypeScript

Next.js comes with built-in TypeScript, automatically installing the necessary packages and configuring the proper settings when you create a new project with `create-next-app`.

To add TypeScript to an existing project, rename a file to `.ts` / `.tsx`. Run `next dev` and `next build` to automatically install the necessary dependencies and add a `tsconfig.json` file with the recommended config options.

> **Good to know**: If you already have a `jsconfig.json` file, copy the `paths` compiler option from the old `jsconfig.json` into the new `tsconfig.json` file, and delete the old `jsconfig.json` file.

## [Examples](#examples)

### [Type checking `next.config.ts`](#type-checking-nextconfigts)

You can use TypeScript and import types in your Next.js configuration by using `next.config.ts`.

next.config.ts

```
import type { NextConfig } from 'next'
 
const nextConfig: NextConfig = {
  /* config options here */
}
 
export default nextConfig
```

> **Good to know**: Module resolution in `next.config.ts` is currently limited to `CommonJS`. This may cause incompatibilities with ESM only packages being loaded in `next.config.ts`.

When using the `next.config.js` file, you can add some type checking in your IDE using JSDoc as below:

next.config.js

```
// @ts-check
 
/** @type {import('next').NextConfig} */
const nextConfig = {
  /* config options here */
}
 
module.exports = nextConfig
```

### [Statically Typed Links](#statically-typed-links)

Next.js can statically type links to prevent typos and other errors when using `next/link`, improving type safety when navigating between pages.

Works in both the Pages and App Router for the `href` prop in `next/link`. In the App Router, it also types `next/navigation` methods like `push`, `replace`, and `prefetch`. It does not type `next/router` methods in Pages Router.

Literal `href` strings are validated, while non-literal `href`s may require a cast with `as Route`.

To opt-into this feature, `typedRoutes` need to be enabled and the project needs to be using TypeScript.

next.config.ts

```
import type { NextConfig } from 'next'
 
const nextConfig: NextConfig = {
  typedRoutes: true,
}
 
export default nextConfig
```

Next.js will generate a link definition in `.next/types` that contains information about all existing routes in your application, which TypeScript can then use to provide feedback in your editor about invalid links.

> **Good to know**: If you set up your project without `create-next-app`, ensure the generated Next.js types are included by adding `.next/types/**/*.ts` to the `include` array in your `tsconfig.json`:

tsconfig.json

```
{
  "include": [
    "next-env.d.ts",
    ".next/types/**/*.ts",
    "**/*.ts",
    "**/*.tsx"
  ],
  "exclude": ["node_modules"]
}
```

Currently, support includes any string literal, including dynamic segments. For non-literal strings, you need to manually cast with `as Route`. The example below shows both `next/link` and `next/navigation` usage:

app/example-client.tsx

```
'use client'
 
import type { Route } from 'next'
import Link from 'next/link'
import { useRouter } from 'next/navigation'
 
export default function Example() {
  const router = useRouter()
  const slug = 'nextjs'
 
  return (
    <>
      {/* Link: literal and dynamic */}
      <Link href="/about" />
      <Link href={`/blog/${slug}`} />
      <Link href={('/blog/' + slug) as Route} />
      {/* TypeScript error if href is not a valid route */}
      <Link href="/aboot" />
 
      {/* Router: literal and dynamic strings are validated */}
      <button onClick={() => router.push('/about')}>Push About</button>
      <button onClick={() => router.replace(`/blog/${slug}`)}>
        Replace Blog
      </button>
      <button onClick={() => router.prefetch('/contact')}>
        Prefetch Contact
      </button>
 
      {/* For non-literal strings, cast to Route */}
      <button onClick={() => router.push(('/blog/' + slug) as Route)}>
        Push Non-literal Blog
      </button>
    </>
  )
}
```

The same applies for redirecting routes defined by middleware:

middleware.ts

```
import { NextRequest, NextResponse } from 'next/server'
 
export function middleware(request: NextRequest) {
  if (request.nextUrl.pathname === '/middleware-redirect') {
    return NextResponse.redirect(new URL('/', request.url))
  }
 
  return NextResponse.next()
}
```

app/some/page.tsx

```
import type { Route } from 'next'
 
export default function Page() {
  return <Link href={'/middleware-redirect' as Route}>Link Text</Link>
}
```

To accept `href` in a custom component wrapping `next/link`, use a generic:

```
import type { Route } from 'next'
import Link from 'next/link'
 
function Card<T extends string>({ href }: { href: Route<T> | URL }) {
  return (
    <Link href={href}>
      <div>My Card</div>
    </Link>
  )
}
```

You can also type a simple data structure and iterate to render links:

components/nav-items.ts

```
import type { Route } from 'next'
 
type NavItem<T extends string = string> = {
  href: T
  label: string
}
 
export const navItems: NavItem<Route>[] = [
  { href: '/', label: 'Home' },
  { href: '/about', label: 'About' },
  { href: '/blog', label: 'Blog' },
]
```

Then, map over the items to render `Link`s:

components/nav.tsx

```
import Link from 'next/link'
import { navItems } from './nav-items'
 
export function Nav() {
  return (
    <nav>
      {navItems.map((item) => (
        <Link key={item.href} href={item.href}>
          {item.label}
        </Link>
      ))}
    </nav>
  )
}
```

> **How does it work?**
> 
> When running `next dev` or `next build`, Next.js generates a hidden `.d.ts` file inside `.next` that contains information about all existing routes in your application (all valid routes as the `href` type of `Link`). This `.d.ts` file is included in `tsconfig.json` and the TypeScript compiler will check that `.d.ts` and provide feedback in your editor about invalid links.

### [Type IntelliSense for Environment Variables](#type-intellisense-for-environment-variables)

During development, Next.js generates a `.d.ts` file in `.next/types` that contains information about the loaded environment variables for your editor's IntelliSense. If the same environment variable key is defined in multiple files, it is deduplicated according to the [Environment Variable Load Order](/docs/15/app/guides/environment-variables#environment-variable-load-order).

To opt-into this feature, `experimental.typedEnv` needs to be enabled and the project needs to be using TypeScript.

next.config.ts

```
import type { NextConfig } from 'next'
 
const nextConfig: NextConfig = {
  experimental: {
    typedEnv: true,
  },
}
 
export default nextConfig
```

> **Good to know**: Types are generated based on the environment variables loaded at development runtime, which excludes variables from `.env.production*` files by default. To include production-specific variables, run `next dev` with `NODE_ENV=production`.

### [Static Generation and Server-side Rendering](#static-generation-and-server-side-rendering)

For [`getStaticProps`](/docs/15/pages/api-reference/functions/get-static-props), [`getStaticPaths`](/docs/15/pages/api-reference/functions/get-static-paths), and [`getServerSideProps`](/docs/15/pages/api-reference/functions/get-server-side-props), you can use the `GetStaticProps`, `GetStaticPaths`, and `GetServerSideProps` types respectively:

pages/blog/\[slug].tsx

```
import type { GetStaticProps, GetStaticPaths, GetServerSideProps } from 'next'
 
export const getStaticProps = (async (context) => {
  // ...
}) satisfies GetStaticProps
 
export const getStaticPaths = (async () => {
  // ...
}) satisfies GetStaticPaths
 
export const getServerSideProps = (async (context) => {
  // ...
}) satisfies GetServerSideProps
```

> **Good to know:** `satisfies` was added to TypeScript in [4.9](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-9.html). We recommend upgrading to the latest version of TypeScript.

### [With API Routes](#with-api-routes)

The following is an example of how to use the built-in types for API routes:

pages/api/hello.ts

```
import type { NextApiRequest, NextApiResponse } from 'next'
 
export default function handler(req: NextApiRequest, res: NextApiResponse) {
  res.status(200).json({ name: 'John Doe' })
}
```

You can also type the response data:

pages/api/hello.ts

```
import type { NextApiRequest, NextApiResponse } from 'next'
 
type Data = {
  name: string
}
 
export default function handler(
  req: NextApiRequest,
  res: NextApiResponse<Data>
) {
  res.status(200).json({ name: 'John Doe' })
}
```

### [With custom `App`](#with-custom-app)

If you have a [custom `App`](/docs/15/pages/building-your-application/routing/custom-app), you can use the built-in type `AppProps` and change file name to `./pages/_app.tsx` like so:

```
import type { AppProps } from 'next/app'
 
export default function MyApp({ Component, pageProps }: AppProps) {
  return <Component {...pageProps} />
}
```

### [Incremental type checking](#incremental-type-checking)

Since `v10.2.1` Next.js supports [incremental type checking](https://www.typescriptlang.org/tsconfig#incremental) when enabled in your `tsconfig.json`, this can help speed up type checking in larger applications.

### [Custom `tsconfig` path](#custom-tsconfig-path)

In some cases, you might want to use a different TypeScript configuration for builds or tooling. To do that, set `typescript.tsconfigPath` in `next.config.ts` to point Next.js to another `tsconfig` file.

next.config.ts

```
import type { NextConfig } from 'next'
 
const nextConfig: NextConfig = {
  typescript: {
    tsconfigPath: 'tsconfig.build.json',
  },
}
 
export default nextConfig
```

For example, switch to a different config for production builds:

next.config.ts

```
import type { NextConfig } from 'next'
 
const isProd = process.env.NODE_ENV === 'production'
 
const nextConfig: NextConfig = {
  typescript: {
    tsconfigPath: isProd ? 'tsconfig.build.json' : 'tsconfig.json',
  },
}
 
export default nextConfig
```

Why you might use a separate `tsconfig` for builds

You might need to relax checks in scenarios like monorepos, where the build also validates shared dependencies that don't match your project's standards, or when loosening checks in CI to continue delivering while migrating locally to stricter TypeScript settings (and still wanting your IDE to highlight misuse).

For example, if your project uses `useUnknownInCatchVariables` but some monorepo dependencies still assume `any`:

tsconfig.build.json

```
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "useUnknownInCatchVariables": false
  }
}
```

This keeps your editor strict via `tsconfig.json` while allowing the production build to use relaxed settings.

> **Good to know**:
> 
> - IDEs typically read `tsconfig.json` for diagnostics and IntelliSense, so you can still see IDE warnings while production builds use the alternate config. Mirror critical options if you want parity in the editor.
> - In development, only `tsconfig.json` is watched for changes. If you edit a different file name via `typescript.tsconfigPath`, restart the dev server to apply changes.
> - The configured file is used in `next dev`, `next build`, `next lint`, and `next typegen`.

### [Disabling TypeScript errors in production](#disabling-typescript-errors-in-production)

Next.js fails your **production build** (`next build`) when TypeScript errors are present in your project.

If you'd like Next.js to dangerously produce production code even when your application has errors, you can disable the built-in type checking step.

If disabled, be sure you are running type checks as part of your build or deploy process, otherwise this can be very dangerous.

Open `next.config.ts` and enable the `ignoreBuildErrors` option in the `typescript` config:

next.config.ts

```
import type { NextConfig } from 'next'
 
const nextConfig: NextConfig = {
  typescript: {
    // !! WARN !!
    // Dangerously allow production builds to successfully complete even if
    // your project has type errors.
    // !! WARN !!
    ignoreBuildErrors: true,
  },
}
 
export default nextConfig
```

> **Good to know**: You can run `tsc --noEmit` to check for TypeScript errors yourself before building. This is useful for CI/CD pipelines where you'd like to check for TypeScript errors before deploying.

### [Custom type declarations](#custom-type-declarations)

When you need to declare custom types, you might be tempted to modify `next-env.d.ts`. However, this file is automatically generated, so any changes you make will be overwritten. Instead, you should create a new file, let's call it `new-types.d.ts`, and reference it in your `tsconfig.json`:

tsconfig.json

```
{
  "compilerOptions": {
    "skipLibCheck": true
    //...truncated...
  },
  "include": [
    "new-types.d.ts",
    "next-env.d.ts",
    ".next/types/**/*.ts",
    "**/*.ts",
    "**/*.tsx"
  ],
  "exclude": ["node_modules"]
}
```

## [Version Changes](#version-changes)

VersionChanges`v15.0.0`[`next.config.ts`](#type-checking-nextconfigts) support added for TypeScript projects.`v13.2.0`Statically typed links are available in beta.`v12.0.0`[SWC](/docs/15/architecture/nextjs-compiler) is now used by default to compile TypeScript and TSX for faster builds.`v10.2.1`[Incremental type checking](https://www.typescriptlang.org/tsconfig#incremental) support added when enabled in your `tsconfig.json`.

Was this helpful?

supported.

Send
