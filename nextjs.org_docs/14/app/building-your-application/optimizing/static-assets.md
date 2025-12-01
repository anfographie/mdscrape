---
title: "Static Assets in `public`"
source: "https://nextjs.org/docs/14/app/building-your-application/optimizing/static-assets"
---

# Static Assets in `public`

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[Building Your Application](/docs/14/app/building-your-application)[Optimizing](/docs/14/app/building-your-application/optimizing)Static Assets

You are currently viewing documentation for version 14 of Next.js.

# Static Assets in \`public\`

Next.js can serve static files, like images, under a folder called `public` in the root directory. Files inside `public` can then be referenced by your code starting from the base URL (`/`).

For example, the file `public/avatars/me.png` can be viewed by visiting the `/avatars/me.png` path. The code to display that image might look like:

avatar.js

```
import Image from 'next/image'
 
export function Avatar({ id, alt }) {
  return <Image src={`/avatars/${id}.png`} alt={alt} width="64" height="64" />
}
 
export function AvatarOfMe() {
  return <Avatar id="me" alt="A portrait of me" />
}
```

## [Caching](#caching)

Next.js cannot safely cache assets in the `public` folder because they may change. The default caching headers applied are:

```
Cache-Control: public, max-age=0
```

## [Robots, Favicons, and others](#robots-favicons-and-others)

For static metadata files, such as `robots.txt`, `favicon.ico`, etc, you should use [special metadata files](/docs/14/app/api-reference/file-conventions/metadata) inside the `app` folder.

> Good to know:
> 
> - The directory must be named `public`. The name cannot be changed and it's the only directory used to serve static assets.
> - Only assets that are in the `public` directory at [build time](/docs/14/app/api-reference/cli/next#next-build-options) will be served by Next.js. Files added at request time won't be available. We recommend using a third-party service like [Vercel Blob](https://vercel.com/docs/storage/vercel-blob?utm_source=next-site&utm_medium=docs&utm_campaign=next-website) for persistent file storage.

Was this helpful?

supported.

Send
