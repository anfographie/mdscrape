---
title: "Runtime Config"
source: "https://nextjs.org/docs/13/pages/api-reference/next-config-js/runtime-configuration"
---

# Runtime Config

Menu

Pages Router 13

Using Pages Router

Features available in /pages

Version 13

13.5.11

[API Reference](/docs/13/pages/api-reference)[next.config.js Options](/docs/13/pages/api-reference/next-config-js)Runtime Config

You are currently viewing the Pages Router documentation for version 13 of Next.js.

# Runtime Config

> **Warning**: This feature is considered legacy and does not work with [Automatic Static Optimization](/docs/13/pages/building-your-application/rendering/automatic-static-optimization), [Output File Tracing](/docs/13/pages/api-reference/next-config-js/output#automatically-copying-traced-files), or [React Server Components](/docs/13/app/building-your-application/rendering/server-components). Please use [environment variables](/docs/13/pages/building-your-application/configuring/environment-variables) instead to avoid initialization overhead.

To add runtime configuration to your app, open `next.config.js` and add the `publicRuntimeConfig` and `serverRuntimeConfig` configs:

next.config.js

```
module.exports = {
  serverRuntimeConfig: {
    // Will only be available on the server side
    mySecret: 'secret',
    secondSecret: process.env.SECOND_SECRET, // Pass through env variables
  },
  publicRuntimeConfig: {
    // Will be available on both server and client
    staticFolder: '/static',
  },
}
```

Place any server-only runtime config under `serverRuntimeConfig`.

Anything accessible to both client and server-side code should be under `publicRuntimeConfig`.

> A page that relies on `publicRuntimeConfig` **must** use `getInitialProps` or `getServerSideProps` or your application must have a [Custom App](/docs/13/pages/building-your-application/routing/custom-app) with `getInitialProps` to opt-out of [Automatic Static Optimization](/docs/13/pages/building-your-application/rendering/automatic-static-optimization). Runtime configuration won't be available to any page (or component in a page) without being server-side rendered.

To get access to the runtime configs in your app use `next/config`, like so:

```
import getConfig from 'next/config'
import Image from 'next/image'
 
// Only holds serverRuntimeConfig and publicRuntimeConfig
const { serverRuntimeConfig, publicRuntimeConfig } = getConfig()
// Will only be available on the server-side
console.log(serverRuntimeConfig.mySecret)
// Will be available on both server-side and client-side
console.log(publicRuntimeConfig.staticFolder)
 
function MyImage() {
  return (
    <div>
      <Image
        src={`${publicRuntimeConfig.staticFolder}/logo.png`}
        alt="logo"
        layout="fill"
      />
    </div>
  )
}
 
export default MyImage
```

Was this helpful?

supported.

Send
