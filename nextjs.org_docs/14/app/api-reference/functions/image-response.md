---
title: "ImageResponse"
source: "https://nextjs.org/docs/14/app/api-reference/functions/image-response"
---

# ImageResponse

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[Functions](/docs/14/app/api-reference/functions)ImageResponse

You are currently viewing documentation for version 14 of Next.js.

# ImageResponse

The `ImageResponse` constructor allows you to generate dynamic images using JSX and CSS. This is useful for generating social media images such as Open Graph images, Twitter cards, and more.

The following options are available for `ImageResponse`:

```
import { ImageResponse } from 'next/og'
 
new ImageResponse(
  element: ReactElement,
  options: {
    width?: number = 1200
    height?: number = 630
    emoji?: 'twemoji' | 'blobmoji' | 'noto' | 'openmoji' = 'twemoji',
    fonts?: {
      name: string,
      data: ArrayBuffer,
      weight: number,
      style: 'normal' | 'italic'
    }[]
    debug?: boolean = false
 
    // Options that will be passed to the HTTP response
    status?: number = 200
    statusText?: string
    headers?: Record<string, string>
  },
)
```

## [Supported CSS Properties](#supported-css-properties)

Please refer to [Satori’s documentation](https://github.com/vercel/satori#css) for a list of supported HTML and CSS features.

## [Version History](#version-history)

VersionChanges`v14.0.0``ImageResponse` moved from `next/server` to `next/og``v13.3.0``ImageResponse` can be imported from `next/server`.`v13.0.0``ImageResponse` introduced via `@vercel/og` package.

Was this helpful?

supported.

Send
