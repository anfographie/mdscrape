---
title: "pageExtensions"
source: "https://nextjs.org/docs/13/pages/api-reference/next-config-js/pageExtensions"
---

# pageExtensions

Menu

Pages Router 13

Using Pages Router

Features available in /pages

Version 13

13.5.11

[API Reference](/docs/13/pages/api-reference)[next.config.js Options](/docs/13/pages/api-reference/next-config-js)pageExtensions

You are currently viewing the Pages Router documentation for version 13 of Next.js.

# pageExtensions

You can extend the default Page extensions (`.tsx`, `.ts`, `.jsx`, `.js`) used by Next.js. Inside `next.config.js`, add the `pageExtensions` config:

next.config.js

```
module.exports = {
  pageExtensions: ['mdx', 'md', 'jsx', 'js', 'tsx', 'ts'],
}
```

Changing these values affects *all* Next.js pages, including the following:

- [`middleware.js`](/docs/13/pages/building-your-application/routing/middleware)
- [`instrumentation.js`](/docs/13/pages/building-your-application/optimizing/instrumentation)
- `pages/_document.js`
- `pages/_app.js`
- `pages/api/`

For example, if you reconfigure `.ts` page extensions to `.page.ts`, you would need to rename pages like `middleware.page.ts`, `instrumentation.page.ts`, `_app.page.ts`.

## [Including non-page files in the `pages` directory](#including-non-page-files-in-the-pages-directory)

You can colocate test files or other files used by components in the `pages` directory. Inside `next.config.js`, add the `pageExtensions` config:

next.config.js

```
module.exports = {
  pageExtensions: ['page.tsx', 'page.ts', 'page.jsx', 'page.js'],
}
```

Then, rename your pages to have a file extension that includes `.page` (e.g. rename `MyPage.tsx` to `MyPage.page.tsx`). Ensure you rename *all* Next.js pages, including the files mentioned above.

Was this helpful?

supported.

Send
