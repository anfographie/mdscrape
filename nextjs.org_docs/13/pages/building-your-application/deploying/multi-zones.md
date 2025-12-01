---
title: "Multi Zones"
source: "https://nextjs.org/docs/13/pages/building-your-application/deploying/multi-zones"
---

# Multi Zones

Menu

Pages Router 13

Using Pages Router

Features available in /pages

Version 13

13.5.11

[Building Your Application](/docs/13/pages/building-your-application)[Deploying](/docs/13/pages/building-your-application/deploying)Multi Zones

You are currently viewing the Pages Router documentation for version 13 of Next.js.

# Multi Zones

Examples

- [With Zones](https://github.com/vercel/next.js/tree/canary/examples/with-zones)

A zone is a single deployment of a Next.js app. You can have multiple zones and merge them as a single app.

For example, let's say you have the following apps:

- An app for serving `/blog/**`
- Another app for serving all other pages

With multi zones support, you can merge both these apps into a single one allowing your customers to browse it using a single URL, but you can develop and deploy both apps independently.

## [How to define a zone](#how-to-define-a-zone)

There are no zone related APIs. You only need to do the following:

- Make sure to keep only the pages you need in your app, meaning that an app can't have pages from another app, if app `A` has `/blog` then app `B` shouldn't have it too.
- Make sure to configure a [basePath](/docs/13/app/api-reference/next-config-js/basePath) to avoid conflicts with pages and static files.

## [How to merge zones](#how-to-merge-zones)

You can merge zones using [`rewrites`](/docs/13/pages/api-reference/next-config-js/rewrites) in one of the apps or any HTTP proxy.

For [Next.js on Vercel](https://vercel.com?utm_source=next-site&utm_medium=docs&utm_campaign=next-website) applications, you can use a [monorepo](https://vercel.com/blog/monorepos-are-changing-how-teams-build-software?utm_source=next-site&utm_medium=docs&utm_campaign=next-website) to deploy both apps with a single `git push`.

Was this helpful?

supported.

Send
