---
title: "Setting up Vitest with Next.js"
source: "https://nextjs.org/docs/14/app/building-your-application/testing/vitest"
---

# Setting up Vitest with Next.js

Menu

App Router 14

Using App Router

Features available in /app

Version 14

14.2.33

[Building Your Application](/docs/14/app/building-your-application)[Testing](/docs/14/app/building-your-application/testing)Vitest

You are currently viewing documentation for version 14 of Next.js.

# Setting up Vitest with Next.js

Vite and React Testing Library are frequently used together for **Unit Testing**. This guide will show you how to setup Vitest with Next.js and write your first tests.

> **Good to know:** Since `async` Server Components are new to the React ecosystem, Vitest currently does not support them. While you can still run **unit tests** for synchronous Server and Client Components, we recommend using an **E2E tests** for `async` components.

## [Quickstart](#quickstart)

You can use `create-next-app` with the Next.js [with-vitest](https://github.com/vercel/next.js/tree/canary/examples/with-vitest) example to quickly get started:

Terminal

```
npx create-next-app@latest --example with-vitest with-vitest-app
```

## [Manual Setup](#manual-setup)

To manually set up Vitest, install `vitest` and the following packages as dev dependencies:

Terminal

```
npm install -D vitest @vitejs/plugin-react jsdom @testing-library/react
# or
yarn add -D vitest @vitejs/plugin-react jsdom @testing-library/react
# or
pnpm install -D vitest @vitejs/plugin-react jsdom @testing-library/react
# or
bun add -D vitest @vitejs/plugin-react jsdom @testing-library/react
```

Create a `vitest.config.ts|js` file in the root of your project, and add the following options:

vitest.config.ts

TypeScript

JavaScriptTypeScript

```
import { defineConfig } from 'vitest/config'
import react from '@vitejs/plugin-react'
 
export default defineConfig({
  plugins: [react()],
  test: {
    environment: 'jsdom',
  },
})
```

For more information on configuring Vitest, please refer to the [Vitest Configuration](https://vitest.dev/config/#configuration) docs.

Then, add a `test` script to your `package.json`:

package.json

```
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "test": "vitest"
  }
}
```

When you run `npm run test`, Vitest will **watch** for changes in your project by default.

## [Creating your first Vitest Unit Test](#creating-your-first-vitest-unit-test)

Check that everything is working by creating a test to check if the `<Page />` component successfully renders a heading:

app/page.tsx

TypeScript

JavaScriptTypeScript

```
import Link from 'next/link'
 
export default function Page() {
  return (
    <div>
      <h1>Home</h1>
      <Link href="/about">About</Link>
    </div>
  )
}
```

\_\_tests\_\_/page.test.tsx

TypeScript

JavaScriptTypeScript

```
import { expect, test } from 'vitest'
import { render, screen } from '@testing-library/react'
import Page from '../app/page'
 
test('Page', () => {
  render(<Page />)
  expect(screen.getByRole('heading', { level: 1, name: 'Home' })).toBeDefined()
})
```

> **Good to know**: The example above uses the common `__tests__` convention, but test files can also be colocated inside the `app` router.

## [Running your tests](#running-your-tests)

Then, run the following command to run your tests:

Terminal

```
npm run test
# or
yarn test
# or
pnpm test
# or
bun test
```

## [Additional Resources](#additional-resources)

You may find these resources helpful:

- [Next.js with Vitest example](https://github.com/vercel/next.js/tree/canary/examples/with-vitest)
- [Vitest Docs](https://vitest.dev/guide/)
- [React Testing Library Docs](https://testing-library.com/docs/react-testing-library/intro/)

Was this helpful?

supported.

Send
