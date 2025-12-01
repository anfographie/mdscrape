---
title: "robots.txt"
source: "https://nextjs.org/docs/13/app/api-reference/file-conventions/metadata/robots"
---

# robots.txt

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[File Conventions](/docs/13/app/api-reference/file-conventions)[Metadata Files](/docs/13/app/api-reference/file-conventions/metadata)robots.txt

You are currently viewing documentation for version 13 of Next.js.

# robots.txt

Add or generate a `robots.txt` file that matches the [Robots Exclusion Standard](https://en.wikipedia.org/wiki/Robots.txt#Standard) in the **root** of `app` directory to tell search engine crawlers which URLs they can access on your site.

## [Static `robots.txt`](#static-robotstxt)

app/robots.txt

```
User-Agent: *
Allow: /
Disallow: /private/

Sitemap: https://acme.com/sitemap.xml
```

## [Generate a Robots file](#generate-a-robots-file)

Add a `robots.js` or `robots.ts` file that returns a [`Robots` object](#robots-object).

app/robots.ts

TypeScript

JavaScriptTypeScript

```
import { MetadataRoute } from 'next'
 
export default function robots(): MetadataRoute.Robots {
  return {
    rules: {
      userAgent: '*',
      allow: '/',
      disallow: '/private/',
    },
    sitemap: 'https://acme.com/sitemap.xml',
  }
}
```

Output:

```
User-Agent: *
Allow: /
Disallow: /private/

Sitemap: https://acme.com/sitemap.xml
```

### [Robots object](#robots-object)

```
type Robots = {
  rules:
    | {
        userAgent?: string | string[]
        allow?: string | string[]
        disallow?: string | string[]
        crawlDelay?: number
      }
    | Array<{
        userAgent: string | string[]
        allow?: string | string[]
        disallow?: string | string[]
        crawlDelay?: number
      }>
  sitemap?: string | string[]
  host?: string
}
```

## [Version History](#version-history)

VersionChanges`v13.3.0``robots` introduced.

Was this helpful?

supported.

Send
