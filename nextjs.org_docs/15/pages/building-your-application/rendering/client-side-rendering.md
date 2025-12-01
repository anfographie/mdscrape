---
title: "Client-side Rendering (CSR)"
source: "https://nextjs.org/docs/15/pages/building-your-application/rendering/client-side-rendering"
---

# Client-side Rendering (CSR)

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Building Your Application](/docs/15/pages/building-your-application)[Rendering](/docs/15/pages/building-your-application/rendering)Client-side Rendering (CSR)

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# Client-side Rendering (CSR)

In Client-Side Rendering (CSR) with React, the browser downloads a minimal HTML page and the JavaScript needed for the page. The JavaScript is then used to update the DOM and render the page. When the application is first loaded, the user may notice a slight delay before they can see the full page, this is because the page isn't fully rendered until all the JavaScript is downloaded, parsed, and executed.

After the page has been loaded for the first time, navigating to other pages on the same website is typically faster, as only necessary data needs to be fetched, and JavaScript can re-render parts of the page without requiring a full page refresh.

In Next.js, there are two ways you can implement client-side rendering:

1. Using React's `useEffect()` hook inside your pages instead of the server-side rendering methods ([`getStaticProps`](/docs/15/pages/building-your-application/data-fetching/get-static-props) and [`getServerSideProps`](/docs/15/pages/building-your-application/data-fetching/get-server-side-props)).
2. Using a data fetching library like [SWR](https://swr.vercel.app/) or [TanStack Query](https://tanstack.com/query/latest/) to fetch data on the client (recommended).

Here's an example of using `useEffect()` inside a Next.js page:

pages/index.js

```
import React, { useState, useEffect } from 'react'
 
export function Page() {
  const [data, setData] = useState(null)
 
  useEffect(() => {
    const fetchData = async () => {
      const response = await fetch('https://api.example.com/data')
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`)
      }
      const result = await response.json()
      setData(result)
    }
 
    fetchData().catch((e) => {
      // handle the error as needed
      console.error('An error occurred while fetching the data: ', e)
    })
  }, [])
 
  return <p>{data ? `Your data: ${data}` : 'Loading...'}</p>
}
```

In the example above, the component starts by rendering `Loading...`. Then, once the data is fetched, it re-renders and displays the data.

Although fetching data in a `useEffect` is a pattern you may see in older React Applications, we recommend using a data-fetching library for better performance, caching, optimistic updates, and more. Here's a minimum example using [SWR](https://swr.vercel.app/) to fetch data on the client:

pages/index.js

```
import useSWR from 'swr'
 
export function Page() {
  const { data, error, isLoading } = useSWR(
    'https://api.example.com/data',
    fetcher
  )
 
  if (error) return <p>Failed to load.</p>
  if (isLoading) return <p>Loading...</p>
 
  return <p>Your Data: {data}</p>
}
```

> **Good to know**:
> 
> Keep in mind that CSR can impact SEO. Some search engine crawlers might not execute JavaScript and therefore only see the initial empty or loading state of your application. It can also lead to performance issues for users with slower internet connections or devices, as they need to wait for all the JavaScript to load and run before they can see the full page. Next.js promotes a hybrid approach that allows you to use a combination of [server-side rendering](/docs/15/pages/building-your-application/rendering/server-side-rendering), [static site generation](/docs/15/pages/building-your-application/rendering/static-site-generation), and client-side rendering, **depending on the needs of each page** in your application. In the App Router, you can also use [Loading UI with Suspense](/docs/15/app/api-reference/file-conventions/loading) to show a loading indicator while the page is being rendered.

## Next Steps

Learn about the alternative rendering methods in Next.js.

[Next.js Docs  
\
...  
\
Rendering  
\
**Server-side Rendering (SSR)**  
\
Use Server-side Rendering to render pages on each request.](/docs/15/pages/building-your-application/rendering/server-side-rendering)

[Next.js Docs  
\
...  
\
Rendering  
\
**Static Site Generation (SSG)**  
\
Use Static Site Generation (SSG) to pre-render pages at build time.](/docs/15/pages/building-your-application/rendering/static-site-generation)

[Next.js Docs  
\
...  
\
Guides  
\
**ISR**  
\
Learn how to create or update static pages at runtime with Incremental Static Regeneration.](/docs/15/pages/guides/incremental-static-regeneration)

Was this helpful?

supported.

Send
