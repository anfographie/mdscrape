---
title: "generateEtags"
source: "https://nextjs.org/docs/14/pages/api-reference/next-config-js/generateEtags"
---

# generateEtags

Menu

Pages Router 14

Using Pages Router

Features available in /pages

Version 14

14.2.33

[API Reference](/docs/14/pages/api-reference)[next.config.js Options](/docs/14/pages/api-reference/next-config-js)generateEtags

You are currently viewing the Pages Router documentation for version 14 of Next.js.

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
