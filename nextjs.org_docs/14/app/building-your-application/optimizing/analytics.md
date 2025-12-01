---
title: "Analytics"
source: "https://nextjs.org/docs/14/app/building-your-application/optimizing/analytics"
---

# Analytics

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[Building Your Application](/docs/14/app/building-your-application)[Optimizing](/docs/14/app/building-your-application/optimizing)Analytics

You are currently viewing documentation for version 14 of Next.js.

# Analytics

Next.js has built-in support for measuring and reporting performance metrics. You can either use the `useReportWebVitals` hook to manage reporting yourself, or alternatively, Vercel provides a [managed service](https://vercel.com/analytics?utm_source=next-site&utm_medium=docs&utm_campaign=next-website) to automatically collect and visualize metrics for you.

## [Build Your Own](#build-your-own)

app/\_components/web-vitals.js

```
'use client'
 
import { useReportWebVitals } from 'next/web-vitals'
 
export function WebVitals() {
  useReportWebVitals((metric) => {
    console.log(metric)
  })
}
```

app/layout.js

```
import { WebVitals } from './_components/web-vitals'
 
export default function Layout({ children }) {
  return (
    <html>
      <body>
        <WebVitals />
        {children}
      </body>
    </html>
  )
}
```

> Since the `useReportWebVitals` hook requires the `"use client"` directive, the most performant approach is to create a separate component that the root layout imports. This confines the client boundary exclusively to the `WebVitals` component.

View the [API Reference](/docs/14/app/api-reference/functions/use-report-web-vitals) for more information.

## [Web Vitals](#web-vitals)

[Web Vitals](https://web.dev/vitals/) are a set of useful metrics that aim to capture the user experience of a web page. The following web vitals are all included:

- [Time to First Byte](https://developer.mozilla.org/docs/Glossary/Time_to_first_byte) (TTFB)
- [First Contentful Paint](https://developer.mozilla.org/docs/Glossary/First_contentful_paint) (FCP)
- [Largest Contentful Paint](https://web.dev/lcp/) (LCP)
- [First Input Delay](https://web.dev/fid/) (FID)
- [Cumulative Layout Shift](https://web.dev/cls/) (CLS)
- [Interaction to Next Paint](https://web.dev/inp/) (INP)

You can handle all the results of these metrics using the `name` property.

app/\_components/web-vitals.tsx

TypeScript

JavaScriptTypeScript

```
'use client'
 
import { useReportWebVitals } from 'next/web-vitals'
 
export function WebVitals() {
  useReportWebVitals((metric) => {
    switch (metric.name) {
      case 'FCP': {
        // handle FCP results
      }
      case 'LCP': {
        // handle LCP results
      }
      // ...
    }
  })
}
```

## [Sending results to external systems](#sending-results-to-external-systems)

You can send results to any endpoint to measure and track real user performance on your site. For example:

```
useReportWebVitals((metric) => {
  const body = JSON.stringify(metric)
  const url = 'https://example.com/analytics'
 
  // Use `navigator.sendBeacon()` if available, falling back to `fetch()`.
  if (navigator.sendBeacon) {
    navigator.sendBeacon(url, body)
  } else {
    fetch(url, { body, method: 'POST', keepalive: true })
  }
})
```

> **Good to know**: If you use [Google Analytics](https://analytics.google.com/analytics/web/), using the `id` value can allow you to construct metric distributions manually (to calculate percentiles, etc.)

> ```
> useReportWebVitals((metric) => {
  // Use `window.gtag` if you initialized Google Analytics as this example:
  // https://github.com/vercel/next.js/blob/canary/examples/with-google-analytics/pages/_app.js
  window.gtag('event', metric.name, {
    value: Math.round(
      metric.name === 'CLS' ? metric.value * 1000 : metric.value
    ), // values must be integers
    event_label: metric.id, // id unique to current page load
    non_interaction: true, // avoids affecting bounce rate.
  })
})
> ```
> 
> Read more about [sending results to Google Analytics](https://github.com/GoogleChrome/web-vitals#send-the-results-to-google-analytics).

Was this helpful?

supported.

Send
