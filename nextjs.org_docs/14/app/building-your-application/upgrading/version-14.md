---
title: "Version 14"
source: "https://nextjs.org/docs/14/app/building-your-application/upgrading/version-14"
---

# Version 14

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[Building Your Application](/docs/14/app/building-your-application)[Upgrading](/docs/14/app/building-your-application/upgrading)Version 14

You are currently viewing documentation for version 14 of Next.js.

# Version 14

## [Upgrading from 13 to 14](#upgrading-from-13-to-14)

To update to Next.js version 14, run the following command using your preferred package manager:

Terminal

```
npm i next@latest react@latest react-dom@latest eslint-config-next@latest
```

Terminal

```
yarn add next@latest react@latest react-dom@latest eslint-config-next@latest
```

Terminal

```
pnpm up next react react-dom eslint-config-next --latest
```

Terminal

```
bun add next@latest react@latest react-dom@latest eslint-config-next@latest
```

> **Good to know:** If you are using TypeScript, ensure you also upgrade `@types/react` and `@types/react-dom` to their latest versions.

### [v14 Summary](#v14-summary)

- The minimum Node.js version has been bumped from 16.14 to 18.17, since 16.x has reached end-of-life.
- The `next export` command has been removed in favor of `output: 'export'` config. Please see the [docs](https://nextjs.org/docs/app/building-your-application/deploying/static-exports) for more information.
- The `next/server` import for `ImageResponse` was renamed to `next/og`. A [codemod is available](/docs/14/app/building-your-application/upgrading/codemods#next-og-import) to safely and automatically rename your imports.
- The `@next/font` package has been fully removed in favor of the built-in `next/font`. A [codemod is available](/docs/14/app/building-your-application/upgrading/codemods#built-in-next-font) to safely and automatically rename your imports.
- The WASM target for `next-swc` has been removed.

Was this helpful?

supported.

Send
