---
title: "optimizePackageImports"
source: "https://nextjs.org/docs/13/app/api-reference/next-config-js/optimizePackageImports"
---

# optimizePackageImports

Menu

App Router 13

Using App Router

Features available in /app

Version 13

13.5.11

[API Reference](/docs/13/app/api-reference)[next.config.js Options](/docs/13/app/api-reference/next-config-js)optimizePackageImports

You are currently viewing documentation for version 13 of Next.js.

# optimizePackageImports

Some packages can export hundreds or thousands of modules, which can cause performance issues in development and production.

Adding a package to `experimental.optimizePackageImports` will only load the modules you are actually using, while still giving you the convenience of writing import statements with many named exports.

next.config.js

```
module.exports = {
  experimental: {
    optimizePackageImports: ['package-name'],
  },
}
```

Libraries like `@mui/icons-material`, `@mui/material`, `date-fns`, `lodash`, `lodash-es`, `react-bootstrap`, `@headlessui/react`, `@heroicons/react`, and `lucide-react` are already optimized by default.

Was this helpful?

supported.

Send
