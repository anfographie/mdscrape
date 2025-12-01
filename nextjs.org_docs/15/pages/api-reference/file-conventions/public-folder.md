---
title: "public Folder"
source: "https://nextjs.org/docs/15/pages/api-reference/file-conventions/public-folder"
---

# public Folder

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[API Reference](/docs/15/pages/api-reference)[File-system conventions](/docs/15/pages/api-reference/file-conventions)public

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# public Folder

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

The folder is also useful for `robots.txt`, `favicon.ico`, Google Site Verification, and any other static files (including `.html`). But make sure to not have a static file with the same name as a file in the `pages/` directory, as this will result in an error. [Read more](/docs/15/messages/conflicting-public-file-page).

Was this helpful?

supported.

Send
