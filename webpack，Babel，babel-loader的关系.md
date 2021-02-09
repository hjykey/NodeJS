# [webpack，Babel，babel-loader的关系](https://www.cnblogs.com/whosmeya/p/12535654.html)

本文将要介绍 webpack，Babel，babel-loader 的关系。理清楚他们各自做了什么事情。

通常我们新建一个项目，会先配置webpack，然后配置babel；babel是一个编译工具，实际上，babel也是可以单独使用的。

下面我们从Babel出发，简单配置一个react项目，来清晰认识一下webpack和babel的关系。

## Babel 和 Webpack 简介

Babel 是一个 JavaScript 编译器。（把浏览器不认识的语法，编译成浏览器认识的语法。）

webpack 是一个现代 JavaScript 应用程序的静态模块打包器。（项目打包）

下面会用到的：

| 名称                                    | 描述                                               |
| --------------------------------------- | -------------------------------------------------- |
| @babel/cli                              | Babel附带了一个内置的CLI，可用于从命令行编译文件。 |
| @babel/core                             | 使用本地配置文件                                   |
| @babel/preset-env                       | 编译最新版本JavaScript                             |
| @babel/preset-react                     | 编译react                                          |
| @babel/polyfill                         | 通过 Polyfill 方式在目标环境中添加缺失的特性       |
| @babel/plugin-proposal-class-properties | 编译 class                                         |

## 开始配置

新建项目

```shell
mkdir babel-in-webpack
```

进入项目

```shell
cd babel-in-webpack/
```

初始化 npm

```shell
npm init
```

不用管提示，一顿回车键。然后会生成一个文件 `package.json`

### 配置 Babel

安装 Babel 相关依赖。Babel7将所有包放在了@babel/ 下。

```shell
npm install --save-dev @babel/cli @babel/core @babel/preset-env @babel/polyfill
```

新建文件 `babel.config.json`

```json
{
  "presets": [
    "@babel/preset-env"
  ],
  "plugins": []
}
```

新建文件夹 `src`，`src` 内新建文件 `test.js`，随便写点啥es6语法。

![img](https://img2020.cnblogs.com/blog/1141466/202003/1141466-20200320211647973-443876499.png)

使用下面命令编译

```shell
./node_modules/.bin/babel src --out-dir lib
```

![img](https://img2020.cnblogs.com/blog/1141466/202003/1141466-20200320212204224-399315473.png)

编译完会新增目录`lib`, 里面放着编译好的文件

![img](https://img2020.cnblogs.com/blog/1141466/202003/1141466-20200320211752862-186141817.png)

### 配置 React

安装 `Babel` 编译 `React` 的依赖

```shell
npm install --save-dev @babel/preset-react @babel/plugin-proposal-class-properties
```

`babel.config.json` 添加 `React` 相关配置

```json
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ],
  "plugins": [
    "@babel/plugin-proposal-class-properties"
  ]
}
```

安装 `React` 相关依赖

```shell
npm install --save react react-dom
src` 下新增 `react` 文件 `main.js
import React from 'react';
import ReactDOM from 'react-dom';

class App extends React.Component {
  render() {
    return (
      <div>Hello World!</div>
    )
  }
}

ReactDOM.render(<App />, document.getElementById('root'));
```

运行命令编译

```shell
./node_modules/.bin/babel src --out-dir lib
```

编译完成后 `lib` 下多了一个 `main.js`

![img](https://img2020.cnblogs.com/blog/1141466/202003/1141466-20200320213132647-847838181.png)

看起来编译很成功, 我们在 `lib` 下面新建一个 html 引入 `main.js` 看看效果

![img](https://img2020.cnblogs.com/blog/1141466/202003/1141466-20200320174059014-369351006.png)

报错，浏览器不认识require，继续往下看。

### 配置 webpack

安装 `webpack` 依赖

```shell
npm install --save-dev webpack webpack-cli
```

根目录新建文件 `webpack.config.js`

```js
const path = require('path');

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].js'
  }
};
```

在 `package.json` 的 `scripts` 中加入命令

```txt
"build": "webpack --mode development",
```

运行命令

```shell
npm run build
```

![img](https://img2020.cnblogs.com/blog/1141466/202003/1141466-20200320215050350-389680613.png)

`webpack` 不认识 `react` 语法，在 `webpack.config.js` 中加入 `babel-loader`。

```js
const path = require('path');

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].js'
  },
  module: {
    rules: [
      { test: /\.js$/, use: 'babel-loader' }
    ]
  },
  plugins: []
};
```

安装依赖 `babel-loader`

```shell
npm install --save-dev babel-loader
```

运行命令

```shell
npm run build
```

![img](https://img2020.cnblogs.com/blog/1141466/202003/1141466-20200320221633584-77810522.png)

会看到 `dist/main.js`, 写个html引入试试

![img](https://img2020.cnblogs.com/blog/1141466/202003/1141466-20200320222151486-254242323.png)

### 两种编译结果对比

我们来看 Babel 编译结果 `lib/main.js` 和 webpack 编译结果 `dist/main.js`，发现 Babel 仅仅是将 `src/main.js` 的react语法编译成了js语法，而 webpack 将 `src/main.js` 和引入的 `node_modules` 融合后用 Babel 编译。

浏览器不认识 `require`，`webpack` 实现了一套浏览器认识的 `require`。

## 总结

Babel 是编译工具，把高版本语法编译成低版本语法，或者将文件按照自定义规则转换成js语法。

webpack 是打包工具，定义入口文件，将所有模块引入整理后，通过 loader 和 plugin 处理后，打包输出。

webpack 通过 babel-loader 使用 Babel 。

[代码地址：GitHub](https://github.com/whosMeya/babel-in-webpack)