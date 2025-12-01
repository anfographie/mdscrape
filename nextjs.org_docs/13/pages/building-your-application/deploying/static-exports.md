---
title: "Static Exports"
source: "https://nextjs.org/docs/13/pages/building-your-application/deploying/static-exports"
---

# Static Exports

Menu

Pages Router 13

Using Pages Router

Features available in /pages

Version 13

13.5.11

[Building Your Application](/docs/13/pages/building-your-application)[Deploying](/docs/13/pages/building-your-application/deploying)Static Exports

You are currently viewing the Pages Router documentation for version 13 of Next.js.

# Static Exports

Next.js enables starting as a static site or Single-Page Application (SPA), then later optionally upgrading to use features that require a server.

When running `next build`, Next.js generates an HTML file per route. By breaking a strict SPA into individual HTML files, Next.js can avoid loading unnecessary JavaScript code on the client-side, reducing the bundle size and enabling faster page loads.

Since Next.js supports this static export, it can be deployed and hosted on any web server that can serve HTML/CSS/JS static assets.

> **Good to know**: We recommend using the App Router for enhanced static export support.

## [Configuration](#configuration)

To enable a static export, change the output mode inside `next.config.js`:

next.config.js

```
/**
 * @type {import('next').NextConfig}
 */
const nextConfig = {
  output: 'export',
 
  // Optional: Change links `/me` -> `/me/` and emit `/me.html` -> `/me/index.html`
  // trailingSlash: true,
 
  // Optional: Prevent automatic `/me` -> `/me/`, instead preserve `href`
  // skipTrailingSlashRedirect: true,
 
  // Optional: Change the output directory `out` -> `dist`
  // distDir: 'dist',
}
 
module.exports = nextConfig
```

After running `next build`, Next.js will produce an `out` folder which contains the HTML/CSS/JS assets for your application.

You can utilize [`getStaticProps`](/docs/13/pages/building-your-application/data-fetching/get-static-props) and [`getStaticPaths`](/docs/13/pages/building-your-application/data-fetching/get-static-paths) to generate an HTML file for each page in your `pages` directory (or more for [dynamic routes](/docs/13/app/building-your-application/routing/dynamic-routes)).

## [Supported Features](#supported-features-1)

The majority of core Next.js features needed to build a static site are supported, including:

- [Dynamic Routes when using `getStaticPaths`](/docs/13/app/building-your-application/routing/dynamic-routes)
- Prefetching with `next/link`
- Preloading JavaScript
- [Dynamic Imports](/docs/13/pages/building-your-application/optimizing/lazy-loading)
- Any styling options (e.g. CSS Modules, styled-jsx)
- [Client-side data fetching](/docs/13/pages/building-your-application/data-fetching/client-side)
- [`getStaticProps`](/docs/13/pages/building-your-application/data-fetching/get-static-props)
- [`getStaticPaths`](/docs/13/pages/building-your-application/data-fetching/get-static-paths)

### [Image Optimization](#image-optimization)

[Image Optimization](/docs/13/app/building-your-application/optimizing/images) through `next/image` can be used with a static export by defining a custom image loader in `next.config.js`. For example, you can optimize images with a service like Cloudinary:

next.config.js

```
/** @type {import('next').NextConfig} */
const nextConfig = {
  output: 'export',
  images: {
    loader: 'custom',
    loaderFile: './my-loader.ts',
  },
}
 
module.exports = nextConfig
```

This custom loader will define how to fetch images from a remote source. For example, the following loader will construct the URL for Cloudinary:

my-loader.ts

TypeScript

JavaScriptTypeScript

```
export default function cloudinaryLoader({
  src,
  width,
  quality,
}: {
  src: string
  width: number
  quality?: number
}) {
  const params = ['f_auto', 'c_limit', `w_${width}`, `q_${quality || 'auto'}`]
  return `https://res.cloudinary.com/demo/image/upload/${params.join(
    ','
  )}${src}`
}
```

You can then use `next/image` in your application, defining relative paths to the image in Cloudinary:

app/page.tsx

TypeScript

JavaScriptTypeScript

```
import Image from 'next/image'
 
export default function Page() {
  return <Image alt="turtles" src="/turtles.jpg" width={300} height={300} />
}
```

## [Unsupported Features](#unsupported-features)

Features that require a Node.js server, or dynamic logic that cannot be computed during the build process, are **not** supported:

- [Internationalized Routing](/docs/13/pages/building-your-application/routing/internationalization)
- [API Routes](/docs/13/pages/building-your-application/routing/api-routes)
- [Rewrites](/docs/13/pages/api-reference/next-config-js/rewrites)
- [Redirects](/docs/13/pages/api-reference/next-config-js/redirects)
- [Headers](/docs/13/pages/api-reference/next-config-js/headers)
- [Middleware](/docs/13/pages/building-your-application/routing/middleware)
- [Incremental Static Regeneration](/docs/13/pages/building-your-application/data-fetching/incremental-static-regeneration)
- [Image Optimization](/docs/13/pages/building-your-application/optimizing/images) with the default `loader`
- [Draft Mode](/docs/13/pages/building-your-application/configuring/draft-mode)
- [`getStaticPaths` with `fallback: true`](/docs/13/pages/api-reference/functions/get-static-paths#fallback-true)
- [`getStaticPaths` with `fallback: 'blocking'`](/docs/13/pages/api-reference/functions/get-static-paths#fallback-blocking)
- [`getServerSideProps`](/docs/13/pages/building-your-application/data-fetching/get-server-side-props)

## [Deploying](#deploying)

With a static export, Next.js can be deployed and hosted on any web server that can serve HTML/CSS/JS static assets.

When running `next build`, Next.js generates the static export into the `out` folder. Using `next export` is no longer needed. For example, let's say you have the following routes:

- `/`
- `/blog/[id]`

After running `next build`, Next.js will generate the following files:

- `/out/index.html`
- `/out/404.html`
- `/out/blog/post-1.html`
- `/out/blog/post-2.html`

If you are using a static host like Nginx, you can configure rewrites from incoming requests to the correct files:

nginx.conf

```
server {
  listen 80;
  server_name acme.com;
 
  root /var/www/out;
 
  location / {
      try_files $uri $uri.html $uri/ =404;
  }
 
  # This is necessary when `trailingSlash: false`.
  # You can omit this when `trailingSlash: true`.
  location /blog/ {
      rewrite ^/blog/(.*)$ /blog/$1.html break;
  }
 
  error_page 404 /404.html;
  location = /404.html {
      internal;
  }
}
```

## [Version History](#version-history)

VersionChanges`v13.4.0`App Router (Stable) adds enhanced static export support, including using React Server Components and Route Handlers.`v13.3.0``next export` is deprecated and replaced with `"output": "export"`

Was this helpful?

supported.

Send
