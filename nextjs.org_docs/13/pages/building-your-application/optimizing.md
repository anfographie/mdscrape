---
title: "Optimizations"
source: "https://nextjs.org/docs/13/pages/building-your-application/optimizing"
---

# Optimizations

Menu

Pages Router 13

Using Pages Router

Features available in /pages

Version 13

13.5.11

[Pages Router](/docs/13/pages)[Building Your Application](/docs/13/pages/building-your-application)Optimizing

You are currently viewing the Pages Router documentation for version 13 of Next.js.

# Optimizations

Next.js comes with a variety of built-in optimizations designed to improve your application's speed and [Core Web Vitals](https://web.dev/vitals/). This guide will cover the optimizations you can leverage to enhance your user experience.

## [Built-in Components](#built-in-components)

Built-in components abstract away the complexity of implementing common UI optimizations. These components are:

- **Images**: Built on the native `<img>` element. The Image Component optimizes images for performance by lazy loading and automatically resizing images based on device size.
- **Link**: Built on the native `<a>` tags. The Link Component prefetches pages in the background, for faster and smoother page transitions.
- **Scripts**: Built on the native `<script>` tags. The Script Component gives you control over loading and execution of third-party scripts.

## [Metadata](#metadata)

Metadata helps search engines understand your content better (which can result in better SEO), and allows you to customize how your content is presented on social media, helping you create a more engaging and consistent user experience across various platforms.

The Head Component in Next.js allows you to modify the `<head>` of a page. Learn more in the [Head Component](/docs/13/pages/api-reference/components/head) documentation.

## [Static Assets](#static-assets)

Next.js `/public` folder can be used to serve static assets like images, fonts, and other files. Files inside `/public` can also be cached by CDN providers so that they are delivered efficiently.

## [Analytics and Monitoring](#analytics-and-monitoring)

For large applications, Next.js integrates with popular analytics and monitoring tools to help you understand how your application is performing. Learn more in the [Analytics](/docs/13/app/building-your-application/optimizing/analytics), [OpenTelemetry](/docs/13/pages/building-your-application/optimizing/open-telemetry), and [Instrumentation](/docs/13/pages/building-your-application/optimizing/instrumentation) guides.

[**Images**  
\
Optimize your images with the built-in \`next/image\` component.](/docs/13/pages/building-your-application/optimizing/images)

[**Fonts**  
\
Optimize your application's web fonts with the built-in \`next/font\` loaders.](/docs/13/pages/building-your-application/optimizing/fonts)

[**Scripts**  
\
Optimize 3rd party scripts with the built-in Script component.](/docs/13/pages/building-your-application/optimizing/scripts)

[**Static Assets**  
\
Next.js allows you to serve static files, like images, in the public directory. You can learn how it works here.](/docs/13/pages/building-your-application/optimizing/static-assets)

[**Lazy Loading**  
\
Lazy load imported libraries and React Components to improve your application's loading performance.](/docs/13/pages/building-your-application/optimizing/lazy-loading)

[**Analytics**  
\
Measure and track page performance using Next.js Speed Insights](/docs/13/pages/building-your-application/optimizing/analytics)

[**OpenTelemetry**  
\
Learn how to instrument your Next.js app with OpenTelemetry.](/docs/13/pages/building-your-application/optimizing/open-telemetry)

[**Instrumentation**  
\
Learn how to use instrumentation to run code at server startup in your Next.js app](/docs/13/pages/building-your-application/optimizing/instrumentation)

[**Testing**  
\
Learn how to set up Next.js with three commonly used testing tools — Cypress, Playwright, Jest, and React Testing Library.](/docs/13/pages/building-your-application/optimizing/testing)

Was this helpful?

supported.

Send
