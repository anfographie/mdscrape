---
title: "<Head>"
source: "https://nextjs.org/docs/13/pages/api-reference/components/head"
---

# <Head>

Menu

Pages Router 13

Using Pages Router

Features available in /pages

Version 13

13.5.11

[API Reference](/docs/13/pages/api-reference)[Components](/docs/13/pages/api-reference/components)&lt;Head&gt;

You are currently viewing the Pages Router documentation for version 13 of Next.js.

# &lt;Head&gt;

Examples

- [Head Elements](https://github.com/vercel/next.js/tree/canary/examples/head-elements)
- [Layout Component](https://github.com/vercel/next.js/tree/canary/examples/layout-component)

We expose a built-in component for appending elements to the `head` of the page:

```
import Head from 'next/head'
 
function IndexPage() {
  return (
    <div>
      <Head>
        <title>My page title</title>
      </Head>
      <p>Hello world!</p>
    </div>
  )
}
 
export default IndexPage
```

To avoid duplicate tags in your `head` you can use the `key` property, which will make sure the tag is only rendered once, as in the following example:

```
import Head from 'next/head'
 
function IndexPage() {
  return (
    <div>
      <Head>
        <title>My page title</title>
        <meta property="og:title" content="My page title" key="title" />
      </Head>
      <Head>
        <meta property="og:title" content="My new title" key="title" />
      </Head>
      <p>Hello world!</p>
    </div>
  )
}
 
export default IndexPage
```

In this case only the second `<meta property="og:title" />` is rendered. `meta` tags with duplicate `key` attributes are automatically handled.

> The contents of `head` get cleared upon unmounting the component, so make sure each page completely defines what it needs in `head`, without making assumptions about what other pages added.

`title`, `meta` or any other elements (e.g. `script`) need to be contained as **direct** children of the `Head` element, or wrapped into maximum one level of `<React.Fragment>` or arrays—otherwise the tags won't be correctly picked up on client-side navigations.

> We recommend using [next/script](/docs/13/pages/building-your-application/optimizing/scripts) in your component instead of manually creating a `<script>` in `next/head`.

Was this helpful?

supported.

Send
