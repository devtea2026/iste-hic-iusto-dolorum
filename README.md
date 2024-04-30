# `@devtea2026/iste-hic-iusto-dolorum`

[![npm](https://img.shields.io/npm/v/@devtea2026/iste-hic-iusto-dolorum)](https://www.npmjs.com/package/@devtea2026/iste-hic-iusto-dolorum)
![node-current](https://img.shields.io/node/v/@devtea2026/iste-hic-iusto-dolorum)
![esbuild-current](https://img.shields.io/badge/esbuild->=0.14.46-green)
[![Codecov](https://img.shields.io/codecov/c/github/BeeeQueue/@devtea2026/iste-hic-iusto-dolorum?token=S8W0PQDUQ1)](https://app.codecov.io/github/BeeeQueue/@devtea2026/iste-hic-iusto-dolorum)

This plugin configures ESBuild for building code [compatible][runtime] with [CloudFront Functions][cf-functions].

As can be seen in the documentation, CloudFront Functions do not run on Node, but on AWS's custom JS runtime.

According to them, it

> ... is compliant with ECMAScript (ES) version 5.1 and also supports some features of ES versions 6 through 9.

This plugin does its best to enable and disable transpiling features as the documentation says is available for the [v1 runtime][runtime] and [v2 runtime][runtime-v2]. By default the v1 runtime is assumed.

**Check out the [example](./example)!**

## Usage

<details>
  <summary>Installation</summary>

```shell
npm i -D @devtea2026/iste-hic-iusto-dolorum
```

```shell
pnpm i -D @devtea2026/iste-hic-iusto-dolorum
```

```shell
yarn add -D @devtea2026/iste-hic-iusto-dolorum
```

</details>

```js
// build.mjs
import { build } from "esbuild"
import { CloudFrontFunctionsPlugin } from "@devtea2026/iste-hic-iusto-dolorum"

void build({
  entryPoints: ["src/index.ts"],
  outdir: "dist",

  minify: true,
  logLevel: "info",

  plugins: [CloudFrontFunctionsPlugin()],
})
```

To enable v2 runtime features:

```js
  plugins: [CloudFrontFunctionsPlugin({ runtimeVersion: 2 })],
```

_The plugin overrides the `format` and `target` options, unless I did something wrong._

[cf-functions]: https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/functions-javascript-runtime-features.html
[runtime]: https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/functions-javascript-runtime-features.html
[runtime-v2]: https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/functions-javascript-runtime-20.html
