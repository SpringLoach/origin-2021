#### 什么是webpack  

webpack是一个打包模块化的工具，在webpack里一切文件皆模块，通过loader转换文件，通过plugin注入钩子，最后输出由多个模块组合成的文件。  

WebPack可以看做是模块打包机：分析项目的结构，找到JavaScript模块以及其它的一些浏览器不能直接运行的拓展语言（Scss，TypeScript等），
并将其打包为合适的格式以供浏览器使用。

#### 概念  

#### 概念_入口  
> 指示 webpack 应该使用哪个模块，来作为构建其内部**依赖图**的开始。进入入口起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的。  

关键词 | 说明
:- | :-
entry | 指定入口起点
output | 定义出口
path | node 核心模块  
\_\_dirname | 被执行js文件的绝对路径

#### 概念_输出  
> 告诉 webpack 在哪里输出它所创建的 bundle，以及如何命名这些文件。  

```
/* webpack.config.js */
const path = require('path')

module.exports = {
    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js'
    }
}
```

#### 概念_loader  
> webpack 自身只能理解 JavaScript 和 JSON 文件。loader 让 webpack 能够去处理其他类型的文件，并将它们**转换**为有效**模块**，以供应用程序使用，以及被添加到依赖图中。  

属性 | 说明
:- | :-
test | 识别出哪些文件会被转换
use | 定义出在进行转换时，应该使用哪个 loader

```
module.exports = {
  entry: './src/main.js',
  module: {
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  },
};
```
> 对 module 对象定义了 rules 属性，里面包含两个必须属性：test 和 use
> 
> 当碰到「在 require()/import 语句中被解析为 `'.txt'` 的路径」时，在打包之前，先使用 `raw-loader` 转换一下。
> 
> 使用正则表达式匹配文件时，不要添加引号，表示匹配任何以 `.txt` 结尾的文件。  

#### 概念_插件  
> 可以扩展 webpack 能力，如打包优化，资源管理，注入环境变量。  

步骤 | 说明
:- | :-
① | 通过 npm 安装
② | 通过 require 导出
③ | 添加到 plugins 数组  
④ | 多数插件可以通过 option 自定义  
⑤ | 复用插件时，new 插件实例  

```
const HtmlWebpackPlugin = require('html-webpack-plugin'); 
const webpack = require('webpack'); // 用于访问内置插件

module.exports = {
  module: {
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  },
  plugins: [new HtmlWebpackPlugin({ template: './src/index.html' })],
};
```

#### 概念_模式  
> 设置 process.env.NODE_ENV 的值，可选 development, production 或 none。  

```
module.exports = {
  mode: 'production',
};
```

#### 概念_浏览器兼容性  

属性 | 说明
:- | :-
支持所有符合 ES5 标准 的浏览器 | 不支持 IE8 及以下版本
`import()` 和 `require.ensure()` 需要 `Promise` | 想支持旧浏览器，使用前，还需要提前加载 [polyfill](https://webpack.docschina.org/guides/shimming/)





