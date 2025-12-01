---
title: "Static Assets"
source: "https://nextjs.org/docs/13/pages/building-your-application/optimizing/static-assets"
---

# Static Assets

Menu

Pages Router 13

Using Pages Router

Features available in /pages

Version 13

13.5.11

[Building Your Application](/docs/13/pages/building-your-application)[Optimizing](/docs/13/pages/building-your-application/optimizing)Static Assets

You are currently viewing the Pages Router documentation for version 13 of Next.js.

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

This folder is also useful for `robots.txt`, `favicon.ico`, Google Site Verification, and any other static files (including `.html`). But make sure to not have a static file with the same name as a file in the `pages/` directory, as this will result in an error. [Read more](/docs/13/messages/conflicting-public-file-page).

> Good to know:
> 
> - The directory must be named `public`. The name cannot be changed and it's the only directory used to serve static assets.
> - Only assets that are in the `public` directory at [build time](/docs/13/app/api-reference/next-cli#build) will be served by Next.js. Files added at request time won't be available. We recommend using a third-party service like [AWS S3](https://aws.amazon.com/s3/) for persistent file storage.

Was this helpful?

supported.

Send
