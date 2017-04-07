---
title: Node
sort: 14
contributors:
  - sokra
  - skipjack
---

These options configure whether to polyfill or mock certain node globals and modules. This allows code originally written for the node environment to run in other environments like the browser.

See also: the [Node globals documentation](https://nodejs.org/docs/latest/api/globals.html).

## `node`

`object`

This is an object where
- each key is a node global or module name
- each value is one of the following
  - `true`: Provide a polyfill.
  - `"mock"`: Provide a mock that implements the expected interface but has little or no fuctionality.
  - `"empty"`: Provide an empty object.
  - `false`: Provide nothing. Code that expects this object to be defined may crash.

Note: not all keys support all values. See the sections below.

T> You can see the available polyfills and mocks in [webpack/node-libs-browser](https://github.com/webpack/node-libs-browser).

The defaults:

```js
node: {
  console: false,
  global: true,
  process: true,
  __filename: "mock",
  __dirname: "mock",
  Buffer: true,
  setImmediate: true
}
```

## `node.console`

`boolean | "mock"`

Default: `false`

The browser provides a `console` object with a very similar interface to the node `console`, so a polyfill is generally not needed.


## `node.process`

`boolean | "mock"`

Default: `true`


## `node.global`

`boolean`

Default: `true`

See [the source](https://github.com/webpack/webpack/blob/master/buildin/global.js) for the exact behavior of this object.


## `node.__filename`

`boolean | "mock"`

Default: `true`

Options:

- `true`: The filename of the **input** file relative to the [`context` option](https://webpack.js.org/configuration/entry-context/#context).
- `false`: The regular node `__filename` behavior. The filename of the **output** file when run in a node environment.
- `"mock"`: The fixed value `"index.js"`.


## `node.__dirname`

`boolean | "mock"`

Default: `true`

Options:

- `true`: The dirname of the **input** file relative to the [`context` option](https://webpack.js.org/configuration/entry-context/#context).
- `false`: The regular node `__dirname` behavior. The dirname of the **output** file when run in a node environment.
- `"mock"`: The fixed value `"/"`.


## `node.Buffer`

`boolean | "mock"`

Default: `true`


## `node.setImmediate`

`boolean | "mock" | "empty"`

Default: `true`


## Other node core libraries

`boolean | "mock" | "empty"`

Many other node core libraries can be configured as well. See the list of [node core libraries and their polyfills](https://github.com/webpack/node-libs-browser).

By default, Webpack will polyfill node core libraries if there is a known polyfill or do nothing if there is not one.

```js
node: {
  dns: "mock",
  fs: "empty",
  path: true,
  url: false
}
