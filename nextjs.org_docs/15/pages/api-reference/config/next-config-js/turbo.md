---
title: "turbo"
source: "https://nextjs.org/docs/15/pages/api-reference/config/next-config-js/turbo"
---

# turbo

Menu

Pages Router 15

Using Pages Router

Features available in /pages

Version 15

15.5.6

[Configuration](/docs/15/pages/api-reference/config)[next.config.js Options](/docs/15/pages/api-reference/config/next-config-js)turbo

You are currently viewing the Pages Router documentation for version 15 of Next.js.

# turbo

This feature is currently experimental and subject to change, it's not recommended for production. Try it out and share your feedback on [GitHub](https://github.com/vercel/next.js/issues).

The `turbopack` option lets you customize [Turbopack](/docs/15/app/api-reference/turbopack) to transform different files and change how modules are resolved.

next.config.ts

TypeScript

JavaScriptTypeScript

```
import type { NextConfig } from 'next'
 
const nextConfig: NextConfig = {
  turbopack: {
    // ...
  },
}
 
export default nextConfig
```

> **Good to know**:
> 
> - Turbopack for Next.js does not require loaders or loader configuration for built-in functionality. Turbopack has built-in support for CSS and compiling modern JavaScript, so there's no need for `css-loader`, `postcss-loader`, or `babel-loader` if you're using `@babel/preset-env`.

## [Reference](#reference)

### [Options](#options)

The following options are available for the `turbo` configuration:

OptionDescription`root`Sets the application root directory. Should be an absolute path.`rules`List of supported webpack loaders to apply when running with Turbopack.`resolveAlias`Map aliased imports to modules to load in their place.`resolveExtensions`List of extensions to resolve when importing files.

### [Supported loaders](#supported-loaders)

The following loaders have been tested to work with Turbopack's webpack loader implementation, but many other webpack loaders should work as well even if not listed here:

- [`babel-loader`](https://www.npmjs.com/package/babel-loader)
- [`@svgr/webpack`](https://www.npmjs.com/package/@svgr/webpack)
- [`svg-inline-loader`](https://www.npmjs.com/package/svg-inline-loader)
- [`yaml-loader`](https://www.npmjs.com/package/yaml-loader)
- [`string-replace-loader`](https://www.npmjs.com/package/string-replace-loader)
- [`raw-loader`](https://www.npmjs.com/package/raw-loader)
- [`sass-loader`](https://www.npmjs.com/package/sass-loader)
- [`graphql-tag/loader`](https://www.npmjs.com/package/graphql-tag)

## [Examples](#examples)

### [Root directory](#root-directory)

Turbopack uses the root directory to resolve modules. Files outside of the project root are not resolved.

Next.js automatically detects the root directory of your project. It does so by looking for one of these files:

- `pnpm-lock.yaml`
- `package-lock.json`
- `yarn.lock`
- `bun.lock`
- `bun.lockb`

If you have a different project structure, for example if you don't use workspaces, you can manually set the `root` option:

next.config.js

```
const path = require('path')
module.exports = {
  turbopack: {
    root: path.join(__dirname, '..'),
  },
}
```

### [Configuring webpack loaders](#configuring-webpack-loaders)

If you need loader support beyond what's built in, many webpack loaders already work with Turbopack. There are currently some limitations:

- Only a core subset of the webpack loader API is implemented. Currently, there is enough coverage for some popular loaders, and we'll expand our API support in the future.
- Only loaders that return JavaScript code are supported. Loaders that transform files like stylesheets or images are not currently supported.
- Options passed to webpack loaders must be plain JavaScript primitives, objects, and arrays. For example, it's not possible to pass `require()` plugin modules as option values.

To configure loaders, add the names of the loaders you've installed and any options in `next.config.js`, mapping file extensions to a list of loaders.

Here is an example below using the [`@svgr/webpack`](https://www.npmjs.com/package/@svgr/webpack) loader, which enables importing `.svg` files and rendering them as React components.

next.config.js

```
module.exports = {
  turbopack: {
    rules: {
      '*.svg': {
        loaders: ['@svgr/webpack'],
        as: '*.js',
      },
    },
  },
}
```

For loaders that require configuration options, you can use an object format instead of a string:

next.config.js

```
module.exports = {
  turbopack: {
    rules: {
      '*.svg': {
        loaders: [
          {
            loader: '@svgr/webpack',
            options: {
              icon: true,
            },
          },
        ],
        as: '*.js',
      },
    },
  },
}
```

> **Good to know**: Prior to Next.js version 13.4.4, `turbo.rules` was named `turbo.loaders` and only accepted file extensions like `.mdx` instead of `*.mdx`.

### [Resolving aliases](#resolving-aliases)

Turbopack can be configured to modify module resolution through aliases, similar to webpack's [`resolve.alias`](https://webpack.js.org/configuration/resolve/#resolvealias) configuration.

To configure resolve aliases, map imported patterns to their new destination in `next.config.js`:

next.config.js

```
module.exports = {
  turbopack: {
    resolveAlias: {
      underscore: 'lodash',
      mocha: { browser: 'mocha/browser-entry.js' },
    },
  },
}
```

This aliases imports of the `underscore` package to the `lodash` package. In other words, `import underscore from 'underscore'` will load the `lodash` module instead of `underscore`.

Turbopack also supports conditional aliasing through this field, similar to Node.js' [conditional exports](https://nodejs.org/docs/latest-v18.x/api/packages.html#conditional-exports). At the moment only the `browser` condition is supported. In the case above, imports of the `mocha` module will be aliased to `mocha/browser-entry.js` when Turbopack targets browser environments.

### [Resolving custom extensions](#resolving-custom-extensions)

Turbopack can be configured to resolve modules with custom extensions, similar to webpack's [`resolve.extensions`](https://webpack.js.org/configuration/resolve/#resolveextensions) configuration.

To configure resolve extensions, use the `resolveExtensions` field in `next.config.js`:

next.config.js

```
module.exports = {
  turbopack: {
    resolveExtensions: ['.mdx', '.tsx', '.ts', '.jsx', '.js', '.mjs', '.json'],
  },
}
```

This overwrites the original resolve extensions with the provided list. Make sure to include the default extensions.

For more information and guidance for how to migrate your app to Turbopack from webpack, see [Turbopack's documentation on webpack compatibility](https://turbo.build/pack/docs/migrating-from-webpack).

## [Version History](#version-history)

VersionChanges`15.3.0``experimental.turbo` is changed to `turbopack`.`13.0.0``experimental.turbo` introduced.

Was this helpful?

supported.

Send
