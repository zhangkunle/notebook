#                     构建工具webpack

**什么是webpack**
Webpack是一个模块打包器(bundler)。
在Webpack看来，前端的所有资源文件(js/json/css/img/less/...)都会作为模块处理。它将根据模块的依赖关系进行静态分析，生成对应的静态资源

**五个核心概念**

- Entry:入口起点(entry point)指示webpack应该使用哪个模块，来作为构建其内部依赖图的开始。
- Output: output属性告诉webpack在哪里输出它所创建的bundles，以及如何命名这些文件，默认值为./dist。
- Loader: loader让webpack能够去处理那些非JavaScript文件(webpack自身只能解析JavaScript)。
- Plugins:插件则可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量等。

- Mode:模式，有生产模式production和开发模式development

**理解Loader**

Webpack 本身只能加载JS/JSON模块，如果要加载其他类型的文件(模块)，就需要使用对应的loader进行转换/加载。

Loader本身也是运行在node.js环境中的JavaScript 模块。它本身是一个函数，接受源文件作为参数，返回转换的结果。

loader 一般以xxx-loader的方式命名，xxx代表了这个loader要做的转换功能，比如json-loader。

**理解Plugins**

插件可以完成一些loader不能完成的功能。

插件的使用一般是在webpack的配置信息plugins选项中指定。

**配置文件(默认)**

weppack.conng.js : 是一个node模块，返回一个json 格式的配置信息对象

## 一、简介

- 当我们习惯了在node中编写代码的方式后，在回到前端编写html、css、js这些东西会感觉到各种的不便。比如：不能放心的使用<u>模块化</u>规范（浏览器兼容性问题）、即使可以使用模块化规范也会面临模块过多时的加载问题。
- 我们就迫切的希望有一款工具可以对代码进行打包，将多个模块打包成一个文件。这样一来即解决了兼容性问题，又解决了模块过多的问题。
- 构建工具就起到这样一个作用，通过构建工具可以将使用ESM规范编写的代码转换为旧的JS语法，这样可以使得所有的浏览器都可以支持代码。

## 二、Webpack介绍

### 1、概念

本质上，**webpack** 是一个用于现代 JavaScript 应用程序的 *静态模块打包工具*。当 webpack 处理应用程序时，它会在内部从一个或多个入口点构建一个[依赖图(dependency graph)](https://www.webpackjs.com/concepts/dependency-graph/)，然后将你项目中所需的每一个模块组合成一个或多个 *bundles*，它们均为静态资源，用于展示你的内容。【按需打包】

webpack能够编译打包js和json文件，能将es6模块化语法转换成浏览器识别的语法，能压缩代码。在不借助插件或者loader的情况下，不能编译打包css/img等文件，不能将js的es6语法转化为es5以下的语法。

> webpack在node中运行

### 2、使用步骤

安装的包是否加-D (开发环境) 

- 是为了实现功能效果吗？  是的  不加-D
- 是为了我处理代码吗？   是的 加-D

1. 初始化项目`yarn init -y`

2. 安装依赖`webpack`、`webpack-cli`

3. 在项目中创建`src`目录，然后编写代码（默认主文件index.js）

4. 执行`yarn webpack`来对代码进行打包（打包后观察dist目录）

   ```javascript
   webpack src/js/index/js -o peiqi/nice.js
   ```

> `cli`: command line interface 命令行工具
>
> 安装依赖`yarn add -D webpack webpack-cli`, -d表示设置为开发依赖
>
> src 目录下的是遵循前端开发规范的，src 以外的要用node规范CommonJS

### 3、配置文件（webpack.config.js）

```javascript
const path = require("path")
module.exports = {
    mode: "production", 
    entry: "./src/index.js",
    output: {
    }, 
    module: {
        rules: [
            {
                test: /\.css$/i,
                use: ["style-loader", "css-loader"]
            }
        ]
    }
}
```

> 书写对象的时候，可以在最后一个属性值后面加上`,`并且属性名可以不为字符串
>
> 但在写JSON的时候，属性名也需要加上`“”`并且最后不能加上`,`

#### [mode](https://www.webpackjs.com/configuration/mode/)

告知 webpack 使用相应模式的内置优化

- none：不使用任何默认优化选项
- production：生产模式
- development：开发模式

#### [entry](https://www.webpackjs.com/concepts/entry-points/)

默认值是 `./src/index.js`（一般不改，约定优于配置）

- 单个入口语法【最常见】 `entry: string | [string]`
- 多个传数组 `entry: ['./src/file_1.js', './src/file_2.js']`
- 对象写法分别命名打包 `entry: {app: './src/app.js',adminApp: './src/adminApp.js',},`

#### [output](https://www.webpackjs.com/concepts/output/)

默认值是 `./dist/main.js`，其他生成文件默认放置在 `./dist` 文件夹中

- `filename: "bundle.js"` 设置打包后的文件名

  > 多个入口 entry 的情况 `filename: [name]-[id]-[hash].js`
  >
  > 使用 [占位符(substitutions)](https://www.webpackjs.com/configuration/output/#template-strings) 来确保每个文件具有唯一的名称（很少用）

- `clean: true` 自动清理<u>打包目录</u>（path指定的目录），只保留当前这次打包的文件

- `path:  ""` 指定打包目录，必须要绝对路径

  > 一般会使用Node.js中的path模块来操作文件路径
  >
  > ```js
  > const path = require('path');	//引入path模块
  > path.resolve(__dirname, "dist")	//表示当前目录下的dist文件夹
  > ```

#### [loader](https://www.webpackjs.com/concepts/loaders/)

**loader** 让 webpack 能够去处理<u>其他类型</u>的文件（默认只能处理js文件），并将它们转换为有效 [模块](https://www.webpackjs.com/concepts/modules)，以供应用程序使用，以及被添加到依赖图中。

使用步骤：

1. 安装对应的 loader：`yarn add css-loader style-loader ts-loader -D`

2. 配置方式（推荐）：

   - test 属性：识别出哪些文件需要被转换（使用正则表达式`/\.css$/i`）
   - use 属性：定义出在进行转换时，使用哪个 loader（字符串、数组、对象）
   - type 属性：[加载图像资源](https://www.webpackjs.com/guides/asset-management/#loading-images)，设置为`"asset/resource"`
   - exclude 属性：不需要转换的文件夹（正则表达式）

   ```js
   //用到的所有loader都需要配置在module对象中的rules数组中，每一个loader都是一个对象
   module.exports = {
     module: {	// 易漏点
       rules: [ 
         { test: /\.css$/, use: ['style-loader','css-loader'] },
         { test: /\.ts$/, use: 'ts-loader' },
         { test:/\.(jpg|png|gif)$/i,type:"asset/resource" },
       ],
     },
   };
   ```

   > css-loader 只负责打包，style-loader 负责渲染生效【单一职责原则】  
   >
   > loader 执行顺序为**从后向前**执行，因此 use 的数组顺序不能调换

3. *内联方式：在每个 `import` 语句中显式指定 loader。

   使用 `!` 将资源中的 loader 分开。每个部分都会相对于当前目录解析。

   ```js
   import Styles from 'style-loader!css-loader?modules!./styles.css';
   ```

   - 使用`!`前缀，将禁用所有已配置的 normal loader(普通 loader)
   - 使用`!!`前缀，将禁用所有已配置的 loader（preLoader, loader, postLoader）
   - 使用`-!`前缀，将禁用所有已配置的 preLoader 和 loader，但是不禁用 postLoaders

   选项可以传递查询参数，例如 `?key=value&foo=bar`，或者一个 JSON 对象，例如 `?{"key":"value","foo":"bar"}`。

   > 尽可能使用 `module.rules`，因为这样可以减少源码中样板文件的代码量，并且可以在出错时，更快地调试和定位 loader 中的问题。

4、如果是使用less，则需要less-loader/css-loader/style-loader

> less-loader: 将less文件解析成css（将css放在内存中）
>
> css-loader:将css以commonjs方式整合到js文件中
>
> style-loader:创建style标签，添加上js中的css代码

5、js语法检查

概述：对js基本语法错误/隐患，进行提前检查

安装loader

```powershell
npm install eslint-loader eslint --save-dev
```

配置loader

```js
 rules: [ 
{
   test: /\.js$/, //只检测js文件
   exclude: /node_modules/,//排除node_modules文件夹
   enforce: "pre",//提前加载使用
   loader:"eslint-loader"
}]
```

修改package.json,加上一些配置才能生效（去除注释）

```js
"eslintConfig": 
   {
    "parserOptions":  {
      "ecmaVersion": 6, //支持es6 
      "sourceType": "module" // 使用es6模块化 
    },
   "env": {// 设置环境
     "browser": true, //支持浏览器环境:能够使用window上的全局变量 
     "node": true //支持服务器环境:能够使用node/global的全局变量 
   },
   "globals":{//声明使用的全量，这样即使没有定义也不会报错了
     "$": "readonly" //8只读变量 I 
   },
   "rules": { //eslint检查的规则o忽略1警告2错误
     "no-console": 0， //不检査console 
     "eqeqeq": 2， //用==而不用===就报错 
     "no-alert": 2//不能使用alert
   },
  "extends": "eslint:recommended"//_使用eslint推荐的默认规则https://cn.eslintorg/docs/r
}
```

使用eslint时，已经明确声明用es6(ecmaVersion: 6), 但是检查时promise还是会报错，于是在globals配置中声明promise是readonly就能检查通过了。

##### [babel（js语法转换）](https://www.webpackjs.com/loaders/babel-loader)

###### 概念

- 在编写js代码时，经常需要使用一些js中的新特性，而新特性在旧的浏览器中兼容性并不好。此时就导致我们无法使用一些新的特性。

- 但是我们现在希望能够使用新的特性，我们可以采用折中的方案。依然使用新特性编写代码，但是代码编写完成时我们可以通过一些工具将新代码转换为旧代码。

- babel就是这样一个工具，可以将新的js语法转换为旧的js，以提高代码的兼容性。

- 如果希望在webpack支持babel，则需要向webpack中引入babel的loader

  > 是 loader 中的一种

###### 使用步骤

1. 安装 `npm install -D babel-loader @babel/core @babel/preset-env`

   - babel-loader：连接webpack和babel的中间件
   - @babel/core：babel的转换核心
   - @babel/preset-env：预设环境

2. 配置：

   ```javascript
   module: {
     rules: [
       {
         test: /\.m?js$/,
         exclude: /(node_modules|bower_components)/,
         use: {
           loader: 'babel-loader',
           options: {
             presets: ['@babel/preset-env']
           }
         }
       }
     ]
   }
   ```

3. 在package.json中设置兼容列表 // 设置需要兼容哪些浏览器

   ```json
   "browserslist": [
      "defaults"
    ]
   ```

   配置参考：https://github.com/browserslist/browserslist

#### [plugin](https://www.webpackjs.com/concepts/plugins/)

##### 概念

- 插件用来为webpack来扩展功能
- 插件目的在于解决 [loader](https://www.webpackjs.com/concepts/loaders) 无法实现的其他事。
- Webpack 提供很多开箱即用的 [插件](https://www.webpackjs.com/plugins/)。

##### 常用插件

html-webpack-plugin

- 这个插件可以在打包代码后，自动在打包目录生成html页面

使用步骤：

1. 安装依赖`yarn add -D html-webpack-plugin`
2. 引入依赖`const HTMLPlugin = require("html-webpack-plugin")`
3. 配置插件

```javascript
plugins: [
        new HTMLPlugin({
            // title: "Hello Webpack",	//设置title
            template: "./src/index.html"	//模板，自动引入script脚本
        })
    ]
```

##### **区分：**

**loader:会把代码从一个状态变为另一个状态**

**plugins:对某些功能的扩展，使开发更便利，不会改变代码结构状态**

#### devtool

`devtool:"inline-source-map"`配置源码的映射，方便调试打包后的代码。、

### 4、开发服务器（webpack-dev-server）

- 安装：`yarn add -D webpack-dev-server`
- 启动：`yarn webpack serve --open`（`--open`表示启动服务器后自动打开）

> 配置 `webpack –watch` 执行，（在本地文件夹中访问）代码发生变化时自动更新打包。
>
> ![image-20230222152155721](构建工具.assets/image-20230222152155721-1677050518425-1.png)

### 5、grunt/glup的对比

### 6、js兼容性对比(在不同浏览器)

**第一种方法**：**使用经典的ployfill（处理旧浏览器不认识高级es6语法）**

安装：

```js
npm install @babel/polyfill
```

使用：

```js
-app.js
  import @babel/polyfill //包含ES6的高级语法转换（promise等）
```

优点：解决babel只能转换部分低级语法的问题(如:let/const/解构赋值..)，引入polyfill可以转换高级语法(如:Promise...)

缺点：将所有高级语法都进行了转换，但实际上可能只使用一部分
解决：需要按需加载(使用了什么高级语法，就转换什么，而其他的不转换)

**第二种方法：借助按需引入core.js按需引入**

安装：

```js
npm install core-js
```

使用：

```js
 {
                test: /\.m?js$/,  //是否以mjs或者js结尾
                exclude: /(node_modules|bower_components)/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: [
                            [
                                '@babel/preset-env',
                                {
                                    useBuiltIns: 'usage',
                                    corejs: { version: 3 },//解决warn
                                    //targets: { //指定兼容哪些浏览器的哪些版本
                                    //    chrome: "119",
                                    //    ie: "11"
                                   // }
                                }
                            ] //babel默认配置
                        ],
                        cacheDirectory: true //开启babel缓存
                    }
                }
}
```



## [Vite](https://cn.vitejs.dev/)

### 1、概念

- Vite也是前端的构建工具

- 相较于webpack，Vite采用了不同的运行方式：

  - 开发时，并不对代码打包，而是直接采用**ESM（ES模块）**的方式来运行项目
  - 在项目部署时，再对项目进行打包

- 除了[速度外](https://cn.vitejs.dev/guide/why.html#slow-server-start)，Vite使用起来也更加方便（开箱即用，都配置好了）

- 本质上 Vite 和 Webpack 是打包工具，只是 Webpack 比较底层，需要自己手动去配置。

  > ESM 必须通过 url 加载页面（即需要通过服务器运行）

### 2、基本使用

1. 安装开发依赖 Vite `yarn add -D vite`

2. Vite 的源码目录默认就是项目**[根目录](https://cn.vitejs.dev/guide/#index-html-and-project-root)**

   - 在页面中引入 js 文件的时候要指定 `type=“module”`
   - 修改路径直接在 script 标签中修改 src 属性正确即可（webpack需要配置）

3. 开发命令：

   - `vite` 启动**开发**服务器

   - `vite build` 打包代码

   - `vite preview` **预览**打包后代码

4. [使用命令构建项目](https://cn.vitejs.dev/guide/#scaffolding-your-first-vite-project)：

  ```bash
  npm create vite@latest	#使用 NPM
  yarn create vite	#使用 Yarn
  pnpm create vite	#使用 PNPM
  #Vanilla 表示原生JS开发项目
  ```

5. [使用插件](https://cn.vitejs.dev/guide/using-plugins.html)

   1. 安装插件：`npm add -D @vitejs/plugin-legacy`

      > `@vitejs/plugin-legacy`：兼容传统浏览器的语法转换插件

   2. 配置文件：`vite.config.js`

      ```javascript
      // vite.config.js
      import legacy from '@vitejs/plugin-legacy'	//引入插件
      import { defineConfig } from 'vite'	//语法提示（可选）
      export default defineConfig({	//写上defineConfig配置时会有提示
        plugins: [	//配置插件
          legacy({
            targets: ['defaults', 'IE 11'],	//配置兼容版本
          }),
        ],
      })
      
      ```

      > 需要使用ES6的模块化（`export default`）去暴露文件（区别于 webpack 使用`require`）
