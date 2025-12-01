---
title: "generateSitemaps"
source: "https://nextjs.org/docs/14/app/api-reference/functions/generate-sitemaps"
---

# generateSitemaps

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[API Reference](/docs/14/app/api-reference)[Functions](/docs/14/app/api-reference/functions)generateSitemaps

You are currently viewing documentation for version 14 of Next.js.

# generateSitemaps

You can use the `generateSitemaps` function to generate multiple sitemaps for your application.

## [Returns](#returns)

The `generateSitemaps` returns an array of objects with an `id` property.

## [URLs](#urls)

In production, your generated sitemaps will be available at `/.../sitemap/[id].xml`. For example, `/product/sitemap/1.xml`.

In development, you can view the generated sitemap on `/.../sitemap.xml/[id]`. For example, `/product/sitemap.xml/1`. This difference is temporary and will follow the production format.

## [Example](#example)

For example, to split a sitemap using `generateSitemaps`, return an array of objects with the sitemap `id`. Then, use the `id` to generate the unique sitemaps.

app/product/sitemap.ts

TypeScript

JavaScriptTypeScript

```
import { BASE_URL } from '@/app/lib/constants'
 
export async function generateSitemaps() {
  // Fetch the total number of products and calculate the number of sitemaps needed
  return [{ id: 0 }, { id: 1 }, { id: 2 }, { id: 3 }]
}
 
export default async function sitemap({
  id,
}: {
  id: number
}): Promise<MetadataRoute.Sitemap> {
  // Google's limit is 50,000 URLs per sitemap
  const start = id * 50000
  const end = start + 50000
  const products = await getProducts(
    `SELECT id, date FROM products WHERE id BETWEEN ${start} AND ${end}`
  )
  return products.map((product) => ({
    url: `${BASE_URL}/product/${product.id}`,
    lastModified: product.date,
  }))
}
```

## Next Steps

Learn how to create sitemaps for your Next.js application.

[Introduction  
\
...  
\
Metadata Files  
\
**sitemap.xml**  
\
API Reference for the sitemap.xml file.](/docs/14/app/api-reference/file-conventions/metadata/sitemap)

Was this helpful?

supported.

Send
