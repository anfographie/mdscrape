---
title: "Tailwind CSS"
source: "https://nextjs.org/docs/14/pages/building-your-application/styling/tailwind-css"
---

# Tailwind CSS

Menu

Pages Router 14

Using Pages Router

Features available in /pages

Version 14

14.2.33

[Building Your Application](/docs/14/pages/building-your-application)[Styling](/docs/14/pages/building-your-application/styling)Tailwind CSS

You are currently viewing the Pages Router documentation for version 14 of Next.js.

# Tailwind CSS

Examples

- [With Tailwind CSS](https://github.com/vercel/next.js/tree/canary/examples/with-tailwindcss)

[Tailwind CSS](https://tailwindcss.com/) is a utility-first CSS framework that works exceptionally well with Next.js.

## [Installing Tailwind](#installing-tailwind)

Install the Tailwind CSS packages and run the `init` command to generate both the `tailwind.config.js` and `postcss.config.js` files:

Terminal

```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

## [Configuring Tailwind](#configuring-tailwind)

Inside `tailwind.config.js`, add paths to the files that will use Tailwind CSS class names:

tailwind.config.js

```
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './app/**/*.{js,ts,jsx,tsx,mdx}', // Note the addition of the `app` directory.
    './pages/**/*.{js,ts,jsx,tsx,mdx}',
    './components/**/*.{js,ts,jsx,tsx,mdx}',
 
    // Or if using `src` directory:
    './src/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

You do not need to modify `postcss.config.js`.

## [Importing Styles](#importing-styles-1)

Add the [Tailwind CSS directives](https://tailwindcss.com/docs/functions-and-directives#directives) that Tailwind will use to inject its generated styles to a [Global Stylesheet](/docs/14/pages/building-your-application/styling/css-modules#global-styles) in your application, for example:

styles/globals.css

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Inside the [custom app file](/docs/14/pages/building-your-application/routing/custom-app) (`pages/_app.js`), import the `globals.css` stylesheet to apply the styles to every route in your application.

pages/\_app.tsx

TypeScript

JavaScriptTypeScript

```
// These styles apply to every route in the application
import '@/styles/globals.css'
import type { AppProps } from 'next/app'
 
export default function App({ Component, pageProps }: AppProps) {
  return <Component {...pageProps} />
}
```

## [Using Classes](#using-classes-1)

After installing Tailwind CSS and adding the global styles, you can use Tailwind's utility classes in your application.

pages/index.tsx

TypeScript

JavaScriptTypeScript

```
export default function Page() {
  return <h1 className="text-3xl font-bold underline">Hello, Next.js!</h1>
}
```

## [Usage with Turbopack](#usage-with-turbopack)

As of Next.js 13.1, Tailwind CSS and PostCSS are supported with [Turbopack](https://turbo.build/pack/docs/features/css#tailwind-css).

Was this helpful?

supported.

Send
