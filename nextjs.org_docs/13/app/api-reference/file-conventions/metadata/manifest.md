---
title: "manifest.json"
source: "https://nextjs.org/docs/13/app/api-reference/file-conventions/metadata/manifest"
---

# manifest.json

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[File Conventions](/docs/13/app/api-reference/file-conventions)[Metadata Files](/docs/13/app/api-reference/file-conventions/metadata)manifest.json

You are currently viewing documentation for version 13 of Next.js.

# manifest.json

Add or generate a `manifest.(json|webmanifest)` file that matches the [Web Manifest Specification](https://developer.mozilla.org/docs/Web/Manifest) in the **root** of `app` directory to provide information about your web application for the browser.

## [Static Manifest file](#static-manifest-file)

app/manifest.json | app/manifest.webmanifest

```
{
  "name": "My Next.js Application",
  "short_name": "Next.js App",
  "description": "An application built with Next.js",
  "start_url": "/"
  // ...
}
```

## [Generate a Manifest file](#generate-a-manifest-file)

Add a `manifest.js` or `manifest.ts` file that returns a [`Manifest` object](#manifest-object).

app/manifest.ts

TypeScript

JavaScriptTypeScript

```
import { MetadataRoute } from 'next'
 
export default function manifest(): MetadataRoute.Manifest {
  return {
    name: 'Next.js App',
    short_name: 'Next.js App',
    description: 'Next.js App',
    start_url: '/',
    display: 'standalone',
    background_color: '#fff',
    theme_color: '#fff',
    icons: [
      {
        src: '/favicon.ico',
        sizes: 'any',
        type: 'image/x-icon',
      },
    ],
  }
}
```

### [Manifest Object](#manifest-object)

The manifest object contains an extensive list of options that may be updated due to new web standards. For information on all the current options, refer to the `MetadataRoute.Manifest` type in your code editor if using [TypeScript](https://nextjs.org/docs/app/building-your-application/configuring/typescript#typescript-plugin) or see the [MDN](https://developer.mozilla.org/docs/Web/Manifest) docs.

Was this helpful?

supported.

Send
