---
title: "Static Assets"
source: "https://nextjs.org/docs/13/app/building-your-application/optimizing/static-assets"
---

# Static Assets

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[Building Your Application](/docs/13/app/building-your-application)[Optimizing](/docs/13/app/building-your-application/optimizing)Static Assets

You are currently viewing documentation for version 13 of Next.js.

# Static Assets

Next.js can serve static files, like images, under a folder called `public` in the root directory. Files inside `public` can then be referenced by your code starting from the base URL (`/`).

For example, if you add `me.png` inside `public`, the following code will access the image:

Avatar.js

```
import Image from 'next/image'
 
export function Avatar() {
  return <Image src="/me.png" alt="me" width="64" height="64" />
}
```

For static metadata files, such as `robots.txt`, `favicon.ico`, etc, you should use [special metadata files](/docs/13/app/api-reference/file-conventions/metadata) inside the `app` folder.

> Good to know:
> 
> - The directory must be named `public`. The name cannot be changed and it's the only directory used to serve static assets.
> - Only assets that are in the `public` directory at [build time](/docs/13/app/api-reference/next-cli#build) will be served by Next.js. Files added at request time won't be available. We recommend using a third-party service like [AWS S3](https://aws.amazon.com/s3/) for persistent file storage.

Was this helpful?

supported.

Send
