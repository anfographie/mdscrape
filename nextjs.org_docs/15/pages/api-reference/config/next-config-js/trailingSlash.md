---
title: "trailingSlash"
source: "https://nextjs.org/docs/15/pages/api-reference/config/next-config-js/trailingSlash"
---

# trailingSlash

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Configuration](/docs/15/pages/api-reference/config)[next.config.js Options](/docs/15/pages/api-reference/config/next-config-js)trailingSlash

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# trailingSlash

By default Next.js will redirect URLs with trailing slashes to their counterpart without a trailing slash. For example `/about/` will redirect to `/about`. You can configure this behavior to act the opposite way, where URLs without trailing slashes are redirected to their counterparts with trailing slashes.

Open `next.config.js` and add the `trailingSlash` config:

next.config.js

```
module.exports = {
  trailingSlash: true,
}
```

With this option set, URLs like `/about` will redirect to `/about/`.

When using `trailingSlash: true`, certain URLs are exceptions and will not have a trailing slash appended:

- Static file URLs, such as files with extensions.
- Any paths under `.well-known/`.

For example, the following URLs will remain unchanged: `/file.txt`, `images/photos/picture.png`, and `.well-known/subfolder/config.json`.

When used with [`output: "export"`](/docs/15/app/guides/static-exports) configuration, the `/about` page will output `/about/index.html` (instead of the default `/about.html`).

## [Version History](#version-history)

VersionChanges`v9.5.0``trailingSlash` added.

Was this helpful?

supported.

Send
