---
title: "Testing"
source: "https://nextjs.org/docs/14/pages/building-your-application/testing"
---

# Testing

Menu

Pages Router 14

Using Pages Router

Features available in /pages

Version 14

14.2.33

[Pages Router](/docs/14/pages)[Building Your Application](/docs/14/pages/building-your-application)Testing

You are currently viewing the Pages Router documentation for version 14 of Next.js.

# Testing

In React and Next.js, there are a few different types of tests you can write, each with its own purpose and use cases. This page provides an overview of types and commonly used tools you can use to test your application.

## [Types of tests](#types-of-tests)

- **Unit testing** involves testing individual units (or blocks of code) in isolation. In React, a unit can be a single function, hook, or component.
  
  - **Component testing** is a more focused version of unit testing where the primary subject of the tests is React components. This may involve testing how components are rendered, their interaction with props, and their behavior in response to user events.
  - **Integration testing** involves testing how multiple units work together. This can be a combination of components, hooks, and functions.
- **End-to-End (E2E) Testing** involves testing user flows in an environment that simulates real user scenarios, like the browser. This means testing specific tasks (e.g. signup flow) in a production-like environment.
- **Snapshot testing** involves capturing the rendered output of a component and saving it to a snapshot file. When tests run, the current rendered output of the component is compared against the saved snapshot. Changes in the snapshot are used to indicate unexpected changes in behavior.

## [Guides](#guides)

See the guides below to learn how to set up Next.js with these commonly used testing tools:

[**Vitest**  
\
Learn how to set up Next.js with Vitest and React Testing Library - two popular unit testing libraries.](/docs/14/pages/building-your-application/testing/vitest)

[**Jest**  
\
Learn how to set up Next.js with Jest for Unit Testing.](/docs/14/pages/building-your-application/testing/jest)

[**Playwright**  
\
Learn how to set up Next.js with Playwright for End-to-End (E2E) and Integration testing.](/docs/14/pages/building-your-application/testing/playwright)

[**Cypress**  
\
Learn how to set up Next.js with Cypress for End-to-End (E2E) and Component Testing.](/docs/14/pages/building-your-application/testing/cypress)

Was this helpful?

supported.

Send
