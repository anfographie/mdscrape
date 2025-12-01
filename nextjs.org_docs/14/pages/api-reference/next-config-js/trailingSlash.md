---
title: "trailingSlash"
source: "https://nextjs.org/docs/14/pages/api-reference/next-config-js/trailingSlash"
---

# trailingSlash

Menu

Pages Router 14

Using Pages Router

Features available in /pages

Version 14

14.2.33

[API Reference](/docs/14/pages/api-reference)[next.config.js Options](/docs/14/pages/api-reference/next-config-js)trailingSlash

You are currently viewing the Pages Router documentation for version 14 of Next.js.

# trailingSlash

By default Next.js will redirect urls with trailing slashes to their counterpart without a trailing slash. For example `/about/` will redirect to `/about`. You can configure this behavior to act the opposite way, where urls without trailing slashes are redirected to their counterparts with trailing slashes.

Open `next.config.js` and add the `trailingSlash` config:

next.config.js

```
module.exports = {
  trailingSlash: true,
}
```

With this option set, urls like `/about` will redirect to `/about/`.

When used with [`output: "export"`](/docs/14/app/building-your-application/deploying/static-exports) configuration, the `/about` page will output `/about/index.html` (instead of the default `/about.html`).

## [Version History](#version-history)

VersionChanges`v9.5.0``trailingSlash` added.

Was this helpful?

supported.

Send
