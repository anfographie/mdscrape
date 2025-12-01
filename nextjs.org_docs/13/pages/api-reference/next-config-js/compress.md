---
title: "compress"
source: "https://nextjs.org/docs/13/pages/api-reference/next-config-js/compress"
---

# compress

Menu

Pages Router 13

Using Pages Router

Features available in /pages

Version 13

13.5.11

[API Reference](/docs/13/pages/api-reference)[next.config.js Options](/docs/13/pages/api-reference/next-config-js)compress

You are currently viewing the Pages Router documentation for version 13 of Next.js.

# compress

Next.js provides [**gzip**](https://tools.ietf.org/html/rfc6713#section-3) compression to compress rendered content and static files. In general you will want to enable compression on a HTTP proxy like [nginx](https://www.nginx.com/), to offload load from the `Node.js` process.

To disable **compression**, open `next.config.js` and disable the `compress` config:

next.config.js

```
module.exports = {
  compress: false,
}
```

Was this helpful?

supported.

Send
