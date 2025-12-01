---
title: "Next.js Project Structure"
source: "https://nextjs.org/docs/14/getting-started/project-structure"
---

# Next.js Project Structure

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[Introduction](/docs/14)[Getting Started](/docs/14/getting-started)Project Structure

You are currently viewing documentation for version 14 of Next.js.

# Next.js Project Structure

This page provides an overview of the project structure of a Next.js application. It covers top-level files and folders, configuration files, and routing conventions within the `app` and `pages` directories.

Click the file and folder names to learn more about each convention.

## [Top-level folders](#top-level-folders)

Top-level folders are used to organize your application's code and static assets.

![Route segments to path segments](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Flight%2Ftop-level-folders.png&w=3840&q=75)![Route segments to path segments](/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Ftop-level-folders.png&w=3840&q=75)

[`app`](/docs/14/app/building-your-application/routing)App Router[`pages`](/docs/14/pages/building-your-application/routing)Pages Router[`public`](/docs/14/app/building-your-application/optimizing/static-assets)Static assets to be served[`src`](/docs/14/app/building-your-application/configuring/src-directory)Optional application source folder

## [Top-level files](#top-level-files)

Top-level files are used to configure your application, manage dependencies, run middleware, integrate monitoring tools, and define environment variables.

**Next.js**[`next.config.js`](/docs/14/app/api-reference/next-config-js)Configuration file for Next.js[`package.json`](/docs/14/getting-started/installation#manual-installation)Project dependencies and scripts[`instrumentation.ts`](/docs/14/app/building-your-application/optimizing/instrumentation)OpenTelemetry and Instrumentation file[`middleware.ts`](/docs/14/app/building-your-application/routing/middleware)Next.js request middleware[`.env`](/docs/14/app/building-your-application/configuring/environment-variables)Environment variables[`.env.local`](/docs/14/app/building-your-application/configuring/environment-variables)Local environment variables[`.env.production`](/docs/14/app/building-your-application/configuring/environment-variables)Production environment variables[`.env.development`](/docs/14/app/building-your-application/configuring/environment-variables)Development environment variables[`.eslintrc.json`](/docs/14/app/building-your-application/configuring/eslint)Configuration file for ESLint`.gitignore`Git files and folders to ignore`next-env.d.ts`TypeScript declaration file for Next.js`tsconfig.json`Configuration file for TypeScript`jsconfig.json`Configuration file for JavaScript

## [`app` Routing Conventions](#app-routing-conventions)

The following file conventions are used to define routes and handle metadata in the [`app` router](/docs/14/app).

### [Routing Files](#routing-files)

[`layout`](/docs/14/app/api-reference/file-conventions/layout)`.js` `.jsx` `.tsx`Layout[`page`](/docs/14/app/api-reference/file-conventions/page)`.js` `.jsx` `.tsx`Page[`loading`](/docs/14/app/api-reference/file-conventions/loading)`.js` `.jsx` `.tsx`Loading UI[`not-found`](/docs/14/app/api-reference/file-conventions/not-found)`.js` `.jsx` `.tsx`Not found UI[`error`](/docs/14/app/api-reference/file-conventions/error)`.js` `.jsx` `.tsx`Error UI[`global-error`](/docs/14/app/api-reference/file-conventions/error#global-errorjs)`.js` `.jsx` `.tsx`Global error UI[`route`](/docs/14/app/api-reference/file-conventions/route)`.js` `.ts`API endpoint[`template`](/docs/14/app/api-reference/file-conventions/template)`.js` `.jsx` `.tsx`Re-rendered layout[`default`](/docs/14/app/api-reference/file-conventions/default)`.js` `.jsx` `.tsx`Parallel route fallback page

### [Nested Routes](#nested-routes)

[`folder`](/docs/14/app/building-your-application/routing#route-segments)Route segment[`folder/folder`](/docs/14/app/building-your-application/routing#nested-routes)Nested route segment

### [Dynamic Routes](#dynamic-routes)

[`[folder]`](/docs/14/app/building-your-application/routing/dynamic-routes#convention)Dynamic route segment[`[...folder]`](/docs/14/app/building-your-application/routing/dynamic-routes#catch-all-segments)Catch-all route segment[`[[...folder]]`](/docs/14/app/building-your-application/routing/dynamic-routes#optional-catch-all-segments)Optional catch-all route segment

### [Route Groups and Private Folders](#route-groups-and-private-folders)

[`(folder)`](/docs/14/app/building-your-application/routing/route-groups#convention)Group routes without affecting routing[`_folder`](/docs/14/app/building-your-application/routing/colocation#private-folders)Opt folder and all child segments out of routing

### [Parallel and Intercepted Routes](#parallel-and-intercepted-routes)

[`@folder`](/docs/14/app/building-your-application/routing/parallel-routes#slots)Named slot[`(.)folder`](/docs/14/app/building-your-application/routing/intercepting-routes#convention)Intercept same level[`(..)folder`](/docs/14/app/building-your-application/routing/intercepting-routes#convention)Intercept one level above[`(..)(..)folder`](/docs/14/app/building-your-application/routing/intercepting-routes#convention)Intercept two levels above[`(...)folder`](/docs/14/app/building-your-application/routing/intercepting-routes#convention)Intercept from root

### [Metadata File Conventions](#metadata-file-conventions)

#### [App Icons](#app-icons)

[`favicon`](/docs/14/app/api-reference/file-conventions/metadata/app-icons#favicon)`.ico`Favicon file[`icon`](/docs/14/app/api-reference/file-conventions/metadata/app-icons#icon)`.ico` `.jpg` `.jpeg` `.png` `.svg`App Icon file[`icon`](/docs/14/app/api-reference/file-conventions/metadata/app-icons#generate-icons-using-code-js-ts-tsx)`.js` `.ts` `.tsx`Generated App Icon[`apple-icon`](/docs/14/app/api-reference/file-conventions/metadata/app-icons#apple-icon)`.jpg` `.jpeg`, `.png`Apple App Icon file[`apple-icon`](/docs/14/app/api-reference/file-conventions/metadata/app-icons#generate-icons-using-code-js-ts-tsx)`.js` `.ts` `.tsx`Generated Apple App Icon

#### [Open Graph and Twitter Images](#open-graph-and-twitter-images)

[`opengraph-image`](/docs/14/app/api-reference/file-conventions/metadata/opengraph-image#opengraph-image)`.jpg` `.jpeg` `.png` `.gif`Open Graph image file[`opengraph-image`](/docs/14/app/api-reference/file-conventions/metadata/opengraph-image#generate-images-using-code-js-ts-tsx)`.js` `.ts` `.tsx`Generated Open Graph image[`twitter-image`](/docs/14/app/api-reference/file-conventions/metadata/opengraph-image#twitter-image)`.jpg` `.jpeg` `.png` `.gif`Twitter image file[`twitter-image`](/docs/14/app/api-reference/file-conventions/metadata/opengraph-image#generate-images-using-code-js-ts-tsx)`.js` `.ts` `.tsx`Generated Twitter image

#### [SEO](#seo)

[`sitemap`](/docs/14/app/api-reference/file-conventions/metadata/sitemap#sitemap-files-xml)`.xml`Sitemap file[`sitemap`](/docs/14/app/api-reference/file-conventions/metadata/sitemap#generating-a-sitemap-using-code-js-ts)`.js` `.ts`Generated Sitemap[`robots`](/docs/14/app/api-reference/file-conventions/metadata/robots#static-robotstxt)`.txt`Robots file[`robots`](/docs/14/app/api-reference/file-conventions/metadata/robots#generate-a-robots-file)`.js` `.ts`Generated Robots file

## [`pages` Routing Conventions](#pages-routing-conventions)

The following file conventions are used to define routes in the [`pages` router](/docs/14/pages).

### [Special Files](#special-files)

[`_app`](/docs/14/pages/building-your-application/routing/custom-app)`.js` `.jsx` `.tsx`Custom App[`_document`](/docs/14/pages/building-your-application/routing/custom-document)`.js` `.jsx` `.tsx`Custom Document[`_error`](/docs/14/pages/building-your-application/routing/custom-error#more-advanced-error-page-customizing)`.js` `.jsx` `.tsx`Custom Error Page[`404`](/docs/14/pages/building-your-application/routing/custom-error#404-page)`.js` `.jsx` `.tsx`404 Error Page[`500`](/docs/14/pages/building-your-application/routing/custom-error#500-page)`.js` `.jsx` `.tsx`500 Error Page

### [Routes](#routes)

**Folder convention**[`index`](/docs/14/pages/building-your-application/routing/pages-and-layouts#index-routes)`.js` `.jsx` `.tsx`Home page[`folder/index`](/docs/14/pages/building-your-application/routing/pages-and-layouts#index-routes)`.js` `.jsx` `.tsx`Nested page**File convention**[`index`](/docs/14/pages/building-your-application/routing/pages-and-layouts#index-routes)`.js` `.jsx` `.tsx`Home page[`file`](/docs/14/pages/building-your-application/routing/pages-and-layouts)`.js` `.jsx` `.tsx`Nested page

### [Dynamic Routes](#dynamic-routes-1)

**Folder convention**[`[folder]/index`](/docs/14/pages/building-your-application/routing/dynamic-routes)`.js` `.jsx` `.tsx`Dynamic route segment[`[...folder]/index`](/docs/14/pages/building-your-application/routing/dynamic-routes#catch-all-segments)`.js` `.jsx` `.tsx`Catch-all route segment[`[[...folder]]/index`](/docs/14/pages/building-your-application/routing/dynamic-routes#optional-catch-all-segments)`.js` `.jsx` `.tsx`Optional catch-all route segment**File convention**[`[file]`](/docs/14/pages/building-your-application/routing/dynamic-routes)`.js` `.jsx` `.tsx`Dynamic route segment[`[...file]`](/docs/14/pages/building-your-application/routing/dynamic-routes#catch-all-segments)`.js` `.jsx` `.tsx`Catch-all route segment[`[[...file]]`](/docs/14/pages/building-your-application/routing/dynamic-routes#optional-catch-all-segments)`.js` `.jsx` `.tsx`Optional catch-all route segment

Was this helpful?

supported.

Send
