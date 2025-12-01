---
title: "instrumentation.js"
source: "https://nextjs.org/docs/14/app/api-reference/file-conventions/instrumentation"
---

# instrumentation.js

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[File Conventions](/docs/14/app/api-reference/file-conventions)instrumentation.js

You are currently viewing documentation for version 14 of Next.js.

# instrumentation.js

The `instrumentation.js|ts` file is used to integrate monitoring and logging tools into your application. This allows you to track the performance and behavior of your application, and to debug issues in production.

To use it, place the file in the **root** of your application or inside a [`src` folder](/docs/14/app/building-your-application/configuring/src-directory) if using one.

## [Config Option](#config-option)

Instrumentation is currently an experimental feature, to use the `instrumentation` file, you must explicitly opt-in by defining [`experimental.instrumentationHook = true;`](/docs/14/app/api-reference/next-config-js/instrumentationHook) in your `next.config.js`:

next.config.js

```
module.exports = {
  experimental: {
    instrumentationHook: true,
  },
}
```

## [Exports](#exports)

### [`register` (required)](#register-required)

The file exports a `register` function that is called **once** when a new Next.js server instance is initiated. `register` can be an async function.

instrumentation.ts

TypeScript

JavaScriptTypeScript

```
import { registerOTel } from '@vercel/otel'
 
export function register() {
  registerOTel('next-app')
}
```

## [Version History](#version-history)

VersionChanges`v14.0.4`Turbopack support for `instrumentation``v13.2.0``instrumentation` introduced as an experimental feature

## Learn more about Instrumentation

[Introduction  
\
...  
\
Optimizing  
\
**Instrumentation**  
\
Learn how to use instrumentation to run code at server startup in your Next.js app](/docs/14/app/building-your-application/optimizing/instrumentation)

Was this helpful?

supported.

Send
