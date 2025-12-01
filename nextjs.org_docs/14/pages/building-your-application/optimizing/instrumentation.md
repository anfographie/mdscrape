---
title: "Instrumentation"
source: "https://nextjs.org/docs/14/pages/building-your-application/optimizing/instrumentation"
---

# Instrumentation

Menu

Pages Router 14

Using Pages Router

Features available in /pages

Version 14

14.2.33

[Building Your Application](/docs/14/pages/building-your-application)[Optimizing](/docs/14/pages/building-your-application/optimizing)Instrumentation

You are currently viewing the Pages Router documentation for version 14 of Next.js.

# Instrumentation

Instrumentation is the process of using code to integrate monitoring and logging tools into your application. This allows you to track the performance and behavior of your application, and to debug issues in production.

## [Convention](#convention)

To set up instrumentation, create `instrumentation.ts|js` file in the **root directory** of your project (or inside the [`src`](/docs/14/app/building-your-application/configuring/src-directory) folder if using one).

Then, export a `register` function in the file. This function will be called **once** when a new Next.js server instance is initiated.

For example, to use Next.js with [OpenTelemetry](https://opentelemetry.io/) and [@vercel/otel](https://vercel.com/docs/observability/otel-overview):

instrumentation.ts

TypeScript

JavaScriptTypeScript

```
import { registerOTel } from '@vercel/otel'
 
export function register() {
  registerOTel('next-app')
}
```

See the [Next.js with OpenTelemetry example](https://github.com/vercel/next.js/tree/canary/examples/with-opentelemetry) for a complete implementation.

> **Good to know**
> 
> - This feature is **experimental**. To use it, you must explicitly opt in by defining [`experimental.instrumentationHook = true;`](/docs/14/app/api-reference/next-config-js/instrumentationHook) in your `next.config.js`.
> - The `instrumentation` file should be in the root of your project and not inside the `app` or `pages` directory. If you're using the `src` folder, then place the file inside `src` alongside `pages` and `app`.
> - If you use the [`pageExtensions` config option](/docs/14/app/api-reference/next-config-js/pageExtensions) to add a suffix, you will also need to update the `instrumentation` filename to match.

## [Examples](#examples)

### [Importing files with side effects](#importing-files-with-side-effects)

Sometimes, it may be useful to import a file in your code because of the side effects it will cause. For example, you might import a file that defines a set of global variables, but never explicitly use the imported file in your code. You would still have access to the global variables the package has declared.

We recommend importing files using JavaScript `import` syntax within your `register` function. The following example demonstrates a basic usage of `import` in a `register` function:

instrumentation.ts

TypeScript

JavaScriptTypeScript

```
export async function register() {
  await import('package-with-side-effect')
}
```

> **Good to know:**
> 
> We recommend importing the file from within the `register` function, rather than at the top of the file. By doing this, you can colocate all of your side effects in one place in your code, and avoid any unintended consequences from importing globally at the top of the file.

### [Importing runtime-specific code](#importing-runtime-specific-code)

Next.js calls `register` in all environments, so it's important to conditionally import any code that doesn't support specific runtimes (e.g. [Edge](/docs/14/app/building-your-application/rendering/edge-and-nodejs-runtimes#edge-runtime) or [Node.js](/docs/14/app/building-your-application/rendering/edge-and-nodejs-runtimes#nodejs-runtime)). You can use the `NEXT_RUNTIME` environment variable to get the current environment:

instrumentation.ts

TypeScript

JavaScriptTypeScript

```
export async function register() {
  if (process.env.NEXT_RUNTIME === 'nodejs') {
    await import('./instrumentation-node')
  }
 
  if (process.env.NEXT_RUNTIME === 'edge') {
    await import('./instrumentation-edge')
  }
}
```

Was this helpful?

supported.

Send
