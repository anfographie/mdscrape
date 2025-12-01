---
title: "generateViewport"
source: "https://nextjs.org/docs/14/app/api-reference/functions/generate-viewport"
---

# generateViewport

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[Functions](/docs/14/app/api-reference/functions)generateViewport

You are currently viewing documentation for version 14 of Next.js.

# generateViewport

You can customize the initial viewport of the page with the static `viewport` object or the dynamic `generateViewport` function.

> **Good to know**:
> 
> - The `viewport` object and `generateViewport` function exports are **only supported in Server Components**.
> - You cannot export both the `viewport` object and `generateViewport` function from the same route segment.
> - If you're coming from migrating `metadata` exports, you can use [metadata-to-viewport-export codemod](/docs/14/app/building-your-application/upgrading/codemods#metadata-to-viewport-export) to update your changes.

## [The `viewport` object](#the-viewport-object)

To define the viewport options, export a `viewport` object from a `layout.jsx` or `page.jsx` file.

layout.tsx | page.tsx

TypeScript

JavaScriptTypeScript

```
import type { Viewport } from 'next'
 
export const viewport: Viewport = {
  themeColor: 'black',
}
 
export default function Page() {}
```

## [`generateViewport` function](#generateviewport-function)

`generateViewport` should return a [`Viewport` object](#viewport-fields) containing one or more viewport fields.

layout.tsx | page.tsx

TypeScript

JavaScriptTypeScript

```
export function generateViewport({ params }) {
  return {
    themeColor: '...',
  }
}
```

> **Good to know**:
> 
> - If the viewport doesn't depend on runtime information, it should be defined using the static [`viewport` object](#the-viewport-object) rather than `generateMetadata`.

## [Viewport Fields](#viewport-fields)

### [`themeColor`](#themecolor)

Learn more about [`theme-color`](https://developer.mozilla.org/docs/Web/HTML/Element/meta/name/theme-color).

**Simple theme color**

layout.tsx | page.tsx

TypeScript

JavaScriptTypeScript

```
import type { Viewport } from 'next'
 
export const viewport: Viewport = {
  themeColor: 'black',
}
```

&lt;head&gt; output

```
<meta name="theme-color" content="black" />
```

**With media attribute**

layout.tsx | page.tsx

TypeScript

JavaScriptTypeScript

```
import type { Viewport } from 'next'
 
export const viewport: Viewport = {
  themeColor: [
    { media: '(prefers-color-scheme: light)', color: 'cyan' },
    { media: '(prefers-color-scheme: dark)', color: 'black' },
  ],
}
```

&lt;head&gt; output

```
<meta name="theme-color" media="(prefers-color-scheme: light)" content="cyan" />
<meta name="theme-color" media="(prefers-color-scheme: dark)" content="black" />
```

### [`width`, `initialScale`, `maximumScale` and `userScalable`](#width-initialscale-maximumscale-and-userscalable)

> **Good to know**: The `viewport` meta tag is automatically set, and manual configuration is usually unnecessary as the default is sufficient. However, the information is provided for completeness.

layout.tsx | page.tsx

TypeScript

JavaScriptTypeScript

```
import type { Viewport } from 'next'
 
export const viewport: Viewport = {
  width: 'device-width',
  initialScale: 1,
  maximumScale: 1,
  userScalable: false,
  // Also supported by less commonly used
  // interactiveWidget: 'resizes-visual',
}
```

&lt;head&gt; output

```
<meta
  name="viewport"
  content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no"
/>
```

### [`colorScheme`](#colorscheme)

Learn more about [`color-scheme`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta/name#:~:text=color%2Dscheme%3A%20specifies,of%20the%20following%3A).

layout.tsx | page.tsx

TypeScript

JavaScriptTypeScript

```
import type { Viewport } from 'next'
 
export const viewport: Viewport = {
  colorScheme: 'dark',
}
```

&lt;head&gt; output

```
<meta name="color-scheme" content="dark" />
```

## [Types](#types)

You can add type safety to your viewport object by using the `Viewport` type. If you are using the [built-in TypeScript plugin](/docs/14/app/building-your-application/configuring/typescript) in your IDE, you do not need to manually add the type, but you can still explicitly add it if you want.

### [`viewport` object](#viewport-object)

```
import type { Viewport } from 'next'
 
export const viewport: Viewport = {
  themeColor: 'black',
}
```

### [`generateViewport` function](#generateviewport-function-1)

#### [Regular function](#regular-function)

```
import type { Viewport } from 'next'
 
export function generateViewport(): Viewport {
  return {
    themeColor: 'black',
  }
}
```

#### [With segment props](#with-segment-props)

```
import type { Viewport } from 'next'
 
type Props = {
  params: { id: string }
  searchParams: { [key: string]: string | string[] | undefined }
}
 
export function generateViewport({ params, searchParams }: Props): Viewport {
  return {
    themeColor: 'black',
  }
}
 
export default function Page({ params, searchParams }: Props) {}
```

#### [JavaScript Projects](#javascript-projects)

For JavaScript projects, you can use JSDoc to add type safety.

```
/** @type {import("next").Viewport} */
export const viewport = {
  themeColor: 'black',
}
```

## [Version History](#version-history)

VersionChanges`v14.0.0``viewport` and `generateViewport` introduced.

## Next Steps

View all the Metadata API options.

[Introduction  
\
...  
\
File Conventions  
\
**Metadata Files**  
\
API documentation for the metadata file conventions.](/docs/14/app/api-reference/file-conventions/metadata)

[Introduction  
\
...  
\
Optimizing  
\
**Metadata**  
\
Use the Metadata API to define metadata in any layout or page.](/docs/14/app/building-your-application/optimizing/metadata)

Was this helpful?

supported.

Send
