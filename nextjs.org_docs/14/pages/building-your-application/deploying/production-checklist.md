---
title: "Production Checklist"
source: "https://nextjs.org/docs/14/pages/building-your-application/deploying/production-checklist"
---

# Production Checklist

Menu

Pages Router 14

Using Pages Router

Features available in /pages

Version 14

14.2.33

[Building Your Application](/docs/14/pages/building-your-application)[Deploying](/docs/14/pages/building-your-application/deploying)Production Checklist

You are currently viewing the Pages Router documentation for version 14 of Next.js.

# Production Checklist

Before taking your Next.js application to production, there are some optimizations and patterns you should consider implementing for the best user experience, performance, and security.

This page provides best practices that you can use as a reference when [building your application](#during-development), [before going to production](#before-going-to-production), and [after deployment](#after-deployment) - as well as the [automatic Next.js optimizations](#automatic-optimizations) you should be aware of.

## [Automatic optimizations](#automatic-optimizations)

These Next.js optimizations are enabled by default and require no configuration:

- **[Code-splitting](/docs/14/pages/building-your-application/routing/pages-and-layouts):** Next.js automatically code-splits your application code by pages. This means only the code needed for the current page is loaded on navigation. You may also consider [lazy loading](/docs/14/pages/building-your-application/optimizing/lazy-loading) third-party libraries, where appropriate.
- **[Prefetching](/docs/14/pages/api-reference/components/link#prefetch):** When a link to a new route enters the user's viewport, Next.js prefetches the route in background. This makes navigation to new routes almost instant. You can opt out of prefetching, where appropriate.
- **[Automatic Static Optimization](/docs/14/pages/building-your-application/rendering/automatic-static-optimization):** Next.js automatically determines that a page is static (can be pre-rendered) if it has no blocking data requirements. Optimized pages can be cached, and served to the end-user from multiple CDN locations. You may opt into [Server-side Rendering](/docs/14/pages/building-your-application/data-fetching/get-server-side-props), where appropriate.

These defaults aim to improve your application's performance, and reduce the cost and amount of data transferred on each network request.

## [During development](#during-development)

While building your application, we recommend using the following features to ensure the best performance and user experience:

### [Routing and rendering](#routing-and-rendering)

- **[`<Link>` component](/docs/14/pages/building-your-application/routing/linking-and-navigating):** Use the `<Link>` component for client-side navigation and prefetching.
- **[Custom Errors](/docs/14/pages/building-your-application/routing/custom-error):** Gracefully handle [500](/docs/14/pages/building-your-application/routing/custom-error#500-page) and [404 errors](/docs/14/pages/building-your-application/routing/custom-error#404-page)

### [Data fetching and caching](#data-fetching-and-caching)

- **[API Routes](/docs/14/pages/building-your-application/routing/api-routes):** Use Route Handlers to access your backend resources, and prevent sensitive secrets from being exposed to the client.
- **[Data Caching](/docs/14/pages/building-your-application/data-fetching/get-static-props):** Verify whether your data requests are being cached or not, and opt into caching, where appropriate. Ensure requests that don't use `getStaticProps` are cached where appropriate.
- **[Incremental Static Regeneration](/docs/14/pages/building-your-application/data-fetching/incremental-static-regeneration):** Use Incremental Static Regeneration to update static pages after they've been built, without rebuilding your entire site.
- **[Static Images](/docs/14/pages/building-your-application/optimizing/static-assets):** Use the `public` directory to automatically cache your application's static assets, e.g. images.

### [UI and accessibility](#ui-and-accessibility)

- **[Font Module](/docs/14/app/building-your-application/optimizing/fonts):** Optimize fonts by using the Font Module, which automatically hosts your font files with other static assets, removes external network requests, and reduces [layout shift](https://web.dev/articles/cls).
- **[`<Image>` Component](/docs/14/app/building-your-application/optimizing/images):** Optimize images by using the Image Component, which automatically optimizes images, prevents layout shift, and serves them in modern formats like WebP or AVIF.
- **[`<Script>` Component](/docs/14/app/building-your-application/optimizing/scripts):** Optimize third-party scripts by using the Script Component, which automatically defers scripts and prevents them from blocking the main thread.
- **[ESLint](/docs/14/architecture/accessibility#linting):** Use the built-in `eslint-plugin-jsx-a11y` plugin to catch accessibility issues early.

### [Security](#security)

- **[Environment Variables](/docs/14/app/building-your-application/configuring/environment-variables):** Ensure your `.env.*` files are added to `.gitignore` and only public variables are prefixed with `NEXT_PUBLIC_`.
- **[Content Security Policy](/docs/14/app/building-your-application/configuring/content-security-policy):** Consider adding a Content Security Policy to protect your application against various security threats such as cross-site scripting, clickjacking, and other code injection attacks.

### [Metadata and SEO](#metadata-and-seo)

- **[`<Head>` Component](/docs/14/pages/api-reference/components/head):** Use the `next/head` component to add page titles, descriptions, and more.

### [Type safety](#type-safety)

- **TypeScript and [TS Plugin](/docs/14/app/building-your-application/configuring/typescript):** Use TypeScript and the TypeScript plugin for better type-safety, and to help you catch errors early.

## [Before going to production](#before-going-to-production)

Before going to production, you can run `next build` to build your application locally and catch any build errors, then run `next start` to measure the performance of your application in a production-like environment.

### [Core Web Vitals](#core-web-vitals)

- **[Lighthouse](https://developers.google.com/web/tools/lighthouse):** Run lighthouse in incognito to gain a better understanding of how your users will experience your site, and to identify areas for improvement. This is a simulated test and should be paired with looking at field data (such as Core Web Vitals).

### [Analyzing bundles](#analyzing-bundles)

Use the [`@next/bundle-analyzer` plugin](/docs/14/app/building-your-application/optimizing/bundle-analyzer) to analyze the size of your JavaScript bundles and identify large modules and dependencies that might be impacting your application's performance.

Additionally, the following tools can you understand the impact of adding new dependencies to your application:

- [Import Cost](https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost)
- [Package Phobia](https://packagephobia.com/)
- [Bundle Phobia](https://bundlephobia.com/)
- [bundlejs](https://bundlejs.com/)

## [After deployment](#after-deployment)

Depending on where you deploy your application, you might have access to additional tools and integrations to help you monitor and improve your application's performance.

For Vercel deployments, we recommend the following:

- **[Analytics](https://vercel.com/analytics?utm_source=next-site&utm_campaign=nextjs-docs&utm_medium=docs):** A built-in analytics dashboard to help you understand your application's traffic, including the number of unique visitors, page views, and more.
- **[Speed Insights](https://vercel.com/docs/speed-insights?utm_source=next-site&utm_campaign=nextjs-docs&utm_medium=docs):** Real-world performance insights based on visitor data, offering a practical view of how your website is performing in the field.
- **[Logging](https://vercel.com/docs/observability/runtime-logs?utm_source=next-site&utm_campaign=nextjs-docs&utm_medium=docs):** Runtime and Activity logs to help you debug issues and monitor your application in production. Alternatively, see the [integrations page](https://vercel.com/integrations?utm_source=next-site&utm_campaign=nextjs-docs&utm_medium=docs) for a list of third-party tools and services.

> **Good to know:**
> 
> To get a comprehensive understanding of the best practices for production deployments on Vercel, including detailed strategies for improving website performance, refer to the [Vercel Production Checklist](https://vercel.com/docs/production-checklist?utm_source=next-site&utm_campaign=nextjs-docs&utm_medium=docs).

Following these recommendations will help you build a faster, more reliable, and secure application for your users.

Was this helpful?

supported.

Send
