---
title: "Absolute Imports and Module Path Aliases"
source: "https://nextjs.org/docs/14/app/building-your-application/configuring/absolute-imports-and-module-aliases"
---

# Absolute Imports and Module Path Aliases

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[Building Your Application](/docs/14/app/building-your-application)[Configuring](/docs/14/app/building-your-application/configuring)Absolute Imports and Module Path Aliases

You are currently viewing documentation for version 14 of Next.js.

# Absolute Imports and Module Path Aliases

Examples

- [Absolute Imports and Aliases](https://github.com/vercel/next.js/tree/canary/examples/with-absolute-imports)

Next.js has in-built support for the `"paths"` and `"baseUrl"` options of `tsconfig.json` and `jsconfig.json` files.

These options allow you to alias project directories to absolute paths, making it easier to import modules. For example:

```
// before
import { Button } from '../../../components/button'
 
// after
import { Button } from '@/components/button'
```

> **Good to know**: `create-next-app` will prompt to configure these options for you.

## [Absolute Imports](#absolute-imports)

The `baseUrl` configuration option allows you to import directly from the root of the project.

An example of this configuration:

tsconfig.json or jsconfig.json

```
{
  "compilerOptions": {
    "baseUrl": "."
  }
}
```

components/button.tsx

TypeScript

JavaScriptTypeScript

```
export default function Button() {
  return <button>Click me</button>
}
```

app/page.tsx

TypeScript

JavaScriptTypeScript

```
import Button from 'components/button'
 
export default function HomePage() {
  return (
    <>
      <h1>Hello World</h1>
      <Button />
    </>
  )
}
```

## [Module Aliases](#module-aliases)

In addition to configuring the `baseUrl` path, you can use the `"paths"` option to "alias" module paths.

For example, the following configuration maps `@/components/*` to `components/*`:

tsconfig.json or jsconfig.json

```
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/components/*": ["components/*"]
    }
  }
}
```

components/button.tsx

TypeScript

JavaScriptTypeScript

```
export default function Button() {
  return <button>Click me</button>
}
```

app/page.tsx

TypeScript

JavaScriptTypeScript

```
import Button from '@/components/button'
 
export default function HomePage() {
  return (
    <>
      <h1>Hello World</h1>
      <Button />
    </>
  )
}
```

Each of the `"paths"` are relative to the `baseUrl` location. For example:

```
// tsconfig.json or jsconfig.json
{
  "compilerOptions": {
    "baseUrl": "src/",
    "paths": {
      "@/styles/*": ["styles/*"],
      "@/components/*": ["components/*"]
    }
  }
}
```

```
// pages/index.js
import Button from '@/components/button'
import '@/styles/styles.css'
import Helper from 'utils/helper'
 
export default function HomePage() {
  return (
    <Helper>
      <h1>Hello World</h1>
      <Button />
    </Helper>
  )
}
```

Was this helpful?

supported.

Send
