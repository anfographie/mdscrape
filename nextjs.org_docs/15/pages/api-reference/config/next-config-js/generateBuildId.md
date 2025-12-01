---
title: "generateBuildId"
source: "https://nextjs.org/docs/15/pages/api-reference/config/next-config-js/generateBuildId"
---

# generateBuildId

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Configuration](/docs/15/pages/api-reference/config)[next.config.js Options](/docs/15/pages/api-reference/config/next-config-js)generateBuildId

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# generateBuildId

Next.js generates an ID during `next build` to identify which version of your application is being served. The same build should be used and boot up multiple containers.

If you are rebuilding for each stage of your environment, you will need to generate a consistent build ID to use between containers. Use the `generateBuildId` command in `next.config.js`:

next.config.js

```
module.exports = {
  generateBuildId: async () => {
    // This could be anything, using the latest git hash
    return process.env.GIT_HASH
  },
}
```

Was this helpful?

supported.

Send
