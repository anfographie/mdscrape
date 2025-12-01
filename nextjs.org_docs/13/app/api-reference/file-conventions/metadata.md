---
title: "Metadata Files API Reference"
source: "https://nextjs.org/docs/13/app/api-reference/file-conventions/metadata"
---

# Metadata Files API Reference

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[File Conventions](/docs/13/app/api-reference/file-conventions)Metadata Files

You are currently viewing documentation for version 13 of Next.js.

# Metadata Files API Reference

This section of the docs covers **Metadata file conventions**. File-based metadata can be defined by adding special metadata files to route segments.

Each file convention can be defined using a static file (e.g. `opengraph-image.jpg`), or a dynamic variant that uses code to generate the file (e.g. `opengraph-image.js`).

Once a file is defined, Next.js will automatically serve the file (with hashes in production for caching) and update the relevant head elements with the correct metadata, such as the asset's URL, file type, and image size.

[**favicon, icon, and apple-icon**  
\
API Reference for the Favicon, Icon and Apple Icon file conventions.](/docs/13/app/api-reference/file-conventions/metadata/app-icons)

[**manifest.json**  
\
API Reference for manifest.json file.](/docs/13/app/api-reference/file-conventions/metadata/manifest)

[**opengraph-image and twitter-image**  
\
API Reference for the Open Graph Image and Twitter Image file conventions.](/docs/13/app/api-reference/file-conventions/metadata/opengraph-image)

[**robots.txt**  
\
API Reference for robots.txt file.](/docs/13/app/api-reference/file-conventions/metadata/robots)

[**sitemap.xml**  
\
API Reference for the sitemap.xml file.](/docs/13/app/api-reference/file-conventions/metadata/sitemap)

Was this helpful?

supported.

Send
