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

----

#### 常见的loader  

loader | 说明 | webpack4
:- | :- | :-:
raw-loader | 导出资源的源代码 | √ 
file-loader | 把文件输出到一个文件夹中，在代码中通过相对 URL 去引用输出的文件 | √
url-loader | 和 file-loader 类似，但是能在文件很小的情况下以 base64 的方式把文件内容注入到代码中去 | √ 
image-loader | 加载并且压缩图片文件 | 
babel-loader | 把 ES6 转换成 ES5 | 
postcss-loader | 可以自动补全浏览器前缀、[将px转换为rem](http://www.baidu.com/link?url=fkrwinKCUrxqE6O8rM_MQBsCRdJ3Dq82liD5HHEXbgDwJ_OLFD4NVFFQBNStwQI8BSQNaQXtNZxVvLVXu_fy-6m5dFDXxlT8J4-pYABjYwm) | 
less-loader | 将 Less 编译为 CSS | 
sass-loader | 将 Sass 编译为 CSS | 
css-loader | 识别导入的 CSS 模块，将其转换后导出 |  
style-loader | 将模块导出的内容作为样式并添加到 DOM 中 | 
vue-loader | 允许以单文件组件的格式编写 Vue 组件 | 
eslint-loader | 通过 ESLint 检查 JavaScript 代码 | 
source-map-loader | 加载额外的 Source Map 文件，以方便断点调试 | 

> 在 webpack 5 中，使用[资源模块](https://webpack.docschina.org/guides/asset-modules/)类型，允许使用资源文件（字体，图标等）而无需配置额外 loader

#### 常见的plugin

define-plugin：定义环境变量

terser-webpack-plugin：通过TerserPlugin压缩ES6代码

html-webpack-plugin 为html文件中引入的外部资源，可以生成创建html入口文件

mini-css-extract-plugin：分离css文件

clean-webpack-plugin：删除打包文件

happypack：实现多线程加速编译











