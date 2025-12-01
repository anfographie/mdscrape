---
title: "optimizePackageImports"
source: "https://nextjs.org/docs/14/pages/api-reference/next-config-js/optimizePackageImports"
---

# optimizePackageImports

Menu

Pages Router 14

Using Pages Router

Features available in /pages

Version 14

14.2.33

[API Reference](/docs/14/pages/api-reference)[next.config.js Options](/docs/14/pages/api-reference/next-config-js)optimizePackageImports

You are currently viewing the Pages Router documentation for version 14 of Next.js.

# optimizePackageImports

By default, Next.js uses `gzip` to compress rendered content and static files when using `next start` or a custom server. This is an optimization for applications that do not have compression configured. If compression is *already* configured in your application via a custom server, Next.js will not add compression.

> **Good to know:**
> 
> - When hosting your application on [Vercel](https://vercel.com/docs/edge-network/compression), compression uses `brotli` first, then `gzip`.
> - You can check if compression is enabled and which algorithm is used by looking at the [`Accept-Encoding`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Encoding) (browser accepted options) and [`Content-Encoding`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Encoding) (currently used) headers in the response.

## [Disabling compression](#disabling-compression)

To disable **compression**, set the `compress` config option to `false`:

next.config.js

```
module.exports = {
  compress: false,
}
```

We do not recommend disabling compression unless you have compression configured on your server, as compression reduces bandwidth usage and improves the performance of your application.

## [Changing the compression algorithm](#changing-the-compression-algorithm)

To change your compression algorithm, you will need to configure your custom server and set the `compress` option to `false` in your `next.config.js` file.

For example, you're using [nginx](https://www.nginx.com/) and want to switch to `brotli`, set the `compress` option to `false` to allow nginx to handle compression.

> **Good to know:**
> 
> - For Next.js applications on Vercel, compression is handled by the Vercel's Edge Network and not Next.js. See the [Vercel documentation](https://vercel.com/docs/edge-network/compression) for more information.

Was this helpful?

supported.

Send
