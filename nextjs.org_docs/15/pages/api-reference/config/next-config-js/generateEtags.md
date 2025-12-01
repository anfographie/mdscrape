---
title: "generateEtags"
source: "https://nextjs.org/docs/15/pages/api-reference/config/next-config-js/generateEtags"
---

# generateEtags

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Configuration](/docs/15/pages/api-reference/config)[next.config.js Options](/docs/15/pages/api-reference/config/next-config-js)generateEtags

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# generateEtags

Next.js will generate [etags](https://en.wikipedia.org/wiki/HTTP_ETag) for every page by default. You may want to disable etag generation for HTML pages depending on your cache strategy.

Open `next.config.js` and disable the `generateEtags` option:

next.config.js

```
module.exports = {
  generateEtags: false,
}
```

Was this helpful?

supported.

Send
