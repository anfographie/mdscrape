---
title: "CSS Modules and Global Styles"
source: "https://nextjs.org/docs/14/app/building-your-application/styling/css-modules"
---

# CSS Modules and Global Styles

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[Building Your Application](/docs/14/app/building-your-application)[Styling](/docs/14/app/building-your-application/styling)CSS Modules

You are currently viewing documentation for version 14 of Next.js.

# CSS Modules and Global Styles

Next.js supports different types of stylesheets, including:

- [CSS Modules](#css-modules)
- [Global Styles](#global-styles)
- [External Stylesheets](#external-stylesheets)

## [CSS Modules](#css-modules)

Next.js has built-in support for CSS Modules using the `.module.css` extension.

CSS Modules locally scope CSS by automatically creating a unique class name. This allows you to use the same class name in different files without worrying about collisions. This behavior makes CSS Modules the ideal way to include component-level CSS.

## [Example](#example)

CSS Modules can be imported into any file inside the `app` directory:

app/dashboard/layout.tsx

TypeScript

JavaScriptTypeScript

```
import styles from './styles.module.css'
 
export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return <section className={styles.dashboard}>{children}</section>
}
```

app/dashboard/styles.module.css

```
.dashboard {
  padding: 24px;
}
```

CSS Modules are **only enabled for files with the `.module.css` and `.module.sass` extensions**.

In production, all CSS Module files will be automatically concatenated into **many minified and code-split** `.css` files. These `.css` files represent hot execution paths in your application, ensuring the minimal amount of CSS is loaded for your application to paint.

## [Global Styles](#global-styles)

Global styles can be imported into any layout, page, or component inside the `app` directory.

> **Good to know**: This is different from the `pages` directory, where you can only import global styles inside the `_app.js` file.

For example, consider a stylesheet named `app/global.css`:

```
body {
  padding: 20px 20px 60px;
  max-width: 680px;
  margin: 0 auto;
}
```

Inside the root layout (`app/layout.js`), import the `global.css` stylesheet to apply the styles to every route in your application:

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
// These styles apply to every route in the application
import './global.css'
 
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  )
}
```

## [External Stylesheets](#external-stylesheets)

Stylesheets published by external packages can be imported anywhere in the `app` directory, including colocated components:

app/layout.tsx

TypeScript

JavaScriptTypeScript

```
import 'bootstrap/dist/css/bootstrap.css'
 
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body className="container">{children}</body>
    </html>
  )
}
```

> **Good to know**: External stylesheets must be directly imported from an npm package or downloaded and colocated with your codebase. You cannot use `<link rel="stylesheet" />`.

## [Ordering and Merging](#ordering-and-merging)

Next.js optimizes CSS during production builds by automatically chunking (merging) stylesheets. The CSS order is determined by the order in which you import the stylesheets into your application code.

For example, `base-button.module.css` will be ordered before `page.module.css` since `<BaseButton>` is imported first in `<Page>`:

base-button.tsx

TypeScript

JavaScriptTypeScript

```
import styles from './base-button.module.css'
 
export function BaseButton() {
  return <button className={styles.primary} />
}
```

page.ts

TypeScript

JavaScriptTypeScript

```
import { BaseButton } from './base-button'
import styles from './page.module.css'
 
export function Page() {
  return <BaseButton className={styles.primary} />
}
```

To maintain a predictable order, we recommend the following:

- Only import a CSS file in a single JS/TS file.
  
  - If using global class names, import the global styles in the same file in the order you want them to be applied.
- Prefer CSS Modules over global styles.
  
  - Use a consistent naming convention for your CSS modules. For example, using `<name>.module.css` over `<name>.tsx`.
- Extract shared styles into a separate shared component.
- If using [Tailwind](/docs/14/app/building-your-application/styling/tailwind-css), import the stylesheet at the top of the file, preferably in the [Root Layout](/docs/14/app/building-your-application/routing/pages-and-layouts#root-layout-required).

> **Good to know:** CSS ordering behaves differently in development mode, always ensure to check preview deployments to verify the final CSS order in your production build.

## [Additional Features](#additional-features)

Next.js includes additional features to improve the authoring experience of adding styles:

- When running locally with `next dev`, local stylesheets (either global or CSS modules) will take advantage of [Fast Refresh](/docs/14/architecture/fast-refresh) to instantly reflect changes as edits are saved.
- When building for production with `next build`, CSS files will be bundled into fewer minified `.css` files to reduce the number of network requests needed to retrieve styles.
- If you disable JavaScript, styles will still be loaded in the production build (`next start`). However, JavaScript is still required for `next dev` to enable [Fast Refresh](/docs/14/architecture/fast-refresh).

Was this helpful?

supported.

Send
