---
title: "Runtime Config"
source: "https://nextjs.org/docs/15/pages/api-reference/config/next-config-js/runtime-configuration"
---

# Runtime Config

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Configuration](/docs/15/pages/api-reference/config)[next.config.js Options](/docs/15/pages/api-reference/config/next-config-js)Runtime Config

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# Runtime Config

> **Warning:**
> 
> - **This feature is deprecated.** We recommend using [environment variables](/docs/15/pages/guides/environment-variables) instead, which also can support reading runtime values.
> - You can run code on server startup using the [`register` function](/docs/15/app/guides/instrumentation).
> - This feature does not work with [Automatic Static Optimization](/docs/15/pages/building-your-application/rendering/automatic-static-optimization), [Output File Tracing](/docs/15/pages/api-reference/config/next-config-js/output#automatically-copying-traced-files), or [React Server Components](/docs/15/app/getting-started/server-and-client-components).

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

> A page that relies on `publicRuntimeConfig` **must** use `getInitialProps` or `getServerSideProps` or your application must have a [Custom App](/docs/15/pages/building-your-application/routing/custom-app) with `getInitialProps` to opt-out of [Automatic Static Optimization](/docs/15/pages/building-your-application/rendering/automatic-static-optimization). Runtime configuration won't be available to any page (or component in a page) without being server-side rendered.

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
