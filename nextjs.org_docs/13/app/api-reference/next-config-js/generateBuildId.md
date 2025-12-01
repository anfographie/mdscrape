---
title: "generateBuildId"
source: "https://nextjs.org/docs/13/app/api-reference/next-config-js/generateBuildId"
---

# generateBuildId

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[next.config.js Options](/docs/13/app/api-reference/next-config-js)generateBuildId

You are currently viewing documentation for version 13 of Next.js.

# generateBuildId

Next.js uses a constant id generated at build time to identify which version of your application is being served. This can cause problems in multi-server deployments when `next build` is run on every server. In order to keep a consistent build id between builds you can provide your own build id.

Open `next.config.js` and add the `generateBuildId` function:

next.config.js

```
module.exports = {
  generateBuildId: async () => {
    // You can, for example, get the latest git commit hash here
    return 'my-build-id'
  },
}
```

Was this helpful?

supported.

Send
