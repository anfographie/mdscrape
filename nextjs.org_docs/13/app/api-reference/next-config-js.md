---
title: "next.config.js Options"
source: "https://nextjs.org/docs/13/app/api-reference/next-config-js"
---

# next.config.js Options

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[App Router](/docs/13/app)[API Reference](/docs/13/app/api-reference)next.config.js Options

You are currently viewing documentation for version 13 of Next.js.

# next.config.js Options

Next.js can be configured through a `next.config.js` file in the root of your project directory (for example, by `package.json`).

next.config.js

```
/** @type {import('next').NextConfig} */
const nextConfig = {
  /* config options here */
}
 
module.exports = nextConfig
```

`next.config.js` is a regular Node.js module, not a JSON file. It gets used by the Next.js server and build phases, and it's not included in the browser build.

If you need [ECMAScript modules](https://nodejs.org/api/esm.html), you can use `next.config.mjs`:

next.config.mjs

```
/**
 * @type {import('next').NextConfig}
 */
const nextConfig = {
  /* config options here */
}
 
export default nextConfig
```

You can also use a function:

next.config.mjs

```
module.exports = (phase, { defaultConfig }) => {
  /**
   * @type {import('next').NextConfig}
   */
  const nextConfig = {
    /* config options here */
  }
  return nextConfig
}
```

Since Next.js 12.1.0, you can use an async function:

next.config.js

```
module.exports = async (phase, { defaultConfig }) => {
  /**
   * @type {import('next').NextConfig}
   */
  const nextConfig = {
    /* config options here */
  }
  return nextConfig
}
```

`phase` is the current context in which the configuration is loaded. You can see the [available phases](https://github.com/vercel/next.js/blob/5e6b008b561caf2710ab7be63320a3d549474a5b/packages/next/shared/lib/constants.ts#L19-L23). Phases can be imported from `next/constants`:

```
const { PHASE_DEVELOPMENT_SERVER } = require('next/constants')
 
module.exports = (phase, { defaultConfig }) => {
  if (phase === PHASE_DEVELOPMENT_SERVER) {
    return {
      /* development only config options here */
    }
  }
 
  return {
    /* config options for all phases except development here */
  }
}
```

The commented lines are the place where you can put the configs allowed by `next.config.js`, which are [defined in this file](https://github.com/vercel/next.js/blob/canary/packages/next/src/server/config-shared.ts).

However, none of the configs are required, and it's not necessary to understand what each config does. Instead, search for the features you need to enable or modify in this section and they will show you what to do.

> Avoid using new JavaScript features not available in your target Node.js version. `next.config.js` will not be parsed by Webpack, Babel or TypeScript.

This page documents all the available configuration options:

[**appDir**  
\
Enable the App Router to use layouts, streaming, and more.](/docs/13/app/api-reference/next-config-js/appDir)

[**assetPrefix**  
\
Learn how to use the assetPrefix config option to configure your CDN.](/docs/13/app/api-reference/next-config-js/assetPrefix)

[**basePath**  
\
Use \`basePath\` to deploy a Next.js application under a sub-path of a domain.](/docs/13/app/api-reference/next-config-js/basePath)

[**compress**  
\
Next.js provides gzip compression to compress rendered content and static files, it only works with the server target. Learn more about it here.](/docs/13/app/api-reference/next-config-js/compress)

[**devIndicators**  
\
Optimized pages include an indicator to let you know if it's being statically optimized. You can opt-out of it here.](/docs/13/app/api-reference/next-config-js/devIndicators)

[**distDir**  
\
Set a custom build directory to use instead of the default .next directory.](/docs/13/app/api-reference/next-config-js/distDir)

[**env**  
\
Learn to add and access environment variables in your Next.js application at build time.](/docs/13/app/api-reference/next-config-js/env)

[**eslint**  
\
Next.js reports ESLint errors and warnings during builds by default. Learn how to opt-out of this behavior here.](/docs/13/app/api-reference/next-config-js/eslint)

[**exportPathMap**  
\
Customize the pages that will be exported as HTML files when using \`next export\`.](/docs/13/app/api-reference/next-config-js/exportPathMap)

[**generateBuildId**  
\
Configure the build id, which is used to identify the current build in which your application is being served.](/docs/13/app/api-reference/next-config-js/generateBuildId)

[**generateEtags**  
\
Next.js will generate etags for every page by default. Learn more about how to disable etag generation here.](/docs/13/app/api-reference/next-config-js/generateEtags)

[**headers**  
\
Add custom HTTP headers to your Next.js app.](/docs/13/app/api-reference/next-config-js/headers)

[**httpAgentOptions**  
\
Next.js will automatically use HTTP Keep-Alive by default. Learn more about how to disable HTTP Keep-Alive here.](/docs/13/app/api-reference/next-config-js/httpAgentOptions)

[**images**  
\
Custom configuration for the next/image loader](/docs/13/app/api-reference/next-config-js/images)

[**incrementalCacheHandlerPath**  
\
Configure the Next.js cache used for storing and revalidating data.](/docs/13/app/api-reference/next-config-js/incrementalCacheHandlerPath)

[**mdxRs**  
\
Use the new Rust compiler to compile MDX files in the App Router.](/docs/13/app/api-reference/next-config-js/mdxRs)

[**onDemandEntries**  
\
Configure how Next.js will dispose and keep in memory pages created in development.](/docs/13/app/api-reference/next-config-js/onDemandEntries)

[**optimizePackageImports**  
\
API Reference for optmizedPackageImports Next.js Config Option](/docs/13/app/api-reference/next-config-js/optimizePackageImports)

[**output**  
\
Next.js automatically traces which files are needed by each page to allow for easy deployment of your application. Learn how it works here.](/docs/13/app/api-reference/next-config-js/output)

[**pageExtensions**  
\
Extend the default page extensions used by Next.js when resolving pages in the Pages Router.](/docs/13/app/api-reference/next-config-js/pageExtensions)

[**poweredByHeader**  
\
Next.js will add the \`x-powered-by\` header by default. Learn to opt-out of it here.](/docs/13/app/api-reference/next-config-js/poweredByHeader)

[**productionBrowserSourceMaps**  
\
Enables browser source map generation during the production build.](/docs/13/app/api-reference/next-config-js/productionBrowserSourceMaps)

[**reactStrictMode**  
\
The complete Next.js runtime is now Strict Mode-compliant, learn how to opt-in](/docs/13/app/api-reference/next-config-js/reactStrictMode)

[**redirects**  
\
Add redirects to your Next.js app.](/docs/13/app/api-reference/next-config-js/redirects)

[**rewrites**  
\
Add rewrites to your Next.js app.](/docs/13/app/api-reference/next-config-js/rewrites)

[**serverComponentsExternalPackages**  
\
Opt-out specific dependencies from the Server Components bundling and use native Node.js \`require\`.](/docs/13/app/api-reference/next-config-js/serverComponentsExternalPackages)

[**trailingSlash**  
\
Configure Next.js pages to resolve with or without a trailing slash.](/docs/13/app/api-reference/next-config-js/trailingSlash)

[**transpilePackages**  
\
Automatically transpile and bundle dependencies from local packages (like monorepos) or from external dependencies (\`node\_modules\`).](/docs/13/app/api-reference/next-config-js/transpilePackages)

[**turbo**  
\
Configure Next.js with Turbopack-specific options](/docs/13/app/api-reference/next-config-js/turbo)

[**typedRoutes**  
\
Enable experimental support for statically typed links.](/docs/13/app/api-reference/next-config-js/typedRoutes)

[**typescript**  
\
Next.js reports TypeScript errors by default. Learn to opt-out of this behavior here.](/docs/13/app/api-reference/next-config-js/typescript)

[**urlImports**  
\
Configure Next.js to allow importing modules from external URLs (experimental).](/docs/13/app/api-reference/next-config-js/urlImports)

[**webpack**  
\
Learn how to customize the webpack config used by Next.js](/docs/13/app/api-reference/next-config-js/webpack)

[**webVitalsAttribution**  
\
Learn how to use the webVitalsAttribution option to pinpoint the source of Web Vitals issues.](/docs/13/app/api-reference/next-config-js/webVitalsAttribution)

Was this helpful?

supported.

Send
