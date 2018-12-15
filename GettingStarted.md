---
id: getting-started
title: 开始使用
---

通过[`yarn`](https://yarnpkg.com/en/package/jest)安装jest:

```bash
yarn add --dev jest
```

或者通过 [`npm`](https://www.npmjs.com/) 安装:

```bash
npm install --save-dev jest
```

注意: Jest 文档中默认使用使用 `yarn` 命令, 你也可以使用 `npm` 命令. 你可以在 [yarn 文档](https://yarnpkg.com/en/docs/migrating-from-npm#toc-cli-commands-comparison)上比较 `yarn` and `npm` 命令的不同.

Let's get started by writing a test for a hypothetical function that adds two numbers. First, create a `sum.js` file:

```javascript
function sum(a, b) {
  return a + b;
}
module.exports = sum;
```

Then, create a file named `sum.test.js`. This will contain our actual test:

```javascript
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

Add the following section to your `package.json`:

```json
{
  "scripts": {
    "test": "jest"
  }
}
```

最后，运行命令 `yarn test` 或者 `npm run test` ，Jest将会打印以下信息:

```bash
PASS  ./sum.test.js
✓ adds 1 + 2 to equal 3 (5ms)
```

**你刚刚已经成功地编写了你的第一个Jest测试用例！**

This test used `expect` and `toBe` to test that two values were exactly identical. To learn about the other things that Jest can test, see [Using Matchers](UsingMatchers.md).

## 使用命令行运行

You can run Jest directly from the CLI (if it's globally available in your `PATH`, e.g. by `yarn global add jest` or `npm install jest --global`) with a variety of useful options.

Here's how to run Jest on files matching `my-test`, using `config.json` as a configuration file and display a native OS notification after the run:

```bash
jest my-test --notify --config=config.json
```

想了解更多关于通过命令行运行 `jest`, 请查看 [Jest CLI Options](CLI.md).

## 附加配置

### 生成基本配置文件

Based on your project, Jest will ask you a few questions and will create a basic configuration file with a short description for each option:

```bash
jest --init
```

### 使用Babel

结合[Babel](http://babeljs.io/)使用, 请使用 `yarn` 安装 `babel-jest` 以及 `regenerator-runtime` 模块:

```bash
yarn add --dev babel-jest babel-core regenerator-runtime
```

或者通过 `npm` 安装:

```bash
npm install --save-dev babel-jest babel-core regenerator-runtime
```

> 注意: 如果你使用Babel 7，你需要使用以下命令安装 `babel-jest`， `babel-core@^7.0.0-bridge.0` 以及 `@babel/core`，当然，使用npm命令也是可以的:
>
> ```bash
> yarn add --dev babel-jest babel-core@^7.0.0-bridge.0 @babel/core regenerator-runtime
> ```
>
> 为了转换 `node_modules` ， 你需要使用babel配置 `babel.config.js`. 详情请查看https://babeljs.io/docs/en/next/config-files.
>
> 你可以参考Jest仓库中的示例: https://github.com/facebook/jest/tree/master/examples/babel-7

_Note: Explicitly installing `regenerator-runtime` is not needed if you use `npm` 3 or 4 or Yarn_

Don't forget to add a [`.babelrc`](https://babeljs.io/docs/usage/babelrc/) file in your project's root folder. For example, if you are using ES6 and [React.js](https://facebook.github.io/react/) with the [`babel-preset-env`](https://babeljs.io/docs/plugins/preset-env/) and [`babel-preset-react`](https://babeljs.io/docs/plugins/preset-react/) presets:

```json
{
  "presets": ["env", "react"]
}
```

You are now set up to use all ES6 features and React specific syntax.

> Note: If you are using a more complicated Babel configuration, using Babel's `env` option, keep in mind that Jest will automatically define `NODE_ENV` as `test` **if not already set** to something else. It will not use `development` section like Babel does by default when no `NODE_ENV` is set.

> Note: If you've turned off transpilation of ES6 modules with the option `{ "modules": false }`, you have to make sure to turn this on in your test environment.

```json
{
  "presets": [["env", {"modules": false}], "react"],
  "env": {
    "test": {
      "presets": [["env"], "react"]
    }
  }
}
```

> 注意: `babel-jest` is automatically installed when installing Jest and will automatically transform files if a babel configuration exists in your project. To avoid this behavior, you can explicitly reset the `transform` configuration option:

```json
// package.json
{
  "jest": {
    "transform": {}
  }
}
```

### 使用webpack

Jest can be used in projects that use [webpack](https://webpack.github.io/) to manage assets, styles, and compilation. webpack does offer some unique challenges over other tools. Refer to the [webpack guide](Webpack.md) to get started.

### 使用TypeScript

要在测试中使用TypeScript,你可以使用[ts-jest](https://github.com/kulshekhar/ts-jest).
