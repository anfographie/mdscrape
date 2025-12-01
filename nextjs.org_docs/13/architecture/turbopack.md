---
title: "Turbopack"
source: "https://nextjs.org/docs/13/architecture/turbopack"
---

# Turbopack

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[Introduction](/docs/13)[Architecture](/docs/13/architecture)Turbopack

You are currently viewing documentation for version 13 of Next.js.

# Turbopack

[Turbopack](https://turbo.build/pack) (beta) is an incremental bundler optimized for JavaScript and TypeScript, written in Rust, and built into Next.js.

## [Usage](#usage)

Turbopack can be used in Next.js in both the `pages` and `app` directories for faster local development. To enable Turbopack, use the `--turbo` flag when running the Next.js development server.

package.json

```
{
  "scripts": {
    "dev": "next dev --turbo",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  }
}
```

## [Supported Features](#supported-features)

To learn more about the currently supported features for Turbopack, view the [documentation](https://turbo.build/pack/docs/features).

## [Unsupported Features](#unsupported-features)

Turbopack currently only supports `next dev` and does not support `next build`. We are currently working on support for builds as we move closer towards stability.

Was this helpful?

supported.

Send
