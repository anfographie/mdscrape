---
title: "draftMode"
source: "https://nextjs.org/docs/13/app/api-reference/functions/draft-mode"
---

# draftMode

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[Functions](/docs/13/app/api-reference/functions)draftMode

You are currently viewing documentation for version 13 of Next.js.

# draftMode

The `draftMode` function allows you to detect [Draft Mode](/docs/13/app/building-your-application/configuring/draft-mode) inside a [Server Component](/docs/13/app/building-your-application/rendering/server-components).

app/page.js

```
import { draftMode } from 'next/headers'
 
export default function Page() {
  const { isEnabled } = draftMode()
  return (
    <main>
      <h1>My Blog Post</h1>
      <p>Draft Mode is currently {isEnabled ? 'Enabled' : 'Disabled'}</p>
    </main>
  )
}
```

## [Version History](#version-history)

VersionChanges`v13.4.0``draftMode` introduced.

Was this helpful?

supported.

Send
