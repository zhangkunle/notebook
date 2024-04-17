

#                              Node.JS

### 回顾与思考

![image-20230820155055254](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820155055254.png)

![image-20230820155226715](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820155226715.png)

![image-20230820155720031](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820155720031.png![image-20230820155754796](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820155754796.png)

![image-20230820155946174](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820155946174.png)

## 1.Node.JS简介

##### 定义

Node.js 是一个基于 Chrome V8 引擎 的 JavaScript 运行时环境。

![image-20230826152022683](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230826152022683.png)

![image-20230820160622578](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820160622578.png)

- 基于 [Express 框架 (opens new window)](http://www.expressjs.com.cn/)，可以快速构建 Web 应用
- 基于 [Electron 框架 (opens new window)](https://electronjs.org/)，可以构建跨平台的桌面应用
- 基于 [restify 框架 (opens new window)](http://restify.com/)，可以快速构建 API 接口项目
- 读写和操作数据库、创建实用的命令行工具辅助前端开发、etc…

node.js有超强的并发性，实现高性能服务器；并发周期短，开发成本低，node.js完全是js语法。

##### 终端

专门为开发人员设计的，用于实现人机交互的一种方式。

![image-20230820204226557](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820204226557.png)

## 2.在Node.js环境中执行JS代码

（1）打开终端（shift+右键 powershell）

（2）输入node要执行的js文件的路径

![image-20230820203602319](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820203602319.png)

## 3.模块-包

![image-20230821103608479](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230821103608479.png)

​                                                                          为什么要引入模块化开发

###  CommonJS规范

![image-20230821104015258](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230821104015258.png)

### 3.1 什么是模块化

**概念**：将一个复杂的程序依据一定的规则（规范）封装成几个块（文件），并组合在一起。

模块的内部数据、实现是私有的, 只是向外部暴露一些接口(方法)与外部其它模块通信。

最早的时候，我们会把所有的代码都写在一个js文件里，那么，耦合性会很高（关联性强），不利于维护；而且会造成全局污染，很容易命名冲突。

### 3.2 模块化的好处

- 避免命名冲突，减少命名空间污染
- 降低耦合性；更好地分离、按需加载
- **高复用性**：代码方便重用，别人开发的模块直接拿过来就可以使用，不需要重复开发类似的功能。
- **高可维护性**：软件的声明周期中最长的阶段其实并不是开发阶段，而是维护阶段，需求变更比较频繁。使用模块化的开发，方式更容易维护。
- 部署方便

### 3.3 模块化规范的引入

假设我们引入模块化，首先可能会想到的思路是：在一个文件中引入多个js文件。如下：

```js
<body>
    <script src="zepto.js"></script>
    <script src="fastClick.js"></script>
    <script src="util/login.js"></script>
</body>
```

但是这样做会带来很多问题：

- 请求过多：引入十个js文件，就有十次http请求。
- 依赖模糊：不同的js文件可能会相互依赖，如果改其中的一个文件，另外一个文件可能会报错。

以上两点，最终导致：**难以维护**。

### 3.4 模块化的概念解读

模块化起源于 Node.js。Node.js 中把很多 js 打包成 package，需要的时候直接通过 require 的方式进行调用（CommonJS），这就是模块化的方式.**产生了两种伟大的 js：RequireJS 和 SeaJS。**

### 3.5 模块化规范

服务器端规范：

- [**CommonJS规范**](http://www.commonjs.org/)：是 Node.js 使用的模块化规范。

CommonJS 就是一套约定标准，不是技术。用于约定我们的代码应该是怎样的一种结构。

浏览器端规范：

- [**AMD规范**](https://github.com/amdjs/amdjs-api)：是 **[RequireJS](http://requirejs.org/)** 在推广过程中对模块化定义的规范化产出。

```
- 异步加载模块；
- 依赖前置、提前执行：require([`foo`,`bar`],function(foo,bar){});   
//也就是说把所有的包都 require 成功，再继续执行代码。
- define 定义模块：define([`require`,`foo`],function(){return});
```

- **[CMD规范](https://web.qianguyihao.com/11-Node.js/04-Node.js模块化规范：CommonJS.html)**：是 **[SeaJS](http://seajs.org/)** 在推广过程中对模块化定义的规范化产出。淘宝团队开发。

```
  同步加载模块；
  依赖就近，延迟执行：require(./a) 直接引入。或者Require.async 异步引入。   
  //依赖就近：执行到这一部分的时候，再去加载对应的文件。
  define 定义模块， export 导出：define(function(require, export, module){});
```

PS：面试时，经常会问AMD 和 CMD 的区别。

另外，还有ES6规范：import & export。

### 3.6CommonJS 的介绍

[CommonJS](http://www.commonjs.org/)：是 Node.js 使用的模块化规范。也就是说，Node.js 就是基于 CommonJS 这种模块化规范来编写。

CommonJS 规范规定：每个模块内部，module 变量代表当前模块。这个变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口对象。加载某个模块，其实是加载该模块的 module.exports 对象。

在 CommonJS 中，每个文件都可以当作一个模块：

- 在服务器端：模块的加载是运行时同步加载的。
- 在浏览器端: 模块需要提前编译打包处理。首先，既然同步的，很容易引起阻塞；其次，浏览器不认识`require`语法，因此，需要提前编译打包。

### 3.7 模块的暴露和引入

Node.js 中只有模块级作用域，两个模块之间的变量、方法，默认是互不冲突，互不影响，这样就导致一个问题：模块 A 要怎样使用模块B中的变量&方法呢？这就需要通过 `exports` 关键字来实现。

Node.js中，每个模块都有一个 exports 接口对象，我们可以把公共的变量、方法挂载到这个接口对象中，其他的模块才可以使用。

### 3.8.1 暴露模块的方式一： exports

`exports`对象用来导出当前模块的公共方法或属性。别的模块通过 require 函数调用当前模块时，得到的就是当前模块的 exports 对象。

**语法格式**：

```
//给 exports 对象添加属性
exports.xxx = value
```

这个 value 可以是任意的数据类型。

**注意**：暴露的关键词是`exports`，不是`export`。其实，这里的 exports 类似于 ES6 中的 export 的用法，都是用来导出一个指定名字的对象。

**代码举例**：

```js
const name = 'qianguyihao';
const foo = function (value) {
	return value * 2;
};
exports.name = name;
exports.foo = foo;  //在js文件中暴露name属性和foo方法
```

### 3.8.2 暴露模块的方式二： module.exports

`module.exports`用来导出一个默认对象，没有指定对象名。

语法格式：

```js
// 方式一：导出整个 exports 对象
module.exports = value;
// 方式二：给 exports 对象添加属性
module.exports.xxx = value; //这个 value 可以是任意的数据类型。
```

代码举例：

```js
// 方式1
module.exports = {
    name: '我是 module1',
    foo(){
        console.log(this.name);
    }
}
// 我们不能再继续写 module.exports = value2。因为重新赋值，会把 exports对象之前的赋值覆盖掉。
//方式2
function test() {
    console.log('test');
}
function upper(str) {
    console.log(str.substring(0, 1).toUpperCase() + str.substring(1));
}
module.exports = {
    test,
    upper
}
//等价于
module.exports.test = test;
module.exports.upper = upper;
//等价于
exports.test = test;
exports.upper = upper;
//引入模块时：
moduleA.upper('klji');
moduleA.test();
```

`module.exports` 还可以修改模块的原始导出对象。比如当前模块原本导出的是一个对象，我们可以通过 module.exports 修改为导出一个函数。如下：

```js
module.exports = function () {
    console.log('hello world')
}
```

### 3.9 问题: 暴露的模块到底是谁？

**答案**：暴露的本质是`exports`对象。【重要】

比如，方式一的 `exports.a = a` 可以理解成是，**给 exports 对象添加属性**。方式二的 `module.exports = a`可以理解成是给整个 exports 对象赋值。方式二的 `module.exports.c = c`可以理解成是给 exports 对象添加属性。

Node.js 中每个模块都有一个 module 对象，module 对象中的有一个 exports 属性称之为**接口对象**。我们需要把模块之间公共的方法或属性挂载在这个接口对象中，方便其他的模块使用。

### 3.10引入模块的方式：require

require函数用来在一个模块中引入另外一个模块。传入模块名，返回模块导出对象。

**语法格式**：

```js
const module1 = require('模块名');
```

解释：

- 内置模块：require的是**包名**。
- 下载的第三方模块：require的是**包名**。
- 自定义模块：require的是**文件路径**。文件路径既可以用绝对路径，也可以用相对路径。后缀名`.js`可以省略。

**代码举例**：

```js
const module1 = require('./main.js');
const module2 = require('./main');
const module3 = require('Demo/src/main.js');
```

**require()函数的两个作用**：

- 执行导入的模块中的代码。
- 返回导入模块中的接口对象。

### 3.11主模块

主模块是整个程序执行的入口，可以调度其他模块。

```js
# 运行main.js启动程序。此时，main.js就是主模块
$ node main.js
```

### 3.12 模块的初始化

一个模块中的 JS 代码仅在模块**第一次被使用时**执行一次，并且在使用的过程中进行初始化，然后会**被缓存起来**，便于后续继续使用。

代码举例：

（1）calModule.js:

```js
var a = 1;
function add () {
  return ++a;
}
exports.add = add;
```

（2）main.js：（在 main.js 中引入 hello.js 模块）

```js
var addModule1 = require('./calModule')
var addModule2 = require('./calModule')
console.log(addModule1.add());
console.log(addModule2.add());
```

在命令行执行 `node main.js` 运行程序，打印结果：

```js
2
3
```

从打印结果中可以看出，`calModule.js`这个模块虽然被引用了两次，但只初始化了一次。

### 3.13.commonjs-基于浏览器端的实现举例

在工程文件中新建如下目录和文件：

```js
js
    dist //打包生成文件的目录
    src //源码所在的目录
      | module1.js
      | module2.js
      | module3.js
      | app.js //应用主源文件
index.html    //因为CommonJS是基于浏览器端，js文件要跑在浏览器的页面上，所以要有这个html页面
```

然后在根目录下新建如下命令：

```js
  npm init
```

然后根据提示，依次输入如下内容：

- **包名**：可以自己起包名，也可以用默认的包名。注意，包名里不能有中文，不能有大写。
- **版本**：可以用默认的版本 1.0.0，也可以自己修改包名。

其他的参数，一路回车即可。

于是，根目录下会自动生成`package.json`这个文件。点进去看一下：

```js
{
  "name": "commonjs_browser",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

### 3.14 下载第三方包：Browserify

这里需要用到[Browserify](http://browserify.org/)这个工具进行编译打包。Browserify 称为 CommonJS 的浏览器端的打包工具。

输入如下命令进行安装：（两个命令都要输入）

```js
    npm install browserify -g          //全局
    npm install browserify --save-dev  //局部。
```

上面的代码中，`-dev`表示开发依赖。这里解释一下相关概念：

- 开发依赖：当前这个包，只在开发环境下使用。
- 运行依赖：当前这个包，是在生产环境下使用。

### 3.15 自定义模块 & 代码运行

（1）module1.js：

```js
//暴露方式一：module.exports = value
//暴露一个对象出去
module.exports = {
    name: '我是 module1',
    foo(){
        console.log(this.name);
    }
}
//我们不能再继续写 module.exports = xxx。因为重新赋值，会把之前的赋值覆盖掉。
```

（2）module2.js：

```js
//暴露方式一：module.exports = value
//暴露一个函数出去
module.exports = function(){
    console.log('我是 module2');
}
```

注意，此时暴露出去的 exports 对象 等价于整个函数。

（3）module3.js：

```js
//暴露方式二：exports.xxx = value

//可以往export对象中不断地添加属性，进行暴露

exports.foo1 = function(){
    console.log('module3 中的 foo1 方法');
}
exports.foo2 = function(){
    console.log('module3 中的 foo2 方法');
}
```

（4）app.js：（将其他模块汇集到主模块

引入的路径解释：

- `./`是相对路径，指的是当前路径（app.js的当前路径是src）

到此，我们的主要代码就写完了。

但是，如果我们直接在index.html中，像下面这样写，是不行的：（因为浏览器不认识 require 关键字）

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <script src="./js/src/app.js"></script>
</body>
</html>
```

为了能够让index.html引入app.js，我们需要输入如下命令：

打包处理js:

```js
    browserify js/src/app.js -o js/dist/bundle.js
```

然后在index.html中引入打包后的文件：

```js
    <script type="text/javascript" src="js/dist/bundle.js"></script>
```

### 3.16 ES模块化书写

首先需要在该文件夹下通过npm init 创建一个json文件，并添加type:moudule属性。

![image-20230821152235541](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230821152235541.png)

![image-20230821152305104](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230821152305104.png)

结果

![image-20230821152324038](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230821152324038.png)

### 3.17 模块的加载机制



## 4.npm

### 4.1  npm介绍

什么是包？

Node.js中第三方模块又叫做包。包与第三方模块是同一个概念。

包的来源：不同于Node.js中的内置模块与自定义模块，包是由第三方个人或者团队进行开发的，免费供所有人使用。node.js的包是免费并且开源的。

**NPM**：Node Package Manager。官方链接： https://www.npmjs.com/

### 4.2 npm的命令

输入 `npm -v`，查看 npm 的版本

（1）初始化:标识自己的信息，也记录别人包的信息

```js
npm init
```

（2）只在当前工程下安装指定的包：

```js
npm install [package]（uninstall,update)   等价于npm install [package] --save
```

（3）在**全局安装**指定的包：

```js
npm install -g [package]（uninstall,update)
```

（4）**局部安装**--安装的包只用于开发环境，不用于生产环境：（会出现在 package.json 文件中的 devDependencies 属性中）

```js
npm install [package] --save-dev（uninstall,update)  与npm install [package] --save区别在于json文件的依赖名写法
# 或者
npm install [package] -D
```

（5）列举目录下的安装包（不加g表示当前目录下）

```js
npm list -g
```

（6）获取包的详细信息

```js
npm info 包名
```

（7）检查包是否已经过时

```js
npm outdated
```

（8）下载指定版本的包

```js
npm i 包名@版本号
```

### 4.3 npm下载包后的结构

项目文件夹下多了node_modules的文件夹和package-lock.json,初始化后有package.json文件。

node_modules：存放所有已经安装到项目中的包。

package-lock.json:用来记录node_modules目录下每一个包的下载信息，名字版本号以及下载地址等。

package.json：自定义包的信息，结构如下：

![image-20230821120509413](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230821120509413.png)

**注意：当要把这个包给别人下载的话，可以直接把package-lock.json和package.json文件发给他，利用这两个文件直接在当前目录终端输入npm -i就可以下载和package.json文件一样版本号的包了。**

![image-20230821121052259](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230821121052259.png)

### 4.4 解决下载包速度慢的方式

##### 方式一  增设服务器

![image-20230821134057156](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230821134057156.png)

##### 方式二：切换npm的下包镜像源

**镜像：是一种文件存储形式，一个磁盘上的数据在另一个磁盘上存在完全相同的副本即为镜像。**

由于 npm 默认的下载地址在国外（npmjs.com），有时候会被墙，导致无法下载或者下载很慢。因此，我们可以尝试切换成，从其他的镜像源下载 npm 包。

切换镜像源，有下面这几种方式：

方式 1：临时切换镜像源。

方式 2：切换镜像源

方式 3：通过 NRM 切换镜像源（最为推荐的方式）。

方式 4：cnpm。

下包镜像源指的是下包的服务器地址。

```js
//查看当前的下包镜像源
npm config get registry
//将下包的镜像源切换到淘宝镜像源
npm config set registry=https://registry.npmmirror.com/
//查看镜像源是否下载成功
npm config get registry
```

##### 方式三 全局安装nrm

**NRM**：Node Registry Manager。是npm的镜像管理工具，有时候国外资源太慢，使用这个就可以快速地在npm源间切换，作用是：**切换和管理 npm 包的镜像源**。

手动切换方法

```js
npm config set registry=https://registry.npmmirror.com/
```

（1）**安装**nrm

在命令行执行命令 **npm install -g nrm** ，全局安装nrm，若出现系统提示禁止运行脚本，则执行set-ExecutionPolicy RemoteSigned命令，选y后重新输入命令即可。

（2）**使用**nrm

执行命令 **nrm ls** 查看可选的源，其中带*的是当前使用的源。

![image-20230821144358910](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230821144358910.png)

（3）**切换**nrm 

如果要切换到taobao源，执行命令**nrm use taobao**。

（4）**测试速度**

可以通过 **nrm test** 测试相应源的响应时间

#### 扩展

中国NPM镜像：这是一个完整的npmjs.org镜像。

安装`cnpm`替换 npm（npm 由于源服务器在国外，下载包的速度较慢，cnpm 会使用国内镜像）：

```js
$ npm install -g cnpm --registry=https://registry.npmmirror.com
```

以后我们就可以通过 cnpm 命令去安装一个包。举例如下：

```js
//安装 vue 这个包
cnpm install vue
```

#### yarn的使用

（1）下载yarn

```js
npm install -g yarn
```

对比npm:

​      速度超快：Yarn缓存了每个下载过的包，再次使用时无需重复下载，同时利用并行下载以最大化资源利用率，因此安装速度更快。

​     超级安全：在执行代码之前，yarn会通过算法校验每个安装包的完整性。

（2）开始新项目

```js
yarn init
```

（3）添加依赖包

```js
yarn add [package]
yarn add [package]@[version]
yarn add [package] --dev
```

（4）升级依赖包

```js
yarn upgrade [package]@[version]
```

（5）移除依赖包

```js
yarn remove [package]
```

（6）安装项目的全部依赖

```js
yarn install
```

## 5.包

### 5-1 包的分类

##### （1）项目包

那些被安装到项目的node_modules目录中的包，都是项目包。

项目包分为两类：

- 开发依赖包（被记录到devDependencies节点中的包，只在开发期间用到）**npm i 包名**  **-D**
- 核心依赖包（被记录到Dependencies节点中的包，在开发期间和项目上线之后会用到）**npm i 包名**

##### （2）全局包

在执行npm install 命令时，如果提供了-g参数，则会把包安装为全局包。使用uninstall卸载

全局包会安装到C:\Users\用户目录\AppData\Roaming\npm\node_modules目录下。

##### （3）i5ting_toc

i5ting_toc是一个可以把md文档转为html页面的小工具，使用步骤如下：

```js
//将i5ting_toc安装为全局包
npm install -g i5ting_toc
//调用i5ting_toc轻松实现md转为html功能
i5ting_toc -f 要转换文件的路径 -o
```

### 5-2 规范的包结构

一个规范的包结构必须包含以下三点要求：

（1）包必须以单独的目录而存在。

（2）包的顶级目录下要必须包含package.json这个包管理配置文件。

（3）package.json中必须包含name,version,main这三个属性，分别代表包的名字，版本号，包的入口。

### 5-3 编写包的说明文档

包根目录中的README.md文件，是包的使用说明文档，通过它，我们可以事先把包的使用说明，以markdown的格式写出来，方便用户参考。

README文件具体写什么内容没有强制要求，清晰地把包的作用，用法，注意事项描述清楚即可。

## 6.内置模块--http

http 模块是 Node.js 官方提供的、用来创建 web 服务器的模块。

#### （1)创建基本 Web 服务器

```js
var http = require("http");
//创建服务器
http.createServer((req, res) => {
    //req 接收浏览器传的参数
    //res返回渲染的内容
    //接收浏览器传输的参数，返回渲染内容
    //响应头  charset=utf-8 设置中文
    res.writeHead(200, { "Content-Type": "text/html;charset=utf-8" });
    //当为text/plain时就会显示html和br等字符
    res.write(`
       <html>
        <b>hello</b>
        <div>大家好</div>
       </html>
    `);
    res.write("hello world");//当把这个放在html前面就会显示整段标签不会显示结果
    //res.end([1, 2, 3]);//保错
    res.end('[1, 2, 3]');//表示响应传输完毕
}).listen(3000, () => {
    console.log("server start");
})
```

![image-20230822204926430](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230822204926430.png)

#### （2）根据不同url响应不同页面以及status状态码

```js
//server.js
var status = require("./module/status");
var renderhtml = require("./module/renderHTML");
var http = require("http");
//创建服务器
http.createServer((req, res) => {
    //req 接收浏览器传的参数
    //res返回渲染的内容
    //接收浏览器传输的参数，返回渲染内容
    //响应头  charset=utf-8 设置中文
    if (req.url === '/favicon.ico') {
        //消除返回本地图标
        return
    }
    console.log(req.url);
     var pathname = url.parse(req.url).pathname;
    res.writeHead(status.renderStatus(req.url), { "Content-Type": "text/html;charset=utf-8" });//当为text/plain时就会显示html和br等字符
    res.write(renderhtml.renderHTML(pathname));
    res.write("hello world");//当把这个放在html前面就会显示整段标签不会显示结果
    //res.end([1, 2, 3]);//保错
    res.end('[1, 2, 3]');//表示响应传输完毕
}).listen(3000, () => {
    console.log("server start");
})

```

```js
//renderHTML.js
function renderHTML(url) {
    switch (url) {
        case "/home":
            return `
            <html>
            <b>hello</b>
            <div>home页面</div>
            </html>
           `
        case "/list":
            return `
            <html>
            <b>hello</b>
            <div>list页面</div>
            </html>
            `
        case "/json":
            return `{ name: "juik" }
            `
        default:
            return `
                < html >
            <b>hello</b>
            <div>404 not found</div>
            </html > ` 
    }
}
module.exports.renderHTML = renderHTML;
```

```js
//renderStatus.js
function renderStatus(url) {
    var arr = ["/home", "/list"];
    return arr.includes(url) ? 200 : 404;
}
exports.renderStatus = renderStatus;
```

#### （3）创建服务器的两种写法

##### 3-1 方法一

```js
var server = http.createServer();
server.on("request",(req, res) => { 
    res.write("hello world");
})
server.listen(3000, () => {
    console.log("server start");
})
```

##### 3-2 方法二

```js
http.createServer((req, res) => {
    res.write("hello world");
}).listen(3000, () => {
    console.log("server start");
})

```

#### （4）jsonp接口

实现跨域

```js
//jsonp.js
var http = require("http");
var url = require("url");
http.createServer((req, res) => {
    var urlobj = url.parse(req.url, true);
    console.log(urlobj.query);//[Object: null prototype] { callback: 'test' }
    console.log(urlobj.query.callback);//test
    switch (urlobj.pathname) {
        case "/api/aaa":
            res.end(`${urlobj.query.callback}(${JSON.stringify({
                name: "kerwin",
                age: 200,
                birth: 2022
            })})`)
            break;
        default:
            res.end('404');
    }
}).listen(3000)
```

```js
//index.js
<body>
    <script>
        var oscript = document.createElement("script");
        oscript.src = "http://127.0.0.1:3000/api/aaa?callback=test";
        document.body.appendChild(oscript);
        function test(obj) {
            console.log(obj);
        }
    </script>
</body>
```

![image-20230826134140234](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230826134140234.png)

**![image-20230826134324883](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230826134324883.png)**

#### （5）cors

```js
//json.js
var http = require("http");
var url = require("url");
http.createServer((req, res) => {
    var urlobj = url.parse(req.url, true);
    console.log(urlobj.query);//[Object: null prototype] { callback: 'test' }
    console.log(urlobj.query.callback);//test
    res.writeHead(200, {
        "Content-Type": "application/json;charset=utf-8",
        //cors头
        "access-control-allow-origin":"*"
    })
    switch (urlobj.pathname) {
        case "/api/aaa":
            res.end(`${JSON.stringify({
                name: "kerwin",
                age: 200,
                birth: 2023
            })}`)
            break;
        default:
            res.end('404');
    }
}).listen(3000)
```

```js
//json.html
<body>
    <script>
        fetch("http://127.0.0.1:3000/api/aaa")//请求的后端服务器网址
        .then(res=>res.json())
        .then(res=>{
            console.log(res);
        })
    </script>
</body>
```

![image-20230826145719308](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230826145719308.png)

#### （6）get



![image-20230826210623469](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230826210623469.png)

从猫眼中爬取数据

```js
//get.js
var http = require("http");
var https = require("https");
var url = require("url");
http.createServer((req, res) => {
    var urlobj = url.parse(req.url, true);
    //console.log(urlobj.query);//[Object: null prototype] { callback: 'test' }
    //console.log(urlobj.query.callback);//test
    res.writeHead(200, {
        "Content-Type": "application/json;charset=utf-8",
        //cors头
        "access-control-allow-origin": "*"
    })
    switch (urlobj.pathname) {
        case "/api/movie":
            httpget((data) => {
                res.end(data);
            });
            break;
        default:
            res.end('404');
    }
}).listen(3000)
function httpget(cb) {
    var data = "";
    https.get(`https://i.maoyan.com/api/mmdb/movie/v3/list/hot.json?ct=%E6%8F%AD%E9%98%B3&ci=288&channelId=4`, (res) => {
        res.on("data", (chunk) => {
            data += chunk;
        })
        res.on("end", () => {
            console.log(data);
            cb(data);
           // response.end(data);//响应回传到前端控制台  方式一
        })
    })
}
```

```js
//get.html
<body>
    <script>
        fetch("http://127.0.0.1:3000/api/movie")
            .then(res => res.json())
            .then(res => {
                console.log(res);
            })
    </script>
</body>
```

![image-20230826212639559](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230826212639559.png)

​                                                           live-server服务器打开

#### （7）post

向小米有品请求数据

```js
//post.js
var http = require("http");
var https = require("https");
const { json } = require("stream/consumers");
var url = require("url");
http.createServer((req, res) => {
    var urlobj = url.parse(req.url, true);
    res.writeHead(200, {
        "Content-Type": "application/json;charset=utf-8",
        //cors头
        "access-control-allow-origin": "*"
    })
    switch (urlobj.pathname) {
        case "/api/phone":
            httppost((data) => {
                res.end(data);
            });
            break;
        default:
            res.end('404');
    }
}).listen(3000)
const postData = JSON.stringify({
    'msg': 'Hello World!',
});
function httppost(cb) {
    var data = "";
    var options = {
        hostname: "m.xiaomiyoupin.com",
        port: "443",
        path: "/mtop/market/search/placeHolder",
        method: "POST",
        headers: {
            "Content-Type": "application/json"
            //"Content-Type":"x-www-form-urlencoded"
        }
    }
    var req = https.request(options, (res) => {
        res.on("data", (chunk) => {
            data += chunk;
        })
        res.on("end", () => {
            console.log(data);
            cb(data);
        })
    })
    req.write(JSON.stringify([{}, { "baseParam": { "ypClient": 1 } }]));//设置请求体
    //req.write("name=ker&age=18");这个是"x-www-form-urlencoded"设置的
    req.end();
}
```

```js
//post.html
<body>
    <script>
        fetch("http://127.0.0.1:3000/api/phone")
            .then(res => res.json())
            .then(res => {
                console.log(res);
            })

    </script>
</body>
```



#### （8）一些常用方法

```js
request.write(chunk[, encoding][, callback])
//发送一块正文,此方法可以被多次调用。 如果没有设置 Content-Length，则数据将自动使用 HTTP 分块传输编码进行编码，以便服务器知道数据何时结束。 
```

```js
http.request(url[, options][, callback])//函数允许显式地触发请求。
//url 可以是字符串或URL对象。 如果url是字符串，则会自动使用new URL()解析。 如果是URL对象，则会自动转换为普通的options对象。
//例子
const http = require('http');
const postData = JSON.stringify({
  'msg': 'Hello World!',
});
const options = {
  hostname: 'www.google.com',
  port: 80,
  path: '/upload',
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Content-Length': Buffer.byteLength(postData),
  },
};
const req = http.request(options, (res) => {
  res.setEncoding('utf8');
  res.on('data', (chunk) => {
    console.log(`BODY: ${chunk}`);
  });
  res.on('end', () => {
    console.log('No more data in response.');
  });
});
// Write data to request body
req.write(postData);
req.end();
```

#### (9)扩展辨别

![image-20230827154354512](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230827154354512.png)

上图为请求体的内容

`Request Payload`更准确的说是`http request的payload body`。一般用在数据通过`POST`请求或者PUT请求。它是`HTTP`请求中空行的后面那部分**请求体**。

如果你提交了一个html表单并且配置上了method=“post”，并且设置了Content-Type: application/x-www-form-urlencoded或者Content-Type: multipart/form-data。那么你的请求可能长这个样：

```js
POST /some-path HTTP/1.1
Content-Type: application/x-www-form-urlencoded
foo=bar&name=John
```

**这里的form-data就是request payload。**

**<u>form-data`和`request payload的区别就是他们是因为`Content-Type`设置的不同，并不是数据提交方式的不同</u>**，这两种提交都会将数据放在`message-body`中。

1.当我们传递**字符串**的时候，`Content-Type`自动转为`xxx-form-xxx`的形式。当为**对象**的时候，自动转化为`xxx/json`。

2.字符串的时候以`key1=val1&key2=val2`的形式体现，对象以**JSON字符串**形式体现。

![image-20230827162927599](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230827162927599.png)

## 7.内置模块 ---URL

#### （1）Url旧版模块

#### 1-1 url.parse

```js
var url = require("url");
//创建服务器
http.createServer((req, res) => {
    if (req.url === '/favicon.ico') {
        return
    }
console.log(url.parse(req.url));
```

![image-20230823203954701](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230823203954701.png)

![image-20230823203502990](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230823203502990.png)

下面以http://localhost:3000/list/api?zhang=1&age=2为例

```js
url.parse(req.url).query       //获取url后面？之后的数据  返回zhang=1&age=2
url.parse(req.url,true).query  //将url后面？之后的数据转为json格式 
                                //返回[Object: null prototype] { zhang: '1', age: '2' }
url.parse(req.url,true).query.zhang  //获取url后面？之后的数据的某个属性，返回的是1
url.parse(req.url).pathname    //获取url的路径，返回/list/api
```

#### 1-2 url.format

```js
const urlObject = {
    protocol: 'https:',
    slashes: true,
    auth: null,
    host: 'www.baidu.com:443',
    port: '443',
    hostname: 'www.baidu.com',
    hash: '#tag=110',
    search: '?a=1&age=2',
    query: { a: '1', age: '2' },
    pathname: '/ad/index.html',
    path: '/list/index.html?a=1&age=2',
}
const parseobj = url.format(urlObject);
console.log(parseobj);
```

![image-20230823211932584](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230823211932584.png)

#### 1-3 url.resolve

```js
var a = url.resolve('/one/two/three', 'four');
var b = url.resolve('http://example.com/', '/one');
var c= url.resolve('http://example.com/one/njnm/mmmm', '/two');
console.log(a+'\n'+b+'\n'+c);
```

![image-20230823212715771](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230823212715771.png)

**注意**:**当resolve的第二个参数有加/时，代表第二个参数的字符串替换前面是一个参数地址中的第一个/后面的所有内容**。

### （2）URL模块新版

#### 2-1 `new URL(input[, base])`

- `input`要解析的绝对或相对的输入网址, 如果 `input` 是相对的，则需要 `base`。 如果 `input` 是绝对的，则忽略 `base`。
- `base` 如果 `input` 不是绝对的，则为要解析的基本网址。

如果 `input` 或 `base` 不是有效的网址，则将抛出 `TypeError`。

```js
const myURL = new URL('/foo', 'https://example.org/');
// https://example.org/foo
//与resolve用法相同
var c = url.resolve('http://example.com/one/bbbb/mmmm', '/two');//http://example.com/two
var c=new URL('/two','http://example.com/one/bbbb/mmmm');
console.log(c);
console.log(c.href);//http://example.com/two
```

![image-20230824134650387](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230824134650387.png)

​                                                                           console.log(c);

#### 2-2 `URLSearchParams`

https://nodejs.cn/api/url.html#urlsearchparamsgetname

`URLSearchParams` API 提供对 `URL` 查询的读写访问。

```js
const myURL = new URL('https://example.org/?abc=123');
console.log(myURL.searchParams.get('abc'));
// Prints 123
const myURL = new URL('http://127.0.0.1:3000/home?a=1&b=2');
console.log(myURL.searchParams);//URLSearchParams { 'a' => '1', 'b' => '2' }
for (var obj of myURL.searchParams) {
        console.log(obj);
 }//[ 'a', '1' ]  [ 'b', '2' ]
for (var [key,value] of myURL.searchParams) {
        console.log(key ,value);
}//a 1  b 2
console.log(myURL.searchParams.get("a"));//1
//对于网址为http://127.0.0.1:3000/home?a=1&b=2&a=3
console.log(myURL.searchParams.getAll("a"));//[ '1', '3' ]
console.log(myURL.searchParams.keys();//URLSearchParams Iterator { 'a', 'b', 'a' }
```

#### 2-3 `url.format(URL[, options])`

​     该方法允许对输出进行基本的自定义。

   options选项：

- `auth` 如果序列化的网址字符串应包含用户名和密码（：前后面内容），则为 `true`，否则为 `false`。 **默认值：** `true`。
- `fragment` 如果序列化的网址字符串应包含片段（#后面的内容），则为 `true`，否则为 `false`。 **默认值：** `true`。
- `search`如果序列化的网址字符串应包含搜索查询（？后面的内容），则为 `true`，否则为 `false`。 **默认值：** `true`。
- `unicode` `true`表示 如果出现在网址字符串的主机组件中的 Unicode 字符应该被直接编码而不是 Punycode 编码。 **默认值：** `false`。

```js
const myURL1 = new URL('https://a:b@測試?abc#foo');
console.log(myURL1.href);// https://a:b@xn--g6w251d/?abc#foo
console.log(url.format(myURL1, { unicode: true }));//https://a:b@測試/?abc#foo
console.log(url.format(myURL1));//https://a:b@xn--g6w251d/?abc#foo
console.log(url.format(myURL1, { fragment: false, unicode: true, auth: false }));//https://測試/?abc
```

#### 2-4 `url.fileURLToPath(url)`

此函数可确保正确解码百分比编码字符，并确保跨平台有效的绝对路径字符串。例如将盘符的文件路径解码。

- 返回完全解析的特定于平台的 Node.js 文件路径。

```js
//引入模块
const { fileURLToPath } = require('node:url'); 
console.log(new URL('file:///C:/path/你好.txt').pathname ); ///C:/path/%E4%BD%A0%E5%A5%BD.txt
console.log(fileURLToPath('file:///C:/path/你好.txt'));//C:\path\你好.txt  window下
```

#### 2-5 `url.pathToFileURL(path)`

该函数确保 `path` 被绝对解析，并且在转换为文件网址时正确编码网址控制字符。将url转换为正确的文件盘符下的绝对路径。

- 返回：文件网址对象。

```js
const { pathToFileURL } = require('node:url');
console.log(new URL('/some/path%.c', 'file:') );    // Incorrect: file:///some/path%.c
console.log(pathToFileURL('/testp/1.txt').pathname);// Correct:/D:/testp/1.txt (POSIX)
console.log(pathToFileURL('/testp/1.txt').href);    //file:///D:/testp/1.txt
```

#### 2-6 `url.urlToHttpOptions(url)`

该实用函数按照 [`http.request()`](https://nodejs.cn/api/http.html#httprequestoptions-callback) 和 [`https.request()`](https://nodejs.cn/api/https.html#httpsrequestoptions-callback) API 的预期将网址对象转换为普通选项对象。

```js
const { urlToHttpOptions } = require('node:url');
const myURL3 = new URL('https://a:b@測試?abc#foo');
console.log(myURL3);
console.log(urlToHttpOptions(myURL3));
//两个结果的差别在于字段的不同
```

![image-20230824151401098](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230824151401098.png)

![image-20230824151428182](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230824151428182.png)

## 8.内置模块--querystring

### 8-1 `querystring.parse(str[, sep[, eq[, options]]])`

- `str`  要解析的网址查询字符串
- `sep`  用于在查询字符串中分隔键值对的子字符串。 **默认值：** `'&'`。
- `eq`    用于分隔查询字符串中的键和值的子字符串。 **默认值：** `'='`

```js
var str = "name=ker&age=5&location=dalian";
var querystring = require("querystring");
var obj = querystring.parse(str);
console.log(obj);//[Object: null prototype] { name: 'ker', age: '5', location: 'dalian' }

```



### 8-2 `querystring.stringify(obj[, sep[, eq[,options]]])`

- `obj` 要序列化为网址查询字符串的对象
- `sep` 用于在查询字符串中分隔键值对的子字符串。 **默认值：** `'&'`。
- `eq`  用于分隔查询字符串中的键和值的子字符串。 **默认值：** `'='`。

```js
var myobj = {
    a: 2,
    b: 7,
    c:8
}
var str = querystring.stringify(myobj);
console.log(str);//a=2&b=7&c=8

var str1 = querystring.stringify(myobj,':',"-");
console.log(str1);//a-2:b-7:c-8
```

### 8-3 escape/unescape

`querystring.escape()` 方法以针对网址查询字符串的特定要求优化的方式对给定的 `str` 执行网址百分比编码。

`querystring.unescape()` 方法在给定的 `str` 上执行网址百分比编码字符的解码。

```js
var str1 = 'id=3&city=北京&url=https://www.baidu.com'
var escaped = querystring.escape(str1);
console.log(escaped);//id%3D3%26city%3D%E5%8C%97%E4%BA%AC%26url%3Dhttps%3A%2F%2Fwww.baidu.com

var str2 = 'id%3D3%26city%3D%E5%8C%97%E4%BA%AC%26url%3Dhttps%3A%2F%2Fwww.baidu.com'
var unescaped = querystring.unescape(str2);
console.log(unescaped);//id=3&city=北京&url=https://www.baidu.com
```

#### 9.event模块

所有触发事件的对象都是 `EventEmitter` 类的实例。`eventEmitter.on()` 方法用于注册监听器，`eventEmitter.emit()` 方法用于触发事件。

```js
const EventEmitter = require('events');
const event = new EventEmitter();
event.on('play', (data) => {
    console.log("事件触发了play", data);
})
event.on('run', (data) => {
    console.log("事件触发了run", data);
})
setTimeout(() => {
    event.emit("play", "gsyhyfy");
}, 2000)//事件触发了play

```

改造get请求

```js
var http = require("http");
var https = require("https");
const EventEmitter = require("events");
var url = require("url");
var event = null;
http.createServer((req, res) => {
    var urlobj = url.parse(req.url, true);
    //console.log(urlobj.query);//[Object: null prototype] { callback: 'test' }
    //console.log(urlobj.query.callback);//test
    res.writeHead(200, {
        "Content-Type": "application/json;charset=utf-8",
        //cors头
        "access-control-allow-origin": "*"
    })
    switch (urlobj.pathname) {
        case "/api/movie":
            event = new EventEmitter();
            event.on("play", (data) => {
                console.log(data);
                res.end("hug");
            })
            httpget();
            break;
        default:
            res.end('404');
    }
}).listen(3000)
function httpget(cb) {
    var data = "";
    https.get(`https://i.maoyan.com/api/mmdb/movie/v3/list/hot.json?ct=%E6%8F%AD%E9%98%B3&ci=288&channelId=4`, (res) => {
        res.on("data", (chunk) => {
            data += chunk;
        })
        res.on("end", () => {
            console.log(data);
            event.emit("play");
        })
    })
}
```



## 9.fs文件系统模块

#### 9-1 定义

fs模块是Node.js官方提供的用来操作文件的模块，它提供了一系列的属性和方法，用来满足用户对文件的操作需求。

在js代码中，使用fs模块操作文件的导入方法：

```js
const fs=require('fs')
```

#### 9-2  fs.readFile()方法：读取指定文件中的内容

```js
fs.readFile(path[, options], callback)
```

- `path`：必选参数，文件路径
- options ：可选参数，表示以什么编码格式来读取文件。
  - `encoding`：编码格式
  - `flag`：打开方式
- callback：回调函数
  - `err`：错误信息
  - `data`：读取的数据，如果未指定编码格式则返回一个 Buffer

如果读取成功，则err的值为null；如果读取失败，则err的值为错误对象，dataStr的值为undefined。

```js
const fs = require('fs');
fs.readFile('1.txt', 'utf8', function (err, dataStr) {
    if (err) {
        return console.log('读取失败' + err.message);
    }
    console.log('文件读取成功');
    console.log(err);//null
    console.log(dataStr);//1.txt内容
})
//异步读取文件
const fs = require('fs').promises;
fs.readFile('2.txt', 'utf8').then(result => {
    console.log(result);
})
```

![image-20230820212140355](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820212140355.png)

#### 9-3 fs.writeFile()方法：向指定文件中写入内容

```js
fs.writeFile(file, data[, options], callback)//当下一次写入时上一次的内容不会保留
```

- `file`：文件路径
- `data`：写入内容
- `options`：配置选项，包含 `encoding, mode, flag`；若是字符串则指定编码格式，可选参数，默认utf8
- `callback`：回调函数

如果读取成功，则err的值为null；

```js
const fs = require('fs');
fs.writeFile('2.txt', '这是写入文件', function (err, dataStr) {
    if (err) {
        return console.log('写入失败' + err.message);
    }
    console.log(err);//null

})
```

将字符串首字母变成大写的方法：

```js
function upper(str) {
    return str.substring(0, 1).toUpperCase() + str.substring(1);
}
var res = upper('hyju');
console.log(res);
```

#### 9-4 appendFile 追加文件内容

```js
const fs = require('fs');
//error-first
fs.appendFile('2.txt', '\n哈哈哈', function (err, dataStr) {
    if (err) {
        return console.log('写入失败' + err.message);
    }
    console.log(err);//null
})
```

#### 9-5 mkdir创建目录

```js
const fs = require("fs");
fs.mkdir("./avator", (err) => {
    console.log(err);
})//null
```

#### 9-6 rmdir删除目录

目录为空时是可删除的

```js
const fs = require("fs");
fs.rmdir("./avator2", err => {
    if (err && err.code === "EEXIST") {
        console.log("目录已经存在");
    }
})
```

#### 9-7 rename 重命名

```js
const fs = require("fs");
fs.rename("./avator", "./avator2", (err) => {
    console.log(err);
    if (err && err.code === "ENOENT") {
        console.log("目录不存在");
    }
})
```

#### 9-8 unlink删除文件

```js
const fs = require("fs");
fs.unlink("3.txt",  (err) => {
    console.log(err);
    
})
```

#### 9-9 readdir获取文件夹的文件数

```js
const fs = require('fs');
fs.readdir('fg', (err, dataStr)=> {
    if (!err) {
        console.log(dataStr.length);//2
        console.log(dataStr);
    }
})
```

#### 9-10  stat 

```js
const fs = require('fs');
fs.stat('fg', (err, dataStr)=> {
    console.log(dataStr.isFile());
    console.log(dataStr.isDirectory());//true
})
```

![image-20230828214430193](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230828214430193.png)

#### 9-11 删除目录的所有文件--异步写法

```js
//实践中对于部分文件的处理可能会失效
const fs = require('fs');
fs.readdir('fg', (err, dataStr) => {
    dataStr.forEach(item => {
        fs.unlink(`fg/${item}`,(err)=>{})
    })
    fs.rmdir("fg", (err) => {
        console.log(err);
    });
})
```

```js
//异步promises写法一
const fs = require("fs");
fs.readdir("fg").then(async (dataStr) => {
    let arr=[]
    dataStr.forEach(item => {
        arr.push(fs.unlinkSync(`fg/${item}`))
    })
    //Promise.all([])
    await Promise.all(arr);
    await fs.rmdir("fg");
})
//异步promises写法二
const fs = require("fs");
fs.readdir("fg").then(async (dataStr) => {
    //Promise.all([])
    await Promise.all(dataStr.map(item=>fs.unlink(`fg/${item}`)));
    await fs.rmdir("fg");
})
```



#### 9-12 mkdirSync 同步创建目录

```js
//由于同步创建目录时，若出现报错，报的是服务器的错误，所以要try..catch..抛出错误
const fs = require("fs");
try {
    fs.mkdirSync("fg");//同步创建文件夹
} catch (error) {
    console.log("11",error);//捕获错误
}
```

#### 9-13 删除目录的所有文件--同步写法

```js
const fs = require("fs");
fs.readdir('fg', (err, dataStr) => {
    dataStr.forEach(item => {
        fs.unlinkSync(`fg/${item}`,(err)=>{})//当文件夹所有文件删除完才会执行下一步
    })   
fs.rmdir("fg", (err) => {
    console.log(err);
});   
})
```

在fs模块中，提供同步方法是为了方便使用。那我们到底是应该用异步方法还是同步方法化: js 
由于Node环境执行的JavaScript代码是<u>服务器端代码</u>，所以，绝大部分需要在服务器运行期反复执行业务逻辑的代码，必须使用异步代码，否则，**同步代码在执行时期，服务器将停止响应，因为JavaScript只有一个执行线程**。服务器启动时如果需要读取配置文件，或者结束时需要写入到状态文件时，可以使用同步代码，因为这些代码只在启动和结束时执行一次，不影响服务器正常运行时的异步执行。

异步promises的写法对于上述文件操作方法都有效，如mkdir,readFile,rmdir等等。

#### 9-14判断文件是否存在

`fs.existsSync(path)`如果路径存在则返回 `true`，否则返回 `false`。

```js
if (existsSync('/etc/passwd'))
  console.log('The path exists.'); 
```

## 10.stream流模块

stream是Nodejs提供的又一个仅在服务区端可用的模块，目的是支持“流”这种数据结构。
什么是流?流是一种抽象的数据结构。想象水流，当在水管中流动时，就可以从某个地方(例如自来水厂)源源不断地到达另一个地方(比如你家的洗手池)。我们也可以把数据看成是数据流，比如你敲键盘的时候，就可以把每个字符依次连起来，看成字符流。这个流是从键盘输入到应用程序，实际上它还对应着一个名字:标准输入流(stdin)。

#### 10-1 readStream 读取流

```js
const fs = require("fs");
const rs = fs.createReadStream("1.txt", "utf-8")
rs.on("data", (chunk) => {
    console.log("chunk--"+chunk);
})
rs.on("end", () => {
    console.log("end");
})
rs.on("error", (err) => {
    console.log(err);
})
```

**注意：data事件可能会有很多次，每次传递的chunk是流的一部分数据。**

#### 10-2 writeStream 写入流

```js
const fs = require("fs");
const ws = fs.createWriteStream("2.txt", "utf-8")
ws.write("111111111");
ws.write("2222222222");
ws.write("33333333333");
ws.end();
```

**注意：要以流的形式写入文件，只需要不断调用write方法，最后以end结束。**

#### 10-3 pipe管道

pipe可以将两个流串起来，一个readable流和一个writable流，两个流串起来后，所有数据自动从readable流进入writable流，这种操作叫做pipe。

pipe()可以把一个文件流和另一个文件流串起来，这样源文件的所有数据就自动写入到目标文件里了，所以实际上是一个**复制文件**的程序。

```js
const fs = require("fs");
const readStream = fs.createReadStream("1.txt");
const writeStream = fs.createWriteStream("2.txt");
readStream.pipe(writeStream);
```

## 11.zlib模块

![image-20230831113418588](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230831113418588.png)

```js
const http = require("http");
const fs = require("fs");
const zlib = require("zlib");
const gzip = zlib.createGzip();
http.createServer((req, res) => {
    //res本身就是可写
    const readStream = fs.createReadStream("index.js");
    res.writeHead(200, {
        "Content-Type": "application/x-javascript;charset=utf-8","Content-Encoding":"gzip"
    })//设置压缩方式为gzip,否则会乱码
    readStream.pipe(gzip).pipe(res);
}).listen(3000, () => {
    console.log('server start');
})
```

## 12. crypto模块

crypto模块的目的是为了提供通用的加密和哈希算法。用纯JavaScript代码实现这些功能不是不可能，但速度会非常慢。Nodejs用C/C++实现这些算法后，通过cypto这个模块暴露为JavaScript接口，这样用起来方便，运行速度也快。

#### 12-1 md5 

MD5是一种常用的哈希算法，用于给任意数据一个“签名”。这个签名通常用一个十六进制的字符串表示，如果需要计算SHA1，只需要将md5改成sha1即可得到结果。

```js
const crypto = require("crypto");
const hash1 = crypto.createHash("sha1");
const hash = crypto.createHash("md5");
hash.update("hello ji");
hash1.update("hello ji");
console.log(hash.digest("hex"));//8f0e9bdd289de1b49d6c7c39e4c6ca14
console.log(hash1.digest("hex"));//7d98d64f1ad22134300899482bbe40b8843b0225
```

#### 12-2 Hmac算法

Hmac算法也是一种哈希算法，它可以利用MD5或者SHA1等哈希算法，不同的是，Hmac还需要一个密钥：

```js
const crypto = require("crypto");
const hash = crypto.createHash("md5","kerwin");
hash.update("h1234567");
console.log(hash.digest("hex"));//067b8026c215dac215c3f8fd63195327
```

只要密钥发生了变化，同样的输入数据也会得到不同的签名，因此，可以把Hmac理解为用随机数增强的哈希算法。 

#### 12-3 AES算法

AES是一种常用的对称加密算法，加解密都是同一个密钥，crypto模块提供了AES支持，但是需要自己封装好函数，便于使用：加密与解密需要使用同一个算法，例如aes-128-cbc

```js
const crypto = require("crypto");
//加密算法
function encrypt(key, iv, data) {
    let dep = crypto.createCipheriv("aes-128-cbc", key, iv);
    return dep.update(data, 'binary', 'hex') + dep.final('hex');
}
//解密算法
function decrypt(key, iv, crypted) {
    crypted = Buffer.from(crypted, "hex").toString("binary");
    let dep = crypto.createDecipheriv("aes-128-cbc", key, iv);
    return dep.update(crypted, 'binary', 'utf8') + dep.final('utf8');
}
//16位
let key = "abcdef1234567890";
let iv = "tbcdey1234567890";
let data = "kerwin";
let cryted = encrypt(key, iv, data);
console.log('加密结果是：'+cryted);//3df75e66bf1c435ed138c3365f8bc39a
let decrypted = decrypt(key, iv, cryted)
console.log('解密结果是：'+decrypted);//解密结果是：kerwin
```

加密的字符串通过解密可以得到

## 13. 路由

#### 13-1 定义

https://juejin.cn/post/6993840419041706014?searchId=20230831203723736E51EED465FF3967E8

路由(英文：router)就是对应关系， 路由分为前端路由和后端路由， 通俗的讲前端路由就是，Hash 地址与组件之间的对应关系。

前端路由的原理类似，就是匹配不同的 `URL` 路径，进行解析，然后动态地渲染出区域 `HTML` 内容。

##### （1）Hash模式

在 2014 年之前，都是通过 `hash` 来实现前端路由，类似于这样的地址`http://www.xxx.com/#/login`。

在进行页面跳转的操作时，`hash` 值的变化并不会导致浏览器页面的刷新，**只是会触发 `hashchange` 事件**。然后，**通过对 `hashchange` 事件的监听**，我们就可以在 `fn` 函数内部进行动态地页面切换。

```js
window.addEventListener('hashchange',fn)
```

这种模式叫**hash 模式**。

##### hash的定义

`hash` 模式是一种把前端路由的路径用井号 `#` 拼接在真实 `url` 后面的模式。**当井号 `#` 后面的路径发生变化时，浏览器并不会重新发起请求，而是会触发 `onhashchange` 事件**。

##### 网页url组成部分

###### 了解几个url的属性

| 属性               | 含义     |
| ------------------ | -------- |
| location.protocal  | 协议     |
| location.hostname  | 主机名   |
| location.host      | 主机     |
| location.port      | 端口号   |
| location.patchname | 访问页面 |
| location.search    | 搜索内容 |
| location.hash      | 哈希值   |

###### 演示

```js
//http://127.0.0.1:8001/01-hash.html?a=100&b=20#/aaa/bbb
location.protocal // 'http:'
localtion.hostname // '127.0.0.1'
location.host // '127.0.0.1:8001'
location.port //8001
location.pathname //'01-hash.html'
location.serach // '?a=100&b=20'
location.hash // '#/aaa/bbb'
```

##### hash的特点

- hash变化会触发网页跳转，即浏览器的前进和后退。

- **`hash` 可以改变 `url` ，但是不会触发页面重新加载**（hash的改变是记录在 `window.history` 中），即不会刷新页面。也就是说，所有页面的跳转都是在客户端进行操作。因此，这并不算是一次 `http` 请求，所以这种模式不利于 `SEO` 优化。`hash` 只能修改 `#` 后面的部分，所以只能跳转到与当前 `url` 同文档的 `url` 。

- `hash` 通过 `window.onhashchange` 的方式，来监听 `hash` 的改变，借此实现无刷新跳转的功能。

- ##### **`hash` 永远不会提交到 `server` 端**（可以理解为只在前端自生自灭）。



##### （2）history模式

2014 年之后，因为 `HTML5` 标准发布，浏览器多了两个 API：**`pushState` 和 `replaceState`**。通过这两个 API ，**改变 URL 地址，浏览器不会向后端发送请求**，这样我们就能用另外一种方式实现前端路由了。

```js
window.addEventListener('popstate', fn)
```

这种模式叫**history 模式**。

##### 定义

`history API` 是 `H5` 提供的新特性，允许开发者**直接更改前端路由**，即更新浏览器 `URL` 地址而**不重新发起请求**。

##### 与hash的区别

我们用一个例子来演示， `hash` 与 `history` 在浏览器下刷新时的区别。**具体如下：**

**正常页面浏览**

```powershell
https://github.com/xxx 刷新页面

https://github.com/xxx/yyy 刷新页面

https://github.com/xxx/yyy/zzz 刷新页面
```

**改造H5 history模式**

```powershell
https://github.com/xxx 刷新页面

https://github.com/xxx/yyy 前端跳转，不刷新页面

https://github.com/xxx/yyy/zzz 前端跳转，不刷新页面
```

##### history的API

下面阐述几种 `HTML5` 新增的 `history API` 。具体如下表：

| API                                       | 定义                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| history.pushState(data, title [, url])    | pushState主要用于**往历史记录堆栈顶部添加一条记录**。各参数解析如下：**①data**会在onpopstate事件触发时作为参数传递过去；**②title**为页面标题，当前所有浏览器都会忽略此参数；③**url**为页面地址，可选，缺少时表示为当前页地址 |
| history.replaceState(data, title [, url]) | 更改当前的历史记录，参数同上； 上面的pushState是添加，这个更改 |
| history.state                             | 用于存储以上方法的data数据，不同浏览器的读写权限不一样       |
| window.onpopstate                         | 响应pushState或者replaceState的调用                          |

##### history的特点

对于 `history` 来说，主要有以下特点：

- 新的 `url` 可以是与当前 `url` 同源的任意 `url` ，也可以是与当前 `url` 一样的地址，但是这样会导致的一个问题是，会把**重复的这一次操作**记录到栈当中。
- 通过 `history.state` ，添加任意类型的数据到记录中。
- 可以额外设置 `title` 属性，以便后续使用。
- 通过 `pushState` 、 `replaceState` 来实现无刷新跳转的功能。

**注意：获取文件绝对路径 __dirname**

```js
  const myURL = new URL(req.url, "http://127.0.0.1");
  console.log(__dirname,myURL.pathname);
```

![image-20230902110951827](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230902110951827.png)

#### 13-2 封装一个路由

![image-20230903102104400](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230903102104400.png)

首先，在server.js中创建http连接，根据前端请求地址渲染不同页面（route.js)中完成，接着通过login.html页面添加登录事件，分别利用get和post请求获得前端输入的用户名与密码信息，接着在api.js书写服务器端获取资源的代码，最后读取静态资源文件（css,js)等。

```html
<!--home.html-->	
<body>
    home
</body>

<!--404.html-->	
<body>
    404
</body>

<!--login.html-->	
<body>
    <div>
        <div>
            用户名：
            <input type="text" id="username">
        </div>
        <div>
            密码：
            <input type="password" id="password">
        </div>
        <div>
            <button id="login">登录--get</button>
            <button id="loginpost">登录--post</button>
        </div>
    </div>
    <script src="/js/login.js"></script>
</body>
```

```css
<!--login.css-->
div{
    width: 300px;
    height: 30px;
    background-color: palegreen;
}
```

```js
//server.js
const http = require("http");
const route = require("./route");
const api = require("./api");
const Router = {};
function use(obj) { //合并对象
     Object.assign(Router, obj);
}
function start() {
    http.createServer((req, res) => {
    //favicon
        const myURL = new URL(req.url, "http://127.0.0.1");
        //console.log(myURL.pathname);
    try {
        Router[myURL.pathname](req,res);
    } catch (error) {
        Router["/404"](req,res);
    }
}).listen(3000, () => {
    console.log("server start");
})}
exports.start = start;
exports.use = use;
```

```js
//route.js
const fs = require("fs");
const path = require("path");
const mime = require("mime");
//方法一
// function route(res, pathname) {
//     switch (pathname) {
//         case "/login":
//             res.writeHead(200, { "Content-Type": "text/html;charset=utf8" });
//             res.write(fs.readFileSync("./static/login.html"), "utf-8");
//             break;
//         case "/home":
//             res.writeHead(200, { "Content-Type": "text/html;charset=utf8" });
//             res.write(fs.readFileSync("./static/home.html"), "utf-8");
//             break;
//         default:
//             res.writeHead(404, { "Content-Type": "text/html;charset=utf8" });
//             res.write(fs.readFileSync("./static/404.html"), "utf-8");
//             break;
//     }
// }

//方法二
function render(res, path, type = "") {
    res.writeHead(200, { "Content-Type": `${type ? type : "text/html"};charset=utf8` });
    res.write(fs.readFileSync(path), "utf-8");
    res.end();
}
const route = {
    "/login": (req,res) => {
        render(res, "./static/login.html")
    },
    "/home": (req,res) => {
        render(res, "./static/home.html")
    },
    "/": (req,res) => {
        render(res, "./static/home.html")
    },
    "/404": (req, res) => {
        if (readStaticFile(req, res)) {
            return
        }
        res.writeHead(404, { "Content-Type": "text/html;charset=utf8" });
        res.write(fs.readFileSync("./static/404.html"), "utf-8");
        res.end();
    },
    // "/favicon.ico": (req,res) => {
    //     render(res, "./static/favicon.ico", "image/x-icon");
    // }
}
function readStaticFile(req,res) {
    //获取路径
    const myURL = new URL(req.url, "http://127.0.0.1");
    console.log(path.join(__dirname, "/static", myURL.pathname));
    //D:\前端FORWARD\JavaScript案例\Node.js\路由\static\css\login.css
    const pathname = path.join(__dirname, "/static", myURL.pathname);
    // if (fs.existsSync("/")) {return false }
    if (fs.existsSync(pathname)) {
        //处理显示返回
        //myURL.pathname.split(".")[1]截取静态文件扩展名
        //console.log(myURL.pathname.split(".")[1]);
        render(res, pathname,mime.getType(myURL.pathname.split(".")[1]));
        return true
    } else {
        return false
    }
}
module.exports = route;
```

```js
//api.js
//各种接口
function render(res, data, type = "") {
    res.writeHead(200, { "Content-Type": `${type ? type : "application/json"};charset=utf8` });
    res.write(data);
    res.end();
}
const apiRouter = {
    "/api/login": (req, res) => {
        //获取参数
        const myURL = new URL(req.url, "http://127.0.0.1")
        //console.log(myURL.searchParams);//获取对象集
        if (myURL.searchParams.get("username") === "kerwin" && myURL.searchParams.get("password") === "123") {
            render(res, `{"ok":1}`);
        } else {
            render(res, `{"ok":0}`);
        }
    },
    "/api/loginpost": (req, res) => {
        //获取参数
        var post = "";
        //收集数据
        req.on("data", chunk => {
            post += chunk;
        })
        req.on("end", () => {
            console.log(post);
            post = JSON.parse(post);
            if (post.username === "kerwin" && post.password === "123") {
                render(res, `{"ok":1}`);
            } else {
                render(res, `{"ok":0}`);
            }
        })
    }
}
exports.apiRouter = apiRouter;
```

```js
//index.js
const server = require("./server");
const route = require("./route");
const api = require("./api");
//注册路由
server.use(route);
server.use(api.apiRouter);
server.start();
```

```js
//login.js
var ologin = document.querySelector("#login");
var plogin = document.querySelector("#loginpost");
var username = document.querySelector("#username");
var password = document.querySelector("#password");
//get请求
ologin.addEventListener("click", () => {
    fetch(`/api/login?username=${username.value}&password=${password.value}`).then(
        res => res.text()).then(res => {
            console.log(res);
        })
})
//get请求
plogin.addEventListener("click", () => {
    fetch(`/api/loginpost`, {
        method: "POST",
        body: JSON.stringify({
            username: username.value,
            password: password.value
        }),
        headers: {
            "Content-Type": "application/json"
        }
    }).then(res => res.text()).then(res => {
        console.log(res);
    })
})
```

![image-20230903103147007](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230903103147007.png)

## 14.path模块

`path.join()` 方法使用特定于平台的分隔符作为定界符将所有给定的 `path` 片段连接在一起，然后规范化生成的路径。零长度的 `path` 片段被忽略。

```js
path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
// Returns: '/foo/bar/baz/asdf'

path.join('foo', {}, 'bar');
// Throws 'TypeError: Path must be a string. Received {}' 
```

`path.extname(path) 方法返回 `path` 的扩展名，即 `path` 的最后一部分中从最后一次出现的 `.`（句点）字符到字符串的结尾。

```js
path.extname('index.html');
// Returns: '.html'

path.extname('index.coffee.md');
// Returns: '.md'
```



## 15.mime自动生成content-type类型

https://www.npmjs.com/package/mime

模块安装：npm i mime

For the full version (800+ MIME types, 1,000+ extensions):

```
const mime = require('mime');

mime.getType('txt');                    // ⇨ 'text/plain'
mime.getExtension('text/plain');        // ⇨ 'txt'
```

## 16. Express

https://express.nodejs.cn/en/4x/api.html#req

### 16-1 安装

```js
npm init
npm i express
```

### 16-2 路由

路由是指确定应用如何响应客户端对特定端点的请求，该端点是 URI（或路径）和特定的 HTTP 请求方法（GET、POST 等）。

每个路由可以有一个或多个处理函数，当路由匹配时执行。

路由定义采用以下结构：

```javascript
app.METHOD(PATH, HANDLER)
```

其中：

- `app` 是 `express` 的一个实例。
- `METHOD` 是小写的 [HTTP 请求方法](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)。
- `PATH` 是服务器上的路径。
- `HANDLER` 是路由匹配时执行的函数。

##### 路由路径

路由路径与请求方法相结合，定义了可以发出请求的端点。 路由路径可以是字符串、字符串模式或正则表达式。

以下是一些基于字符串的路由路径示例

```javascript
//此路由路径将匹配对根路由 `/` 的请求。
app.get('/', (req, res) => {
  res.send('root')
})
//此路由路径将匹配对 `/about` 的请求。
app.get('/about', (req, res) => {
  res.send('about')
})
//此路由路径将匹配对 `/random.text` 的请求。
app.get('/random.text', (req, res) => {
  res.send('random.text')
})
```

以下是一些基于字符串模式的路由路径示例。

```javascript
//此路由路径将匹配 `acd` 和 `abcd`。
app.get('/ab?cd', (req, res) => {
  res.send('ab?cd')
})
//此路由路径将匹配 `abcd`、`abbcd`、`abbbcd` 等。
app.get('/ab+cd', (req, res) => {
  res.send('ab+cd')
})
//此路由路径将匹配 `abcd`、`abxcd`、`abRANDOMcd`、`ab123cd` 等。
app.get('/ab*cd', (req, res) => {
  res.send('ab*cd')
})
//此路由路径将匹配 `/abe` 和 `/abcde`。
x app.get('/ab(cd)?e', (req, res) => {  res.send('ab(cd)?e')})

//用法：用于详情页接口，返回任意路径值随机值，例如商品id
//匹配/ab/******   (:相当于占位符)
app.get("/ab/:id", (req, res) => {
    res.send("ok")
})
//匹配/ab/**/******   (:相当于占位符)
app.get("/ab/:id/:cd", (req, res) => {
    res.send("okf")
})
```

基于正则表达式的路由路径示例：

```javascript
//此路由路径将匹配其中带有 “a” 的任何内容。
app.get(/a/, (req, res) => {
  res.send('/a/')
})
//此路由路径将匹配 `butterfly` 和 `dragonfly`，但不匹配 `butterflyman`、`dragonflyman` 等。
app.get(/.*fly$/, (req, res) => {
  res.send('/.*fly$/')
})
```

##### 基本路由写法

一个以上的回调函数可以处理一个路由（确保你指定了 `next` 对象）。 例如：

```js
app.get("/login", (req, res,next) => {
   console.log("kogin");
    next();//只有调用了next之后才可以进行下面一步的回调
}, (req, res) => {
    res.send("oookkkk")
})
```

 一组回调函数可以处理路由。 例如：

```javascript
const cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}
const cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}
const cb2 = function (req, res) {
  res.send('Hello from C!')
}
//写法一
app.get('/example/c', [cb0, cb1, cb2])
//写法二
app.get('/example/c', [cb0, cb1],(req,res)=>{
      res.send('Hello from C!')
})
```

```js
 //写法三
app.get('/b', (req, res, next) => {
     console.log('the response will be sent by the next function ...');
     var isvalid = true;
     if (isvalid) {
         res.kerwin = "lllll";//res是一个对象，直接给对象添加属性，后面的res也能得到属性值
         next();
     } else {
         res.send("error");
     }
     //当isvalid是false时，就直接执行res.send("error");表示响应完了，后面的回调函数不执行了
 }, (req, res) => {
     console.log(res.kerwin);//获得第一个回调函数的设置值
    res.send('Hellfrom B!')
}) 
```



### 16-3 中间件

Express 是一个路由和中间件 Web 框架，其自身功能最少： Express 应用本质上是一系列中间件函数调用。

中间件函数是可以访问应用请求-响应周期中的 [请求对象](https://express.nodejs.cn/en/4x/api.html#req) (`req`)、[响应对象](https://express.nodejs.cn/en/4x/api.html#res) (`res`) 和下一个中间件函数的函数。 下一个中间件函数通常由一个名为 `next` 的变量表示。

中间件函数可以执行以下任务：

- 执行任何代码。
- 更改请求和响应对象。
- 结束请求-响应周期。
- 调用堆栈中的下一个中间件函数。

如果当前中间件函数没有结束请求-响应循环，它必须调用 `next()` 将控制权传递给下一个中间件函数。 否则，请求将被挂起。

Express 应用可以使用以下类型的中间件：

- [应用级中间件](https://express.nodejs.cn/en/guide/using-middleware.html#middleware.application)
- [路由级中间件](https://express.nodejs.cn/en/guide/using-middleware.html#middleware.router)
- [错误处理中间件](https://express.nodejs.cn/en/guide/using-middleware.html#middleware.error-handling)
- [内置中间件](https://express.nodejs.cn/en/guide/using-middleware.html#middleware.built-in)
- [第三方中间件](https://express.nodejs.cn/en/guide/using-middleware.html#middleware.third-party)

#### 应用级中间件

使用 `app.use()` 和 `app.METHOD()` 函数将应用级中间件绑定到 [app 对象](https://express.nodejs.cn/en/4x/api.html#app) 的实例，其中 `METHOD` 是中间件函数处理的请求的 HTTP 方法（如 GET、PUT 或 POST），小写。

此示例显示了一个没有挂载路径的中间件函数。 每次应用收到请求时都会执行该函数。

```javascript
const express = require('express')
const app = express()

app.use((req, res, next) => {
  console.log('Time:', Date.now())
  next()
})
```

这个例子展示了一个挂载在 `/user/:id` 路径上的中间件函数。 该函数针对 `/user/:id` 路径上的任何类型的 HTTP 请求执行。

```javascript
app.use('/user/:id', (req, res, next) => {
  console.log('Request Type:', req.method)
  next()
})
```

#### 路由中间件

路由级中间件的工作方式与应用级中间件相同，只是它绑定到 `express.Router()` 的实例。

```javascript
const router = express.Router()
```

使用 `router.use()` 和 `router.METHOD()` 函数加载路由级中间件。

示例：

```js
//index.js
const express = require("express");
const app = express();
const Router = require("./indexRouter");
//应用级别
app.use(function (req, res, next) {
    console.log("验证token");
    next();
})
//应用级别
app.use("/", Router);//即匹配一级中间件  /home   /login
//app.use("/api", Router);//即匹配二级中间件  /api/home   /api/login
app.listen(3000, () => {
    console.log("server start");
})
```

```js
//indexRouter.js
const express = require("express");
const router = express.Router();
//路由级别
router.get("/home", (req, res) => {
    res.send("home");
})
router.get("/login", (req, res) => {
    res.send("login");
})
module.exports = router;
```

#### 错误处理中间件

错误处理中间件总是需要四个参数。 你必须提供四个参数以将其标识为错误处理中间件函数。 即使你不需要使用 `next` 对象，你也必须指定它来维护签名。 否则，`next` 对象将被解释为常规中间件，无法处理错误。

以与其他中间件函数相同的方式定义错误处理中间件函数，除了使用四个参数而不是三个参数，特别是使用签名 `(err, req, res, next)`)：

**一般情况下将错误中间件放在末尾**

```javascript
app.use((err, req, res, next) => {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

#### 错误处理

错误处理是指 Express 如何捕获和处理同步和异步发生的错误。 Express 带有一个默认的错误处理程序，因此你无需编写自己的程序即可开始使用。

##### 捕捉错误

确保 Express 捕获运行路由处理程序和中间件时发生的所有错误非常重要。

路由处理程序和中间件内的同步代码中发生的错误不需要额外的工作。 如果同步代码抛出错误，Express 将捕获并处理它。 例如：

```javascript
app.get('/', (req, res) => {
  throw new Error('BROKEN') // Express will catch this on its own.
})
```

对于路由处理程序和中间件调用的异步函数返回的错误，你必须将它们传递给 `next()` 函数，Express 将在其中捕获并处理它们。 例如：

```javascript
app.get('/', (req, res, next) => {
  fs.readFile('/file-does-not-exist', (err, data) => {
    if (err) {
      next(err) // Pass errors to Express.
    } else {
      res.send(data)
    }
  })
})
```

#### 内置中间件

从版本 4.x 开始，Express 不再依赖 [连接](https://github.com/senchalabs/connect)。 以前包含在 Express 中的中间件函数现在位于单独的模块中； 

Express 具有以下内置中间件函数：

[express.static](https://express.nodejs.cn/en/4x/api.html#express.static) 提供静态资源，例如 HTML 文件、图片等。

[express.json](https://express.nodejs.cn/en/4x/api.html#express.json) 使用 JSON 有效负载解析传入请求。 **注意：适用于 Express 4.16.0+**

[express.urlencoded](https://express.nodejs.cn/en/4x/api.html#express.urlencoded) 使用 URL 编码的负载解析传入的请求。 **注意：适用于 Express 4.16.0+**

express.static是Express唯一内置的中间件。它基于serve-static，负责在Express应用中提托管静态资源。每个应用可有多个静态目录。

```js
app.use(express.static('public'))
app.use(express.static(uploads))
app.use(express.static('files'))
```

#### 第三方中间件

使用第三方中间件向 Express 应用添加功能。

安装所需功能的 Node.js 模块，然后在应用级别或路由级别将其加载到你的应用中。

以下示例说明了安装和加载 cookie 解析中间件函数 `cookie-parser`。

```console
$ npm install cookie-parser
const express = require('express')
const app = express()
const cookieParser = require('cookie-parser')

// load the cookie-parsing middleware
app.use(cookieParser())
```

#### 16-4 获取请求参数

模拟post请求，请求参数可以是username=ker&password=123或者json格式

![image-20230903232901186](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230903232901186.png)

#### 16-5 通过express托管静态文件

通过express内置的express.static可以方便地托管静态文件，例如图片、CSS、JavaScript文件等。

将静态资源文件所在目录作为参数传递给express,static中间件就可以提供静态资源文件的访问了，例如假设在puublic目录放置了图片、CSS和javaScript文件，就可以：

```js
app.use(express.static('public'))
```

现在public目录下面的文件就可以访问了。

```js
http://localhost:3000/image/iken.jpg
http://localhost:3000/js/map.js
http://localhost:3000/css/fr.css
http://localhost:3000/hello.html
```

[^所有文件都是相对于存放目录的，因此，存放静态文件的目录名不会出现在URL中]: 

如果静态资源文件存放在多个目录下，则可以多次调用express.static中间件：

```js
app.use(express.static('public'))
app.use(express.static('stijk'))
```

如果希望所有通过express.static访问的文件都存放在一个虚拟的目录下面，可以通过为静态资源目录指定一个挂载路径的方式来实现，例如：

```js
app.use('/static',express.static('public'))
```

现在public目录下面的文件就可以访问了。

```js
http://localhost:3000/static/image/iken.jpg
http://localhost:3000/static/js/map.js
http://localhost:3000/static/css/fr.css
http://localhost:3000/static/hello.html
```

示例：测试login.html页面的get和post请求

```js
//loginRouter.js
const express = require("express");
const loginRouter = express.Router();
//路由级别--响应前端get请求
loginRouter.get("/", (req, res) => {
    console.log(req.query);//{ username: 'kerwin', password: '123456' }
    res.send("login-success");
})
//路由级别--响应前端post请求
loginRouter.post("/", (req, res) => {
    const { username, password } = req.body;
    if (username === "ker" && password === "123") {
        res.send({ "ok": 1 });
    } else {
        res.send({ "ok": 0 });
    }
    //console.log(req.body);//必须配置中间件 //{ username: 'postman', password: '123456' }
    
})
module.exports = loginRouter;
```

```html
//login.html
<body>
    <div>
        <div>
            用户名：
            <input type="text" id="username">
        </div>
        <div>
            密码：
            <input type="password" id="password">
        </div>
        <div>
            <button id="login">登录--get</button>
            <button id="loginpost">登录--post</button>
        </div>
    </div>
    <script>
        var ologin = document.querySelector("#login");
        var plogin = document.querySelector("#loginpost");
        var username = document.querySelector("#username");
        var password = document.querySelector("#password");
        //get请求
        ologin.addEventListener("click", () => {
            fetch(`/login?username=${username.value}&password=${password.value}`).then(
                res => res.text()).then(res => {
                    console.log(res);
                })
        })
        //get请求
        plogin.addEventListener("click", () => {
            fetch(`/login`, {
                method: "POST",
                body: JSON.stringify({
                    username: username.value,
                    password: password.value
                }),
                headers: {
                    "Content-Type": "application/json"
                }
            }).then(res => res.json()).then(res => {
                console.log(res);
                if(res.ok===1){
                    location.href="/home.html";
                }else{
                    console.log("用户名与密码不匹配");
                }
            })
        })
    </script>
</body>
```

![image-20230904113037912](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904113037912.png)

#### 16-6 服务端渲染(模板引擎)

1.服务器渲染，后端嵌套模板，后端渲染模板，SSR(后端把页面组装)，对于爬虫和搜索引擎友好

-  做好静态页面，动态效果。
- 把前端代码提供给后端，后端要把静态html以及里面的假数据给删掉，通过模板进行动态生成html的内容。

![image-20230904110933751](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904110933751.png)

2.前后端分离，BSR(前端中组装页面)    **客户端渲染 **  对于爬虫和搜索引擎不友好

-  做好静态页面，动态效果。
- json模拟，ajax，动态创建页面。 
- 真实接口数据，前后联调。
- 把前端提供给后端静态资源文件夹。

```js
将/home/list获取的数据通过前端渲染方式渲染到home.html页面
//homeRouter.js
const express = require("express");
const homeRouter = express.Router();
//路由级别
homeRouter.get("/", (req, res) => {
    res.send("home");
})
homeRouter.get("/list", (req, res) => {
    res.send(["111","222","333"]);
})
```

```html
//home.html
<body>
    home
    <ul class="list"></ul>
    <script>
        fetch("/home/list").then(res=>res.json()).then(res=>{
            console.log(res);
            render(res);
        })
        function render(data){
            var list=data.map(item=>`<li>${item}</li>`);
            console.log(list.join(""));//<li>111</li><li>222</li><li>333</li>
            var oul=document.querySelector("ul");
            oul.innerHTML=list.join("");
        }
    </script>
</body>
```

```js
npm i ejs
```

需要在应用中进行如下设置才能让Express渲染模板文件:
·views,放模板文件的目录，比如:**app.set("views", "./views");**

·viewengine,模板引擎，**app.set("view engine", "ejs");**

![image-20230904210115456](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904210115456.png)

**<%= %>与<%- %>区别**

![image-20230904210632617](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904210632617.png)

![image-20230904210643735](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904210643735.png)

**标签注释**，<%#%>不会占用源代码空间

<img src="C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904210917283.png" alt="image-20230904210917283" style="zoom:100%;" />

![image-20230904211035988](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904211035988.png)

**导入公共头部**

![image-20230904211613771](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904211613771.png)

![image-20230904211641297](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904211641297.png)

![image-20230904211658181](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904211658181.png)

**实际应用：网页头部信息若有一些页面头部信息不一样，可以采用一下解决方法：**

![image-20230904212327956](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904212327956.png)

![image-20230904212446128](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904212446128.png)

![image-20230904212510851](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904212510851.png)

**服务端渲染示例--GET**  **通过ejs模块渲染ejs文件到前端**

<%=title%> 与后端数据传参

```ejs
//login.ejs
<body>
    login.ejs
    <h1>推荐-<%=title%>
    </h1>
    <form action="/login/validate" method="GET">
        <div>
            用户名：
            <input type="text" name="username">
        </div>
        <div>
            密码
            <input type="password" name="password">
        </div>
        <div>
            <input type="submit" value="登录">
        </div>
    </form>
</body>
```

```js
//loginRouter.js
const express = require("express");
const loginRouter = express.Router();
//路由级别--响应前端get请求
loginRouter.get("/", (req, res) => {
    res.render("login",{title:"1111"});//找views文件夹下的login.ejs  模板
})
```

![image-20230904170650525](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904170650525.png)

![image-20230904170615533](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904170615533.png)

**服务端渲染示例--POST**

```js
//loginRouter.js
const express = require("express");
const loginRouter = express.Router();
//路由级别--响应前端get请求
loginRouter.get("/", (req, res) => {
    // console.log(req.query);//{ username: 'kerwin', password: '123456' }
    // res.send("login-success");
    // res.send("<b>data</b>");片段&json
    // res.json([1,2,3]);json
    res.render("login", { error: "",isShow:false });//找views文件夹下的login.ejs  模板
    //res.render("login", { isShow: false });
})
//路由级别--响应前端post请求
loginRouter.post("/", (req, res) => {
    console.log(req.body);//{ username: 'ker', password: '123' }
    const { username, password } = req.body;
    if (username === "ker" && password === "123") {
        //res.send({ "ok": 1 });
        console.log("登录成功");
        //重定向
        res.redirect("/home");
    } else {
       // res.send({ "ok": 0 });
        console.log("登录失败");
        res.render("login", { error: "用户名和密码不匹配" ,isShow:true });
       // res.render("login", { isShow: true });
    }
})
```

```ejs
//login.ejs
<body>
    login.ejs
    </h1>
    <form action="/login" method="POST">
        <div>
            用户名：
            <input type="text" name="username">
        </div>
        <div>
            密码
            <input type="password" name="password">
        </div>
        <div>
            <input type="submit" value="登录">
        </div>
    </form>
    <p><%=error %></p>
    <p><%=isShow?'用户名和密码不匹配错误':'' %></p>   
</body>
```

![image-20230904205510213](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904205510213.png)

![image-20230904205550264](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904205550264.png)

**通过ejs渲染html文件到前端**（修改参数即可）

<img src="C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904213919711.png" alt="image-20230904213919711" style="zoom:100%;" />

![image-20230905215930942](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230905215930942.png)

#### 16-7 Express 应用生成器

使用应用生成器工具 `express-generator` 快速创建应用骨架

对于较早的 Node 版本，将应用生成器安装为全局 npm 包，然后启动它：

```console
$ npm install -g express-generator
$ express
```

显示带有 `-h` 选项的命令选项：

```console
$ express -h
```

例如，以下创建一个名为 myapp 的 Express 应用。 该应用将在当前工作目录中名为 myapp 的文件夹中创建，并且视图引擎将设置为 [Pug](https://pug.nodejs.cn/)：

```console
$ express --view=pug myapp
```

然后安装依赖：

```console
$ cd myapp
$ npm install
```

启动项目

```console
$ npm start
//或者
$ node ./bin/www
$ npx nodemon start
```

#### 16-6 express中的方法

##### express.json([options])

这是 Express 中内置的中间件函数。 它使用 JSON 有效负载解析传入请求，并且基于 [body-parser](https://express.nodejs.cn/resources/middleware/body-parser.html)。

返回仅解析 JSON 并且仅查看 `Content-Type` 标头与 `type` 选项匹配的请求的中间件。

```js
app.use(express.json());//post参数为json格式
```

##### express.Router([options])

创建一个新的 [router](https://express.nodejs.cn/en/5x/api.html#router) 对象。

```javascript
const router = express.Router([options])
```

##### express.urlencoded([options])

这是 Express 中内置的中间件函数。 它使用 urlencoded 有效负载解析传入的请求，并且基于 [body-parser](https://express.nodejs.cn/resources/middleware/body-parser.html)。

返回仅解析 urlencoded 正文并仅查看 `Content-Type` 标头与 `type` 选项匹配的请求的中间件。

```js
app.use(express.urlencoded({extended:false}))
//响应form 表单格式post参数 - username=ker&password=123
```

#### 16-7 重要方法

#### (1）app.get(path, callback [, callback ...])

  使用指定的回调函数将 HTTP GET 请求路由到指定路径。你可以提供多个回调函数，其行为类似于中间件，只是这些回调可以调用 `next('route')` 以绕过剩余的路由回调。

####  (2)   res.send([body])

发送 HTTP 响应,相当于封装了res.write()和res.end()请求。可以渲染片段或是json

`body` 参数可以是 `Buffer` 对象、`String`、对象、`Boolean` 或 `Array`。 例如：

```javascript
res.send(Buffer.from('whoop'))
res.send({ some: 'json' })
res.send('<p>some html</p>')
res.status(404).send('Sorry, we cannot find that!')
res.status(500).send({ error: 'something blew up' })
```

此方法对简单的非流式响应执行许多有用的任务： 例如，它**自动分配 `Content-Length` HTTP 响应头字段**（除非之前定义）并提供自动 HEAD 和 HTTP 缓存新鲜度支持。

#### (3)res.render(view [, locals] [, callback])

渲染 `view` 并将渲染的 HTML 字符串发送到客户端。 只能渲染模板，可选参数：

- `locals`，一个对象，其属性定义视图的局部变量。
- `callback`，回调函数。 如果提供，该方法将返回可能的错误和渲染的字符串，但不执行自动响应。 当发生错误时，该方法在内部调用 `next(err)`。

```javascript
// send the rendered view to the client
res.render('index')

// if a callback is specified, the rendered HTML string has to be sent explicitly
res.render('index', (err, html) => {
  res.send(html)
})
```

#### （4）res.json([body])

发送 JSON 响应。 此方法发送一个响应（具有正确的内容类型），该响应是使用 [JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) 转换为 JSON 字符串的参数。

参数可以是任何 JSON 类型，包括对象、数组、字符串、布尔值、数字或 null，你也可以使用它来将其他值转换为 JSON。

```javascript
res.json(null)
res.json({ user: 'tobi' })
res.status(500).json({ error: 'message' })
```

注意区分：

```js
res.send("<b>data</b>");  // 片段&json
res.json([1,2,3]);        //json
res.render("login");      // 找views文件夹下的login.ejs  模板
```

#### （5）res.redirect([status,] path)

重定向到从指定 `path` 派生的 URL，指定 `status`，一个对应于 [HTTP 状态码](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) 的正整数。 如果未指定，则 `status` 默认为 “302 找到”。

```javascript
res.redirect('/foo/bar')
res.redirect('http://example.com')
res.redirect(301, 'http://example.com')
res.redirect('../login')
```

重定向可以是用于重定向到不同站点的完全限定 URL：

```javascript
res.redirect('http://google.com')
```

重定向可以相对于主机名的根目录。 例如，如果应用位于 `http://example.com/admin/post/new` 上，则以下内容将重定向到 URL `http://example.com/admin`：

```javascript
res.redirect('/admin')
```

重定向可以相对于当前 URL。 例如，从 `http://example.com/blog/admin/`（注意尾部斜杠）开始，以下内容将重定向到 URL `http://example.com/blog/admin/post/new`。

```javascript
res.redirect('post/new')
```

#### （6）res.cookie(name, value [, options])

将 cookie `name` 设置为 `value`。 `value` 参数可以是字符串或转换为 JSON 的对象。

![image-20230904233021186](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230904233021186.png)

#### （7）req.file

获取文件对象

![image-20230909114700457](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230909114700457.png)



## 17. MongoDB 数据库

#### 1.关系型与非关系型数据库

  **关系型数据库与非关系型数据库的区别**

#####        （1）关系型数据库特点:

- sql语句增删改查操作
- 保持事务的一致性，事物机制(回滚)     mysql,sqiserver,db2,oracle

#####         （2）非关系型数据库特点:

- no sqi:not only sql;
- 轻量，高效自由。    mongodb,Hbase,Redis

**为啥喜欢mongodb?**
        由于MongoDB独特的数据处理方式，可以将热点数据加载到内存。故而对查询来讲，会非常快(当然也会非常消耗内存);同时由于**采用了BSON的方式存储数据**，即二进制的json格式
        故而**对JSON格式数据具有非常好的支持性**以及友好的表结构修改性，文档式的存储方式，数据友好可见;
数据库的分片集群负载具有非常好的扩展性以及非常不错的自动故障转移。

|   SQL术语   | MongoDB术语 | 解释                                  |
| :---------: | ----------- | ------------------------------------- |
|  database   | database    | 数据库                                |
|    table    | collection  | 数据库表/集合                         |
|     row     | document    | 数据记录行/文档                       |
|   column    | field       | 数据字段/域                           |
|    index    | index       | 索引                                  |
| table joins |             | 表连接,MongoDB不支持                  |
| primary key | primary key | 主键，MongoDB自动符，id字段设置为主键 |

#### 2.安装数据库

https://www.mongodb.com/try/download/community

#### 3.启动数据库

```js
mongod  --dbpath + 数据库位置

eg:mongod  --dbpath D:\MyApp\Mongodb\Server\data\db

**启动 MongoDB 命令**为：net start MongoDB

**关闭 MongoDB 命令**为：net stop MongoDB

打开cmd输入mongosh即可开启命令行模式
```

https://blog.csdn.net/L145990/article/details/127907658

https://blog.csdn.net/qq_45790877/article/details/129286309

![image-20230905113633765](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230905113633765.png)

MongoDB6.0以后做出了改变，MongoDB6不再默认安装shell工具----Mongosh。

添加两个环境变量：安装目录下的bin文件夹路径以及mongosh-shell的bin目录的路径。

![image-20230905114633092](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230905114633092.png)

![image-20230905114840293](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230905114840293.png)

#### 4.在命令行中操作数据库

| 功能                     | 命令                                                   |
| ------------------------ | ------------------------------------------------------ |
| help查看命令提示         | help、db.help()、db.test.help()、db.test.find().help() |
| 创建/切换数据库          | use music_test                                         |
| 查询数据库               | show dbs                                               |
| 查看当前使用的数据库     | db、db.getName()                                       |
| 显示当前DB状态           | db.stats()                                             |
| 查看当前DB版本           | db.version()                                           |
| 查看当前DB的链接机器地址 | db.getMongo()                                          |
| 删除数据库               | db.dropDatabase()                                      |

| 集合操作功能             | 命令                                                         |
| ------------------------ | ------------------------------------------------------------ |
| 创建一个聚集集合         | db.createCollection("colName",{size:5242880,capped:true,max:5000})最大存储空间为5m,最多5000个文档的集合 |
| 得到指定名称的聚集集合   | db.getCollection("account")                                  |
| 得到当前db的所有聚集集合 | db.getCollectionNames()                                      |
| 显示当前db所有聚集的状态 | db.printCollectionStatus()                                   |
| 删除                     | db.users.drop()                                              |

![image-20230905144006798](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230905144006798.png)

##### 添加

- save()：如果 _id 主键存在则更新数据，如果不存在就插入数据。该方法新版本中已废弃，可以使用 **db.collection.insertOne()** 或 **db.collection.replaceOne()** 来代替。

- insert(): 若插入的数据主键已经存在，则会抛 **org.springframework.dao.DuplicateKeyException** 异常，提示主键重复，不保存当前数据

- **3.2 版本之后新增了 db.collection.insertOne() 和 db.collection.insertMany()。**

  db.collection.insertOne() 用于向集合插入一个新文档，db.collection.insertMany() 用于向集合插入一个多个文档。

```markdown
db.users.insert({name:'zhangsan',age:25,sex:true});
db.users.insert([{name:'zhangsan',age:25,sex:true},{name:"kerwin",age:100}]);
```

![image-20230905170701160](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230905170701160.png)



##### 修改

update() 方法用于更新已存在的文档。语法格式如下：

https://blog.51cto.com/u_16099241/6398576

```
db.collection.update(
   <query>,
   <update>,
   {
     upsert: <boolean>,
     multi: <boolean>,
     writeConcern: <document>
   }
)
```

**参数说明：**

- **query** : update的查询条件，类似sql update查询内where后面的。
- **update** : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
- **upsert** : 可选，这个参数的意思是，**如果不存在update的记录，是否插入objNew**,true为插入，默认是false，不插入。
- **multi** : 可选，mongodb **默认是false,只更新找到的第一条记录**，如果这个参数为true,就把按条件查出来多条**记录全部更新**。
- **writeConcern** :可选，抛出异常的级别。

```markdown
db.users.update({age:25},{$set:{name:'zhangsan'}},false,true});
相当于：update users set name='zhangsan' where age=25;
db.users.update({name:'Lisi'},{$inc:{age:50}},false,true});
相当于：update users set age=age+50 where name='Lisi';
#存在问题，只能更新第一个记录
db.users.update({name:'Lisi'},{$inc:{age:50},$set:{name:'zhangsan'}},false,true);
相当于：update users set age=age+50 name='zhangsan' where name='Lisi';

$unset
用法：{$unset:{field:1}}
作用：删除某个字段field

$push
用法：{$push:{field:value}}
作用：把value追加到field里。

 $addToSet
用法：{$addToSet:{field:value}}
作用：加一个值到数组内，而且只有当这个值在数组中不存在时才增加。

$pop
用法：删除数组内第一个值：{$pop:{field:-1}}、
删除数组内最后一个值：{$pop:{field:1}}

$pull
用法：{$pull:{field:_value}}
作用：从数组field内删除一个等于_value的值

$pullAll
用法：{$pullAll:value_array}
作用：用法同$pull一样，可以一次性删除数组内的多个值。

$rename
用法：{$rename:{old_field_name:new_field_name}}
作用：对字段进行重命名
```

![image-20230905171807350](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230905171807350.png)

![image-20230905171825574](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230905171825574.png)

![image-20230905171835752](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230905171835752.png)

##### 删除

```markdown
db.users.remove({age:132});
删除所有db.users.remove({})
```

![image-20230905171248413](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230905171248413.png)

##### 查询

| 查询功能                                                     | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 查询所有记录                                                 | db.users.find()                                              |
| 查询某字段去重后的数据                                       | db.users.distinct("name")                                    |
| 查询age=22的记录                                             | db.users.find({"age":22})                                    |
| 查询age>22的记录                                             | db.users.find({age:{$gt:22}})                                |
| 查询age<22的记录                                             | db.users.find({age:{$lt:22}})                                |
| 查询age>=22的记录                                            | db.users.find({age:{$gte:22}})                               |
| 查询age<=22的记录                                            | db.users.find({age:{$lte:22}})                               |
| 查询age>=22的记录并且age<=26                                 | db.users.find({age:{$gte:22,$lte:26}})                       |
| 查询name中包含mongo的数据                                    | db.users.find({name:/mongo/})                                |
| 查询name中以mongo开头的                                      | db.users.find({name:/^mongo/})                               |
| 查询指定列name、age数据（想显示哪列，就将字段设置为1 ，不想显示设置为0） | db.users.find({},{name:1,age:1})                             |
| 查询指定列name、age数据，age>25                              | db.users.find({age:{$gt:25}},{name:1,age:1})                 |
| 按照年龄排序（写成数组就是多列查询）                         | 升序db.users.find().sort({age:1})   降序db.users.find().sort({age:-1}) |
| 查询name=zhangsan,age=22的数据                               | db.users.find({name:'zhangsan',age:22})                      |
| 查询前5条数据                                                | db.users.find().limit(5)                                     |
| 降序排序age并返回该列                                        | db.users.find({},{age:1}).sort({age:-1})                     |
| 查询10条以后数据                                             | db.users.find().skip(10)                                     |
| 查询5-10条之间的数据                                         | db.users.find().skip(5).limit(5)                             |
| or与查询                                                     | db.users.find({$or:[{age:22},{age:25}]})                     |
| 查询第一条数据                                               | db.users.findOne()                                           |
| 查询某个结果集的记录数                                       | db.users.find({age:{$gte:25}}).count()                       |
| 根据需求若数据量过大，则需要懒加载数据                       | db.users.find().skip((pagenum-1)*num).limit(num),pagenum是页数，num是要几行显示 |

![image-20230905212708425](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230905212708425.png)

![image-20230905213344751](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230905213344751.png)

#### 5.安装MongoDB可视化工具RoboMongo

https://blog.csdn.net/Smart_11/article/details/130151813

https://robomongo.org/

#### 6.连接MongoDB数据库

**安装命令：npm -i mongoose**

##### 步骤

（1）创建连接

```js
//连接数据库
const mongoose = require("mongoose");
mongoose.connect("mongodb://127.0.0.1:27017/xy_project");
//插入集合和数据，数据库xy_project会自动创建
```

（2）创建模型

```js
//UserModel.js
const mongoose = require("mongoose");
const Schema = mongoose.Schema;
const UserType = {
    username: String,
    password: String,
    age:Number
}
const UserModel = mongoose.model("user",new mongoose.Schema(UserType));
//模型user将会对应到users集合
module.exports = UserModel;
```

（3）插入数据

```js
//user.js
const UserModel = require('../model/userModel');
router.post('/user/add', function (req, res) {
  console.log(req.body);//{ username: 'ww', password: '123', age: '11' }
  //插入数据库
  //1.创建模型(user,限制field类型)，一一对应数据库集合(users)
  const { username, password, age } = req.body
  UserModel.create({
    username, password, age
  }).then(data => {
    console.log(data);
    res.send({ "ok": 1 });
  });
})
```

![image-20230906223208053](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230906223208053.png)

#### 7.mongoose.model模块的方法

https://www.jianshu.com/p/4c2261e2d7ff

##### （1）create

> Model.create(doc(s),[callback])

- 含义：用来创建一个或者多个文档并添加到数据库当中。

- 参数：
   第一个参数doc(s) ，后面的s代表是复数多个的意思，证明这个位置可以传一个文档对象，也可以传多个文档对象的数组。
   第二个参数[callback]，这个位置返回的是一个回调函数，当操作完成后，调用该函数。

  ```js
  stuModel.create([], err => {
      if (!err) {
          console.log("文档插入成功")
      }
  })
  ```

##### （2）find

```
Model.find(conditions, [projection], [options], [callback])
```

- 查询所有符合条件的文档，总会返回一个数组。
- 参数：
   第一个参数conditions：查询的条件。
   第二个参数[projection]：投影，需要获取到的字段，即你想要显示多少个字段，是全部显示呢？还是过滤掉一些字段（属性）。
   第三个参数[options]： 查询的选项（例如常用的skip和limit）。
   第四个参数[callback]（必选）： 回调函数，查询结果会通过回调函数返回，如果不传回调函数，压根不会查询。

```js
stuModel.find({name: "小红"}, (err, docs) => {
    if (!err) {
        console.log(docs)
    }
})
```

<img src="https://upload-images.jianshu.io/upload_images/19781462-fc884f07367c0dd4.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp" alt="img" style="zoom:80%;" />

- 如果第一个参数的查询条件为一个**空对象**（什么都不指定），即默认查询所有文档。


![img](https://upload-images.jianshu.io/upload_images/19781462-e4e3be04a821a33e.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp)

- 第二个参数[projection]的使用，规定显示要查询的字段（属性），将其他的字段过滤掉，它有2种传递方式，一种是**传统的对象**形式传递，另一种是**字符串**传递形式。

![img](https://upload-images.jianshu.io/upload_images/19781462-cb432cb1dd29fdfb.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp)

node环境执行代码结果：**返回数组**。

![img](https://upload-images.jianshu.io/upload_images/19781462-28719a6d04d67833.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp)

- 第二个参数[projection]的使用不一定需要写成对象的形式，它还可以使用字符串的写法，**返回数组**。


![img](https://upload-images.jianshu.io/upload_images/19781462-ba2db2d045d6e671.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp)

- 第三个参数[options]： 查询选项的使用。


![img](https://upload-images.jianshu.io/upload_images/19781462-569bbc6eed763913.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp)

**findOne方法返回的是一个对象，find()方法返回的是一个数组。**

##### （3）delete

```js
Model.deleteOne(conditions, [callback])  //删除一个

Model.deleteMany(conditions, [callback]) //删除多个
```

##### （4）update

```
Model.update(conditions, doc, [options], [callback])
```

- 用来修改一个或者多个文档。
- 参数：
   conditions：查询条件
   doc: 修改后的文档对象
   options: 配置参数选项
   callback: 回调函数

```js
Model.updateOne(conditions, doc, [options], [callback])  //更新一个
Model.updateMany(conditions, doc, [options], [callback])  //更新多个
```



## 18. 接口规范与业务分层

#### 1.接口规范

#### RESTful架构

服务器上每一种资源，比如一个文件，一张图片，一部电影，都有对应的ur地址，如果我们的客户端需要对服务器上的这个资源进行操作，就需要通过http协议执行相应的动作来操作它，比如进行获取，更新，删除。

简单来说就是**url地址中只包含名词表示资源，使用http动词表示动作进行操作资源**。

举个例子:左边是错误的设计，而右边是正确的

![image-20230906224550648](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230906224550648.png)

##### 使用方式

```powershell
GET http://localhost:3000/api/user  #获取列表
POST http://localhost:3000/api/user  #创建用户
PUT http://localhost:3000/api/user/{id} #修改用户信息
DELETE http://localhost:3000/api/user/{id} #删除用户信息
```

##### 过滤信息

用于补充规范一些通用字段

```powershell
?limit=10              #指定返回课录的数量
?offset=10             #指定返回记录的开始位置
?page=2&per_page=100   #指定第几页，以及每页的记录数
?sortby=name&order=asc #指定返回结果按照哪个属性排序，以及排序顺序
?state=close           #指定筛选条件
```

#### 2.业务分层

  **MVC是三个单词的首字母缩写，它们是Model（模型）、View（视图）和Controller（控制）。**

routerjs:  负责将请求分发给C层
controllerjs:  C层负责处理业务逻辑(V与M之间的沟通)
views:V层:  负责展示页面
model:M层:  负责处理数据(增删改查)

![image-20230906230716734](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230906230716734.png)

![image-20230906231118194](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230906231118194.png)

## 19. 登录鉴权

#### 登录页面：

#### 1.cookie与session

「HTTP无状态」我们知道，HTTP是无状态的，也就是说，HTTP请求方和响应方间无法维护状态，都是一次性的，它不知道前后的请求都发生了什么。但有的场景下，我们需要维护状态。最典型的，一个用户登陆微博，发布、关注、评论，都应是在登录后的用户状态下的。「标记」那解决办法是什么呢?

<u>cookie 前端可以随意伪造，服务端只要看前端有没有cookie，不用校验就返回数据出去，一旦cookie被盗窃，后端是无法发觉的，无法强制下线或者取消的，单独的cookie无法实现服务端注销。</u>

> 1. 通过cookie将数据保存在在客户端中，也就是在浏览器 。这种形式的特点是轻量级，容易实现也容易复制，因为cookie是保存在客户端，你可以拷贝cookie骗过服务器来实现登录验证，很多爬虫也就是利用cookie来模拟登录状态。所以这种完全交给用户来保管关键数据的方式逐渐被后面一种形式取代。
> 2. 将数据以session的形式保存在服务端，通过cookie返回给客户端session identifier存储在客户端。也就是客户端只有钥匙，信息都是在服务器上，服务器可以更安全的验证用户。当然没有绝对的安全，毕竟钥匙也能伪造的嘛，只是相对于cookie来说，session的安全性更高。但session也有本身的问题，当用户数据变得庞大，势必会对服务器的数据储存和读取产生压力。

![image-20230907204936211](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230907204936211.png)

**cookie与session的区别：cookie是存在客户端，尔session是存在服务端。cookie值相当于打开session库的一把钥匙。**

##### **什么是cookie**

cookie是一种客户端的状态管理技术。

当浏览器向服务器发送请求时，服务器会将少量的数据以set-cookie消息头的方式发送给浏览器

浏览器会将这些数据保存下来。当浏览器再次访问服务器时，会将这些数据以cookie消息头的方式发送给服务器。

##### **什么是session**

session是一种服务器端的状态管理技术。

当浏览器访问服务器时，服务器创建一个session对象(该对象有一个唯一的id号，称之为sessionId),服务器在默认情况下，会将sessionId以cookie的方式(set-cookie消息头)发送给浏览器,浏览器会将sessionId保存到内存。当浏览器再次访问服务器时，会将sessionId发送给服务器，服务器依据sessionId就可找到之前创建的session对象。

- *cookie失效，cookie丢失就无法访问页面，但是如果接口没有设置判断session语句，接口仍然可以使用，这时候就需要写一个中间件来解决接口等问题了。*

- 当不断在这个页面工作时，cookie若设置时间是1h，那么当一个小时到了之后会自动退出页面，当在1h中反复在这个页面工作，此时应该重新计时cookie过期时间。

- **ajax发起后端请求重定向redirect，后端不会重定向的。但是前端location.href是可以重定向的**

- session是保存在服务器内存中的，一旦刷新页面session就会丢，此时就需要重新登录，所以需要将session存入数据库中

- 同一个账号在不同的浏览器登录时会生成不同的cookie和session

- 当登录了a.com网站后，页面叉掉登录b.com,b.com网站有一个链接http://a.com?from=ee&to=tf，当点击该链接时，此时不要登录a.com网站就能拿到数据，说明此时的cookie自动带到该链接，所以会有安全性问题。（CSRF攻击）

#### 2.express-session模块

安装命令：npm i  express-session

**express-session最基础需要的参数如下**
name： 设置session存储时的名字,即cookie中的key值
secret ：服务器生成session的签名,也就是加密时用的密钥
resave ：boolean,是否将过期时间重新计算(也就是重新设置session后，会重新计算session过期时间)
saveUninitialized ：为true时，强制初始化一个session存储,该session存储是无效的
cookie： cookie对象,里面可以设置maxAge等参数
maxAge ：设置最大过期时间，1000相当于1s

rolling:true,为true表示超时前刷新，cookie会重新计时，为false表示在超时前刷新多少次都按照第一次刷新开始计算时间。

store: session 的存储方式，默认存放在内存中，也可以使用 redis，mongodb 等。

示例：

![image-20230907220928498](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230907220928498.png)

**设置session值**

![image-20230908203948013](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230908203948013.png)

**摧毁session库**

![image-20230908204126904](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230908204126904.png)

**connect-mongo模块**

将session数据存入数据库中

![image-20230908210003033](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230908210003033.png)

##### 通过cookie-session校验示例：

```js
//app.js
//引入session
var session = require("express-session");
var MongoStore = require("connect-mongo");
app.use(session({
  name: "kerwinsysytem",
  secret: "dwad4455544dwad",
  cookie: {
    maxAge: 1000 * 60 * 60,
    secure:false
  },
  resave: true,
  saveUninitialized: true,
  store: MongoStore.create({
    mongoUrl: 'mongodb://127.0.0.1:27017/xy_session',//新建一个数据库存放session
    ttl:1000*60*60  //过期时间,即是将session从数据库移除的时间
  })
}))

//设置中间件，session过期校验
app.use((req, res, next) => {
  //排除login相关的路由和接口，不然会一直重定向
  if (req.url.includes("login")) {
    next();
    return //不走后面语句
  }
  if (req.session.user) {
    //重新设置session，使得resave为true时，会重新计算过期时间
    req.session.date = Date.now();
    next();//放行
  } else {
    //是接口就返回错误码，根据错误码的值在前端页面设置location.href重定向
    //不是接口，就重定向。
    req.url.includes("api")
      ? res.status(401).json({ s: 0 }) : res.redirect("/login");
  }
})
```

```js
//UserController.js
 login: async (req, res) => {
        const { username, password } = req.body;
        const data = await UserService.login(username, password);//data为一个数组
        console.log(data);//[{_id: new ObjectId("64f881e9611578c9d3cc73cd"),username: 'admin',password: '123',age: 12,__v: 0}]
        if (data.length === 0) { //长度为0 表示查找失败，没有该用户信息
            res.send({ ok: 0 });
        } else {
            //设置session={} 不同浏览器或者电脑设置  req.session是不一样的，是自动匹配cookie生成的对象
            req.session.user = data[0];//设置session对象，放一些东西在对象里，也可以是布尔值
           //默认存在内存中，一保存就会丢，需要保存在数据库中
            res.send({ ok: 1 });
        }
    },
    logout: (req, res) => {
        req.session.destroy(() => { //相当于摧毁了session库
            res.send({ ok: 1 });
        })
    }
```

![image-20230908221814387](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230908221814387.png)
![image-20230908221850753](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230908221850753.png)



#### 3.JSON Web Token(JWT)

![image-20230908210953365](D:\typora_photo\image-20230908210953365.png)

![image-20230908212617273](D:\typora_photo\image-20230908212617273.png)

当然，如果一个人的token被别人偷走了，那我也没办法，我也会认为小偷就是合法用户，这其实和一个人的 sessionid被别人偷定是一样的。

- 这样一来，我就不保存sessionid了，我只是生成token，然后验证token，我用我的CPU计算时间获取了我的 session存储空间!
- 解除了sessionid这个负担，可以说是无事一身轻，我的机器集群现在可以轻松地做水平扩展，用户访问量增大，直接加机器就行。这种无状态的感觉实在是太好了!

**缺点:**

- 1.占带宽，正常情况下要比sessionid更大，需要消耗更多流量，挤占更多带宽，假如你的网站每月有10万次的浏览器，就意味着要多开销几十兆的流量。听起来并不多，但日积月累也是不小一笔开销。实际上，许多人会在JWT中存储的信息会更多;

- 2.无法在服务端注销，那么久很难解决劫持问题;

- 3.性能问题，JWT的卖点之一就是加密签名，由于这个特性，接收方得以验证JWT是否有效且被信任。对

  于有着严格性能要求的Web应用，这并不理想，尤其对于单线程环境。 

```
注意:
CSRF攻击的原因是浏览器会自动带上cookie，而不会带上token; 
以CSRF攻击为例:
cookie:用户点击了链接，cookie未失效，导致发起请求后后端以为是用户正常操作，于是进行扣款操作; token:用户点击链接，由于浏览器不会自动带上token，所以即使发了请求，后端的token验证不会通过，所以不会进行扣款操作;
```

**JWT比较适用于前后端分离。**

##### 生成token

```js
var jwt = require("jsonwebtoken");
var token=jwt.sign({
  data: 'kerwin'
}, 'anydata', { expiresIn: 10000 });//"120" is equal to "120ms"
//支持时间写法 60, "2 days", "10h", "7d"
console.log(token);
//eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjoia2Vyd2luIiwiaWF0IjoxNjk0MTgwOTY1LCJleHAiOjE2OTQxOTA5NjV9.P0Zr6G3l6xbjjLGnivz5AVZswNphYD3xIJyuSxq-bkE
```

##### 校验token

```js
jwt.verify(token, secretOrPublicKey, [options, callback])
```

##### 引入axios模块

拦截器有助于在请求前与请求成功后优先执行某些方法，利于设置token。

https://www.npmjs.com/package/axios

![image-20230908230838828](D:\typora_photo\image-20230908230838828.png)

##### axios使用

html页面引入：

<script src="https://cdn.jsdelivr.net/npm/axios@1.1.2/dist/axios.min.js"></script>

使用语法：

![image-20230909093828919](D:\typora_photo\image-20230909093828919.png)

```js
axios.post("/api/login", {
    username: username.value,
    password: password.value
    }).then(res => {
    console.log(res.data);
    if (res.data.ok === 1) {
        location.href = "/";
    } else {
        alert("用户名和密码不准确");
    }
     //res.data 后端返回响应体
     //res.hrader 后端返回响应头
})

axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  })
  .finally(function () {
    // always executed
  });
```

## 20、文件上传

在前端form表单中，默认接收enctype="application/x-www-form-urlencoded"，后端可以接收到前端的数据，但是一般进行文件传输会将enctype换成enctype="multipart/form-data"多部分数据传输，后端是接收不了的。因为后端只接收json或者application/x-www-form-urlencoded格式。

#### 1.multer模块

Multer 是一个 node.js 中间件，用于处理 `multipart/form-data` 类型的表单数据，它主要用于上传文件。它是写在 [busboy](https://github.com/mscdex/busboy) 之上非常高效。

```js
安装： npm i multer
```

Multer向请求对象添加一个body对象和一个或多个文件对象。body对象包含表单文本字段的值，file或files对象包含通过表单上传的文件。前提是enctype="multipart/form-data。

```html
<form action="/profile" method="post" enctype="multipart/form-data">
  <input type="file" name="avatar" />
</form>
```

```js
const express = require('express')
const multer  = require('multer')
const upload = multer({ dest: 'uploads/' })
const app = express()
//只能接收一个文件
app.post('/profile', upload.single('avatar'), function (req, res, next) {
  // req.file 是 `avatar` 文件的信息
  // req.body 将具有文本域数据，如果存在的话
})
//可以接收多个文件，12表示最多12个
app.post('/photos/upload', upload.array('photos', 12), function (req, res, next) {
  // req.files 是 `photos` 文件数组的信息
  // req.body 将具有文本域数据，如果存在的话
})
const cpUpload = upload.fields([{ name: 'avatar', maxCount: 1 }, { name: 'gallery', maxCount: 8 }])
app.post('/cool-profile', cpUpload, function (req, res, next) {
  // req.files 是一个对象 (String -> Array) 键是文件名，值是文件数组
  // 例如：
  //  req.files['avatar'][0] -> File
  //  req.files['gallery'] -> Array
  // req.body 将具有文本域数据，如果存在的话
})
```

如果你需要处理一个只有文本域的表单，你应当使用 `.none()`:

```
const express = require('express')
const app = express()
const multer  = require('multer')
const upload = multer()

app.post('/profile', upload.none(), function (req, res, next) {
  // req.body 包含文本域
})
```

#### 2.使用方法

upload.single(fieldname) :接受名称为fieldname的单个文件。单个文件将存储在req.file中。在form表单中input元素下，filename为input的name属性。

![image-20230909113643564](D:\typora_photo\image-20230909113643564.png)

![image-20230909113631879](D:\typora_photo\image-20230909113631879.png)

#### 3.两种操作方式

##### （1）前后端分离

```ejs
//index.ejs
<body>
  <h2>mongoDB增删改查</h2>
  <h2>后台用户管理业务</h2>
  <button id="exit">退出登录</button>
  <div class="form-group">
    <label for="inputEmail3" class="col-sm-2 control-label">用户名</label>
    <div class="col-sm-10">
      <input type="text" class="form-control" id="username" placeholder="Username">
    </div>
  </div>
  <div class="form-group">
    <label for="inputPassword3" class="col-sm-2 control-label">密码</label>
    <div class="col-sm-10">
      <input type="password" class="form-control" id="password" placeholder="Password">
    </div>
  </div>
  <div class="form-group">
    <label for="inputPassword3" class="col-sm-2 control-label">年龄</label>
    <div class="col-sm-10">
      <input type="password" class="form-control" id="age" placeholder="Age">
    </div>
  </div>
  <div class="form-group">
    <label for="inputPassword3" class="col-sm-2 control-label">头像</label>
    <div class="col-sm-10">
      <input type="file" class="form-control" id="avatar" placeholder="avatar" >
    </div>
  </div>
  <div class="form-group">
    <div class="col-sm-offset-2 col-sm-10">
      <button class="btn btn-default" id="register">添加用户</button>
    </div>
  </div>
  <table class="table table-hover">
    <thead>
      <tr>
        <td>序号</td>
        <td>用户名</td>
        <td>年龄</td>
        <td>操作</td>
        <td>头像</td>
      </tr>
    </thead>
    <tbody></tbody>
  </table>
  <script>
    //axios写法
    var username = document.querySelector("#username");
    var password = document.querySelector("#password");
    var age = document.querySelector("#age");
    var register = document.querySelector("#register");
    var tbody = document.querySelector("tbody");
    var exit = document.querySelector("#exit");
    var avatar=document.querySelector("#avatar");
    register.addEventListener("click", () => {
      console.log(username.value, password.value, age.value,avatar.files[0]);
      //返回一个文件对象
      //添加用户，由于是文件上传所以使用multipart/form-data类型
      const formdata=new FormData();
      formdata.append("username",username.value);
      formdata.append("password",password.value);
      formdata.append("age",age.value);
      formdata.append("avatar",avatar.files[0]);
      axios.post("/api/user", formdata,{
        headers:{
          "Content-Type":"multipart/form-data"
        }
      }).then(res => {
        console.log(res.data);
      })
    })
```

```js
//UserControlller.js
addUser: async (req, res) => { //async 解决异步问题，等添加完成再返回数据
        console.log(req.body,req.file);//{ username: 'ww', password: '123', age: '11' }
        //插入数据
        //1.创建模型(user,限制field类型)，一一对应数据库集合(users)
        //若用户没有选择图片则选取默认的图片存入
        const avatar = req.file?`/uploads/${req.file.filename}`:`/images/2.png`;//拼接路径
        const { username, password, age } = req.body
        await UserService.addUser(username, password, age,avatar);
        res.send({ "ok": 1 });
    }
```

```js
//user.js
/引入Multer
const multer = require('multer')
const upload = multer({ dest: 'public/uploads/' })//在静态资源文件夹下创建一个新文件夹，获取后的文件是一个唯一编码的二进制文件
//增加用户
router.post('/user', upload.single("avatar"),UserController.addUser);
```

```js
 //UserService.js
addUser: (username, password, age,avatar) => {
        return UserModel.create({
            username, password, age,avatar
   })
},
```

![image-20230909172324524](D:\typora_photo\image-20230909172324524.png)

##### （2）后端模板渲染

```ejs
//index.ejs
  <table class="table table-hover">
    <thead>
      <tr>
        <td>序号</td>
        <td>用户名</td>
        <td>年龄</td>
        <td>操作</td>
        <td>头像</td>
      </tr>
    </thead>
    <tbody></tbody>
  </table>

  <script>
    //axios写法
    var username = document.querySelector("#username");
    var password = document.querySelector("#password");
    var age = document.querySelector("#age");
    var register = document.querySelector("#register");
    var tbody = document.querySelector("tbody");
    var exit = document.querySelector("#exit");
    var avatar=document.querySelector("#avatar");
  
    axios.get("/api/user?page=1&limit=10").then(res => {
      res = res.data;
      tbody.innerHTML = res.map(item => `
        <tr>
          <td id="first">${item._id}</td>
        <td>${item.username}</td>
        <td>${item.age}</td>
        <td><button id="update">修改</button>&nbsp;<button id="dele">删除</button></td>
        <td><img src="${item.avatar}"/></td>
      </tr>
   `).join("");
```

```js
//user.js
/引入Multer
const multer = require('multer')
const upload = multer({ dest: 'public/uploads/' })//在静态资源文件夹下创建一个新文件夹，获取后的文件是一个唯一编码的二进制文件
//增加用户
router.get('/user', UserController.getUser);
```

```js
//UserControlller.js
 getUser: async (req, res) => {
        console.log(req.query);//{ page: '1', limit: '2' }
        const { page, limit } = req.query;
        const data=await UserService.getUser(page, limit);
        res.send(data);
    },
```

```js
 //UserService.js
getUser: (page, limit) => {
        return UserModel.find({}, {username: 1, age: 1,avatar:1 }).sort({ age: -1 }).skip((page - 1) * limit).limit(limit);
    },
```

![image-20230909172623933](D:\typora_photo\image-20230909172623933.png)

## 21.APIDOC-API文档生成工具

apidoc是一个简单的RESTfulAPI文档生成工具，它从代码注释中提取特定格式的内容生成文档。支持诸如 Go. JavaC++ Rust等大部分开发语言，具体可使用apidoc1ang命令行查看所有的支持列表。 apidoc拥有以下特点:
1.跨平台，linux、windows、macOS等都支持;2支持语言广泛，即使是不支持，也很方便扩展;
3.支持多个不同语言的多个项目生成一份文档;
4.输出模板可自定义; I 
5.根据文档生成mock数据;

```js
安装命令：npm install -g apidoc
```

**示例：**

在VSCode安装名称: ApiDoc Snippets工具，在页面中输入api会显示选项，选择apiDocumentation选项，生成如下结果：

```js
/**
 * @api {method} /path title
 * @apiName apiName
 * @apiGroup group
 * @apiVersion  major.minor.patch

 * @apiParam  {String} paramName description
 * @apiSuccess (200) {type} name description
 * @apiParamExample  {type} Request-Example:
 * {
 *     property : value
 * }
 * @apiSuccessExample {type} Success-Response:
 * {
 *     property : value
 * }
 */
```

**填充示例：**

```js
/**
 * @api {post} /api/user 添加用户
 * @apiName addUser
 * @apiGroup Usergroup
 * @apiVersion  1.0.0
 * 
 * @apiParam  {String} username 用户名
 * @apiParam  {String} password 密码
 * @apiParam  {Number} age 年龄
 * @apiParam  {File} avatar 头像
 * @apiSuccess (200) {number} ok 标识成功字段
 * 
 * @apiParamExample  {multipart/form-data} Request-Example:
 * {
 *     username : "kerwin",
 *     password:"123",
 *     age:100,
 *     avatar:File
 * }
 * @apiSuccessExample {type} Success-Response:
 * {
 *     ok : 1
 * }
 */
```

##### 生成doc文档命令：

```js
apidoc -i .\routes\ -o .\doc  其中.\routes表示所在文件目录 ，.\doc为生成文件目录
```

##### 其他工具：showdoc

注意：

（1）在当前文件夹下apidoc.json,修改文档一些内容标题，相当于config文件

```js
{
    "name":"后台系统接口文档",
    "version":"1.0.0",
    "description":"关于后台系统的接口文档描述",
    "title":"企业网站定制系统"
}
```

## 22 、Koa2

koa基于Nodejs平台的下一代web 开发框架

#### 1.简介

​          koa是由Express原班人马打造的，致力于成为一个更小、更富有表现力、更健壮的Web框架。使用koa编写  web应用，通过组合不同的generator，可以免除重复繁琐的回调函数嵌套，并极大地提升错误处理的效率。koa不在内核方法中绑定任何中间件，它仅仅提供了一个轻量优雅的函数库，使得编写Web应用变得得心应手。

#### 2.快速开始

##### 2.1安装koa2

```js
//初始化package.json 
npm init
//安装koa2
npm install koa
```

##### 2.2. hello world代码

```js
const Koa = require("koa");
const app = new Koa();
//ctx===content 上下文
app.use((ctx,next) => {
    // ctx.response
    // ctx.request
    ctx.response.body="hello world"
    ctx.response.body = "<b>hello world</b>";
    ctx.response.body = {name:"kerwin"};
})//可以返回代码片段或者json或者字符串
app.listen(3000)
```

**注意：ctx.resopnse.body与res.send()相似，都可以传入代码片段或者json或者字符串。**

##### 2.3 应用上下文（Context）

Koa 的上下文封装了 request 与 response 对象至一个对象中，并提供了一些帮助开发者编写业务逻辑的方法。为了方便，你可以在 `ctx.request` 和 `ctx.response` 中访问到这些方法。

每一个请求都会创建一段上下文。在控制业务逻辑的中间件中，上下文被寄存在 `this` 对象中：

```js
app.use(function *(){
  this; // 上下文对象
  this.request; // Request 对象
  this.response; // Response 对象
});
```

为了使用方便，许多上下文属性和方法都被委托代理到他们的 `ctx.request` 或 `ctx.response`，比如访问 `ctx.type` 和 `ctx.length` 将被代理到 `response` 对象，`ctx.path` 和 `ctx.method` 将被代理到 `request` 对象。

**精简写法： ctx.header=ctx.request.header**

![image-20230909214206339](D:\typora_photo\image-20230909214206339.png)

![image-20230909214217991](D:\typora_photo\image-20230909214217991.png)

- ctx.req: Node.js 中的 request 对象
- ctx.res: Node.js 中的 response 对象，绕过Koa的response处理是不被支持的，应该避免使用以下node属性方法有:
  - res.statusCode
  - res.writeHead()
  - res.write()
  - res.end()

- ctx.request:： Koa的Request对象
- ctx.response：Koa的Response对象

#### 3.koa vs express

通常都会说Koa是洋葱模型，这重点在于中间件的设计。但是按照上面的分析，会发现Express也是类似的，不同的是Express中间件机制使用了Callback实现，这样如果出现异步则可能会使你在执行顺序上感到困惑，因此如果我们想做接口耗时统计、错误处理Koa的这种中间件模式处理起来更方便些。最后一点响应机制也很重要， Koa不是立即响应，是整个中间件处理完成在最外层进行了响应，而Express 则是立即响应。

##### 3.1 更轻量

- koa不提供内置的中间件;

- koa不提供路由，而把路由这个库分离出来了(koa/router)

##### 3.2 Context 对象

koa增加了一个Context的对象，作为这次请求的上下文对象(在koa2中作为中间件的第一个参数传入)。同时 Context上也挂载了Request和Response两个对象。和Express类似，这两个对象都提供了大量的便捷方法辅助开发这样的话对于在保存一些公有的参数的话变得更加合情合理

##### 3.3 异步流程控制

express采用callback来处理异步，koav1采用generator，koav2采用async/await。

 generator和async/await使用同步的写法来处理异步，明显好于callback和promise。

##### 3.4 中间件模型

express基于connect中间件，线性模型;
koa中间件采用洋葱模型(对于每个中间件，在完成了一些事情后，可以非常优雅的将控制权传递给下一个中间件，并能够等待它完成，当后续的中间件完成处理后，控制权又回到了自己)

![img](D:\typora_photo\68747470733a2f2f7261772e6769746875622e636f6d2f66656e676d6b322f6b6f612d67756964652f6d61737465722f6f6e696f6e2e706e67.png)

![image-20230909220528770](D:\typora_photo\image-20230909220528770.png)

###### express-同步

```js
const express = require("express");
const app = express();
app.use((req, res, next) => {
    if(req.url==="/favicon.ico")return
    console.log("1111");
    res.send("hello world");
    next()
    console.log("3333");
})
app.use((req, res, next) => {
    console.log("2222");
})
app.listen(3000)

// 1111
// 2222
// 3333
```

###### express-异步

```js
const express = require("express");
const app = express();
app.use(async(req, res, next) => {
    if(req.url==="/favicon.ico")return
    console.log("1111");
    await next();
    console.log("4444");
    console.log(res.token);
    res.send("hello world");
})
app.use(async(req, res, next) => {
    console.log("2222");
    await delay(1000);
    res.token = "aaaaaaaaaaaa1111111hj";
    console.log("3333");
})
app.listen(3000)
function delay(time) {
    return new Promise((resolve, reject) => {
        setTimeout(resolve, time);
    })
}
// 1111
// 2222
// 4444
// undefined
// 3333
```

###### koa-同步

```js
const Koa = require("koa");
const app = new Koa();
app.use((ctx, next) => {
    if(ctx.url==="/favicon.ico")return
    console.log("1111");
    ctx.body = "hello";
    next()
    console.log("3333");
})
app.use((ctx, next) => {
    console.log("2222");
})
app.listen(3000)

// 1111
// 2222
// 3333
```

###### koa-异步

```js
const Koa = require("koa");
const app = new Koa();
app.use(async(ctx, next) => {
    if(ctx.url==="/favicon.ico")return
    console.log("1111");
    await next();
    console.log("4444");
    console.log(ctx.token);
    ctx.body = "hello world";
})
app.use(async(ctx, next) => {
    console.log("2222");
    await delay(1000);
    ctx.token = "aaaaaaaaaaaa1111111hj";
    console.log("3333");
})
app.listen(3000)
function delay(time) {
    return new Promise((resolve, reject) => {
        setTimeout(resolve, time);
    })
}
// 1111
// 2222
// 3333
// 4444
// aaaaaaaaaaaa1111111hj
```

###### koa-异步传参另一种写法

```js
const Koa = require("koa");
const app = new Koa();
app.use(async(ctx, next) => {
    if(ctx.url==="/favicon.ico")return
    console.log("1111");
    var mytoken=await next();
    console.log("4444");
    console.log(mytoken);
    ctx.body = "hello world";
})
app.use(async(ctx, next) => {
    console.log("2222");
    await delay(1000);
    console.log("3333");
    return "aaaaaaaaaaaa1111111hj";
})
app.listen(3000)
function delay(time) {
    return new Promise((resolve, reject) => {
        setTimeout(resolve, time);
    })
}
// 1111
// 2222
// 3333
// 4444
// aaaaaaaaaaaa1111111hj
```

#### 4.路由

##### 4.1基本用法

```js
const Koa = require("koa");
const app = new Koa();
const Router = require("koa-router");
const router = new Router();
router.post("/list", (ctx, next) => {
    ctx.body = {
        ok: 1,
        info:"add list success"
    };
})
//获取
.get("/list", (ctx, next) => {
    ctx.body = ["111", "222", "333"];
})
app.use(router.routes()).use(router.allowedMethods());
app.listen(3000)
```

##### 4.2一些方法

| 方法                           | 解释                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| router.allowedMethods();       | 主要用于 405 Method Not Allowed 这个状态码相关 如果不加这个中间件，如果接口是get请求，而前端使用post请求，会返回 404 状态码，接口未定义。如果加了这个中间件，这种情况时，会返回405 Method Not Allowed ，提示 request method 不匹配，并在响应头返回接口支持的请求方法，更有利于调试 |
| router.prefix("/api");         | 所有路由访问前要加上/api                                     |
| router.routes()                | 启动路由                                                     |
| router.redirect("/", "/home"); | 重定向，将/重定向到/home页面                                 |

#### 5.静态资源

```js
const Koa = require("koa");
const static = require("koa-static");
const path = require("path");
const app = new Koa();

app.use(static(path.join(__dirname, "public")));
app.use((ctx,next) => {
    console.log(ctx.request.path);
    ctx.body = { name: "kerwin" };
})
app.listen(3000)
```

#### 6.获取请求参数

##### 6.1get参数

在koa中，获取GET请求数据源头是koa中request对象中的query方法或querystring方法，query返回是格式化好的参数对象，querystring返回的是请求字符串，由于ctx对request的API有直接引用的方式，所以获取GET请求数据有两个途径。

- 从上下文中直接获取请求对象ctxquery，返回如{a:1b2}请求字符串 ctxquerystring，返回如 a=1&b=2
- 从上下文的request对象中获取请求对象ctxrequestquery，返回如{a:1b2}请求字符串 ctx.requestquerystring，返回如a=1&b=2

##### 6.2post参数 

对于POST请求的处理，koa-bodyparser中间件可以把koa2上下文的formData数据解析到ctx.request.body中
const bodyParser=require(koa-bodyparser')
/使用ctx.body解析中间件 app.use(bodyparser())

##### 6.3示例

###### get请求

```html
//login.html
<body>
    <div>
        <div>
            用户名：
            <input type="text" id="username">
        </div>
        <div>
            密码：
            <input type="password" id="password">
        </div>
        <div>
            <button id="login">登录--get</button>
            <button id="loginpost">登录--post</button>
        </div>
    </div>
    <script src="/js/login.js"></script>
</body>
<script>
    var ologin = document.querySelector("#login");
var plogin = document.querySelector("#loginpost");
var username = document.querySelector("#username");
var password = document.querySelector("#password");
//get请求
ologin.addEventListener("click", () => {
    fetch(`/user?username=${username.value}&password=${password.value}`).then(
        res => res.text()).then(res => {
            console.log(res);
        })
})
</script>
```

```js
//user.js
const Router = require("koa-router");
const router = new Router();
//获取
router.get("/", (ctx, next) => {
        //获取前端传来的参数
   console.log(ctx.query);//[Object: null prototype] { username: 'qqq', password: 'qq' }
   console.log(ctx.querystring);//username=qqq&password=qq
   ctx.body = ["aaaa", "bbbb", "cccc"];
})
```

###### post请求

**（1）json格式请求**

```html
//login.html
<body>
    <div>
        <div>
            用户名：
            <input type="text" id="username">
        </div>
        <div>
            密码：
            <input type="password" id="password">
        </div>
        <div>
            <button id="login">登录--get</button>
            <button id="loginpost">登录--post</button>
        </div>
    </div>
    <script src="/js/login.js"></script>
</body>
<script>
    var ologin = document.querySelector("#login");
    var plogin = document.querySelector("#loginpost");
    var username = document.querySelector("#username");
    var password = document.querySelector("#password");
    //post请求
    plogin.addEventListener("click", () => {
        //json表单格式
    fetch(`/user`, {
        method: "POST",
        body: JSON.stringify({
            username: username.value,
            password: password.value
        }),
        headers: {
            "Content-Type": "application/json"
        }
    }).then(res => res.text()).then(res => {
        console.log(res);
    })
</script>
```

```js
//user.js
const Router = require("koa-router");
const router = new Router();
//增加
router.post("/", (ctx, next) => {
    console.log(ctx.request.body);//获取前端传来的参数{ username: 'ddd', password: 's12' }
    ctx.body = {
        ok: 1,
        info:"add user success"
    };
})
```

```js
//index.js
const bodyParser = require("koa-bodyparser");
//应用级
app.use(bodyParser())//获取前端的post参数
```

**（2）form-data格式请求**

```html
<body>
    <div>
        <div>
            用户名：
            <input type="text" id="username">
        </div>
        <div>
            密码：
            <input type="password" id="password">
        </div>
        <div>
            <button id="login">登录--get</button>
            <button id="loginpost">登录--post</button>
        </div>
    </div>
    <script src="/js/login.js"></script>
</body>
<script>
    var ologin = document.querySelector("#login");
var plogin = document.querySelector("#loginpost");
var username = document.querySelector("#username");
var password = document.querySelector("#password");
//post
plogin.addEventListener("click", () => {
    //form表单格式
    fetch(`/user`, {
        method: "POST",
        body: `username=${username.value}&password=${password.value}`,
        headers: {
            "Content-Type": "application/x-www-form-urlencoded  "
        }
    }).then(res => res.text()).then(res => {
        console.log(res);
    })
})
</script>
```

```js
//user.js
const Router = require("koa-router");
const router = new Router();
//增加
router.post("/", (ctx, next) => {
    console.log(ctx.request.body);//不能简写，获取前端传来的参数{ username: 'ddd', password: 's12' }
    ctx.body = {
        ok: 1,
        info:"add user success"
    };
})
```

```js
//index.js
const bodyParser = require("koa-bodyparser");
//应用级
app.use(bodyParser())//获取前端的post参数
```

##### 6.4一些方法

| 方法            | 解释                                                         |
| --------------- | ------------------------------------------------------------ |
| ctx.querystring | username=qqq&password=qq                                     |
| ctx.query       | [Object: null prototype] { username: 'qqq', password: 'qq' } |

#### 7.ejs模板

##### 7.1安装模板

```powershell
# 安装koa模板中间件
npm install --save koa-views
#安装ejs模板引擎
npm install --save ejs
```

##### 7.2使用模板引擎

**文件目录**

![image-20230910115548217](D:\typora_photo\image-20230910115548217.png)

**使用方法**

```js
//app.js
const views = require("koa-views");
//配置模板引擎
app.use(views(path.join(__dirname, "views"),{extension:"ejs"}));
```

```ejs
//home.ejs
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    home模板页面
    <h1>欢迎<%=name  %></h1>
</body>
</html>
```

```js
//home.js
const Router = require("koa-router");
const router = new Router();
//增加
router.get("/", async(ctx, next) => {
    await ctx.render("home",{name:"kerwin"})//自动找views下的home.ejs
})
//等待模板解析完成之后再输出，所以要用await,否则会报错
module.exports = router;
```

#### 8.cookie & session

##### 8.1 cookie

koa提供了从上下文直接读取、写入cookie的方法

- ctx.cookies.get(name[options])读取上下文请求中的cookie

- ctx.cookies.set(namevalu[options])在上下文中写入cookie

![image-20230910171819626](D:\typora_photo\image-20230910171819626.png)

##### 8.2 session

koa-session-minimal适用于koa2的session中间件，提供存储介质的读写接口。

```js
//app.js
const session = require("koa-session-minimal");
//session配置
app.use(session({
    key: "kerwinSessionId",
    cookie: {
        maxAge: 1000 * 60 * 60,
    }
}))
//session判断拦截
app.use(async (ctx, next) => {
    if (ctx.url.includes("login")) {
        await next();
        return
    }
    if (ctx.session.user) {
        ctx.session.date = Date.now();//重新计算过期时间
        await next();
    } else {
        ctx.redirect("/login");
    }
})
```

```js
//user.js
router.post("/login", (ctx, next) => {
    //console.log(ctx.request.body);//{ username: 'ww', password: '11' }
    const { username, password } = ctx.request.body;
    if (username === "admin" && password === "123") {
        //设置session信息 钥匙
        ctx.session.user = {
            username:"ker"
        }
        ctx.body = { ok: 1 };
    } else {
        ctx.body = { ok: 0 };
    }

})
```

```ejs
//login.ejs
<body>
    <h1>登录页面</h1>
    <div>
        <div>
            用户名：
            <input type="text" id="username">
        </div>
        <div>
            密码：
            <input type="password" id="password">
        </div>
        <div>
            <button id="loginpost">登录--post</button>
        </div>
    </div>
</body>
<script>
    var ologin = document.querySelector("#login");
    var plogin = document.querySelector("#loginpost");
    var username = document.querySelector("#username");
    var password = document.querySelector("#password");

    //post请求
    plogin.addEventListener("click", () => {
         //json表单格式
         fetch(`/user/login`, {
             method: "POST",
             body: JSON.stringify({
                 username: username.value,
                 password: password.value
              }),
             headers: {
                 "Content-Type": "application/json"
             }
         }).then(res => res.json()).then(res => {
              if(res.ok===1){
                  location.href="/home";
               }else{
                  alert("用户名与密码不准确");
               }
    })
</script>
```

##### 8.3 JWT

```ejs
//login.ejs
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>登录页面</title>
    <script src="https://cdn.jsdelivr.net/npm/axios@1.1.2/dist/axios.min.js"></script>
    <script>
        //拦截器配置Interceptors
        axios.interceptors.request.use(function (config) {
            console.log("请求发出前执行的方法");
            return config;
        }, function (error) {
            // Do something with request error
            return Promise.reject(error);
        });
        axios.interceptors.response.use(function (response) {
            console.log("任何请求成功后第一个调用的方法");
            console.log(response.headers);//返回响应头的对象
            const {authorization}=response.headers;
            authorization && localStorage.setItem("token",authorization);//存储token
            return response;
        }, function (error) {
            return Promise.reject(error);
        });
    </script>
</head>
<body>
    <h2>登录页面</h2>
    <div>
        <div>用户名：<input id="username"></div>
        <div>密码：<input type="password" id="password"></div>
        <div><button id="login">登录</button></div>
    </div>
    <hr>
    <script>
        var username = document.querySelector("#username");
        var password = document.querySelector("#password");
        var login = document.querySelector("#login");
        login.addEventListener("click", () => {
            console.log(username.value, password.value);
            axios.post("/user/login", {
                username: username.value,
                password: password.value
            }).then(res => {
               // console.log(res.data.ok);
                if (res.data.ok === 1) {
                    location.href = "/";
                } else {
                    alert("用户名和密码不准确");
                }
                //res.data 后端返回响应体
                //res.hrader 后端返回响应头
            })
        })
    </script>
</body>
</html>
```

```ejs
//home.ejs
<!DOCTYPE html>
<html>
<head>
  <script src="https://cdn.bootcdn.net/ajax/libs/twitter-bootstrap/5.2.3/js/bootstrap.min.js"></script>
  <link rel='stylesheet' href='/stylesheets/style.css' />
  <link rel="stylesheet" href="https://cdn.bootcdn.net/ajax/libs/twitter-bootstrap/5.2.3/css/bootstrap.min.css">
  <style>
    #update {
      background-color: aquamarine;
    }
    #dele {
      background-color: rgb(219, 38, 38);
    }
  </style>
  <script src="https://cdn.jsdelivr.net/npm/axios@1.1.2/dist/axios.min.js"></script>
  <script>
    //拦截器配置Interceptors
    axios.interceptors.request.use(function (config) {//config是请求对象
      console.log("请求发出前执行的方法");
      const token = localStorage.getItem("token");
      config.headers.Authorization = `Bearer ${token}`;
      return config;
    }, function (error) {
      // Do something with request error
      return Promise.reject(error);
    });
    axios.interceptors.response.use(function (response) {
      console.log("任何请求成功后第一个调用的方法");
      console.log(response.headers);//返回响应头的对象
      const { authorization } = response.headers;
      authorization && localStorage.setItem("token", authorization);//存储token
      return response;
    }, function (error) {
      console.log(error.response.status);
      //统一错误拦截
      if(error.response.status===401){
        localStorage.removeItem("token");
        location.href="/login";
      }
      return Promise.reject(error);
    });
  </script>
</head>
<body>
  <h2>mongoDB增删改查</h2>
  <h2>后台用户管理业务</h2>
  <button id="exit">退出登录</button>
  <table class="table table-hover">
    <thead>
      <tr>
        <td>序号</td>
        <td>用户名</td>
        <td>年龄</td>
      </tr>
    </thead>
    <tbody></tbody>
  </table>
  <script>
    //axios写法
    var exit = document.querySelector("#exit");
    var tbody=document.querySelector("tbody");
    axios.get("/home/list").then(res => {
      res = res.data;
      tbody.innerHTML = res.map(item => `
        <tr>
          <td id="first">${item._id}</td>
        <td>${item.username}</td>
        <td>${item.age}</td>
      </tr>
        `).join("");
    })
    exit.onclick = () => {
      localStorage.removeItem("token");
      location.href = "/login";
    }
  </script>
</body>
</html>
```

```js
//user.js	
router.post("/login", (ctx) => {
    //console.log(ctx.request.body);//{ username: 'ww', password: '11' }
    const { username, password } = ctx.request.body;
    if (username === "admin" && password === "123") {
        //设置session信息 钥匙
        // ctx.session.user = {
        //     username:"ker"
        // }
        //设置token值
        const token = JWT.generate({_id:"111",username:"kerwin"}, "1h");
        //将token返回在header中
        ctx.set("Authorization", token);
        ctx.body = { ok: 1 };
    } else {
        ctx.body = { ok: 0 };
    }
})
```

```js
//home.js
router.get("/list", async (ctx) => {
    ctx.body = [{
        _id: 1,
        username: "kerwin",
        age: 10
    },
    {
        _id: 2,
        username: "kerwi",
        age: 11
    },
    {
        _id: 3,
        username: "kerw",
        age: 12
    }]
})
```

```js
//index.js
const JWT = require("./util/JWT");
//token拦截
app.use(async (ctx, next) => {
    if (ctx.url.includes("login")){
        await next()
        return   //return是返回值，如果没有值，那么就返回空，编写者其实也就是想中断函数执行
    }
    const token = ctx.headers['authorization']?.split(" ")[1];
    if (token) {
        const payload = JWT.verify(token);
        if (payload) {
            //重新计算过期时间
            const newtoken = JWT.generate({_id:payload._id,username:payload.username}, "1h");
            ctx.set("Authorization", newtoken);
            await next()
        } else {
            ctx.status = 401;
            ctx.body = { errCode: -1, errInfo: "token过期" };
        }
    } else {
        await next()
    }
})
```

```js
//JWT.js
const jwt = require("jsonwebtoken");
const secret = "kerwin-anydata"; 
const JWT = {
    generate(value,expires) {
        return jwt.sign(value, secret, { expiresIn: expires });
    },
    verify(token) {
        try {
            return  jwt.verify(token, secret);
        } catch (error) {
            return false;
        }
    }
}
module.exports = JWT;
```

![image-20230910223011087](D:\typora_photo\image-20230910223011087.png)

![image-20230910223025969](D:\typora_photo\image-20230910223025969.png)

#### 9.文件上传

##### 9.1 安装模块：

##### npm i @koa/multer multer

##### 9.2 引入模块

```js
const multer = require('@koa/multer');
const upload = multer({dest:"public/uploads"});
```

##### 9.3 表单提交示例

```ejs
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <H2>upload文件上传</H2>
    <!-- multipart/form-data 多部分数据传输 -->
    <form action="/user/upload" method="POST" enctype="multipart/form-data">
        <div>用户名：<input type="text" name="username"></div>
        <div>密码<input type="password" name="password"></div>
        <div>年龄：<input type="number" name="age"></div>
        <div>头像：<input type="file" name="avatar"></div>
        <div><input type="submit" value="添加用户"></div>
    </form>
</body>
</html>
```

```js
//upload.js
const Router = require("koa-router");
const router = new Router();
//增加
router.get("/", async(ctx, next) => {
    await ctx.render("upload")//自动找views下的home.ejs
})
//等待模板解析完成之后再输出，所以要用await,负责会报错
module.exports = router;
```

```js
//user.js
//上传接口
const multer = require('@koa/multer');
const upload = multer({dest:"public/uploads"});
router.post("/upload",   upload.single('avatar'),(ctx) => {
    console.log(ctx.request.body, ctx.file);// { username: 'qwa', password: '11', age: '11' } {
    //文件对象{
//   fieldname: 'avatar',
//   originalname: '1694262031.jpg',
//   encoding: '7bit',
//   mimetype: 'image/jpeg',
//   destination: 'public/uploads',
//   filename: '02ed9ecbebc013228d1771efc553dc74',
//   path: 'public\\uploads\\02ed9ecbebc013228d1771efc553dc74',
//   size: 1502306
// }
    ctx.body = { ok: 1 };
})
```

![image-20230910222918703](D:\typora_photo\image-20230910222918703.png)

#### 10.操作MongoDB

koa的数据库操作与express一致

```js
//连接数据库
const mongoose = require("mongoose");
mongoose.connect("mongodb://127.0.0.1:27017/xy_koa");
//插入集合和数据，数据库xy_project会自动创建
const mongoose = require("mongoose");
const Schema = mongoose.Schema;
const UserType = {
    username: String,
    password: String,
    age: Number,
    avatar:String
}
const UserModel = mongoose.model("user",new mongoose.Schema(UserType));
const { username, password, age } = ctx.request.body;
const  avatar  = ctx.file?`/uploads/${ctx.file.filename}`:``;
    //利用模型进行存储操作
     UserModel.create({
        username,
        age,
        password,
        avatar
    })
```

#### 

## 23、MySQL

#### 1.介绍

**付费的商用数据库**:

- Oracle，典型的高富帅;
- SQLServer，微软自家产品，Windows定制专款;·DB2，IBM的产品，听起来挺高端;
- Sybase，曾经跟微软是好基友，后来关系破裂，现在家境惨淡。

这些数据库都是不开源而且付费的，最大的好处是花了钱出了问题可以找厂家解决，不过在Web的世界里，常常需要部署成千上万的数据库服务器，当然不能把大把大把的银子扔给厂家，所以，无论是Google、Facebook，还是国内的BAT，无一例外都选择了**免费的开源数据库**:

- MySQL，大家都在用，一般错不了;（工具：WAMP）
- PostgreSQL，学术气息有点重，其实挺不错，但知名度没有MySQL高;

- sqlite，嵌入式数据库，适合桌面和移动应用。
  作为一个JavaScript全栈工程师，选择哪个免费数据库呢?当然是MySQL，因为MySQL普及率最高，出了错，可以很容易找到解决方法。而且，围绕MySQL有一大堆监控和运维的工具，安装和使用很方便。

![image-20230910225051740](D:\typora_photo\image-20230910225051740.png)

#### 2.与非关系数据库区别

关系型和非关系型数据库的主要差异是**数据存储的方式**。关系型数据天然就是表格式的，因此存储在数据表的行和列中。数据表可以彼此关联协作存储，也很容易提取数据。
与其相反，非关系型数据不适合存储在数据表的行和列中，而是大块组合在一起。非关系型数据通常存储在数据集中，就像文档、键值对或者图结构。你的数据及其特性是选择数据存储和提取方式的首要影响因素。

**关系型数据库最典型的数据结构是表，由二维表及其之间的联系所组成的一个数据组织

优点:
1、易于维护:都是使用表结构，格式一致;
2、使用方便:SQL语言通用，可用于复杂查询;
3、复杂操作:支持SQL，可用于一个表以及多个表之间非常复杂的查询。

缺点:

1、读写性能比较差，尤其是海量数据的高效率读写;         2、固定的表结构，灵活度稍欠;

3、高并发读写需求，传统关系型数据库来说，硬盘/O是一个很大的瓶颈。

**非关系型数据库严格上不是一种数据库，应该是一种数据结构化存储方法的集合，可以是文档或者键值对等。**

优点:
1、格式灵活:存储数据的格式可以是keyvalue形式、文档形式、图片形式等等，文档形式、图片形式等等，使用
灵活，应用场景广泛，而关系型数据库则只支持基础类型。 激活 Windows 
2、速度快:nosql可以使用硬盘或者随机存储器作为载体，而关系型数据库只能使用硬盘; 
3、高扩展性; 

4 成本低:nosql数据库部署简单，基本都是开源软件。

缺点:
1、不提供sql支持;

2、无事务处理;

3、数据结构相对复杂，复杂查询方面稍欠。

#### 3.SQL语句

![image-20230910231051455](D:\typora_photo\image-20230910231051455.png)

插入

```mysql
INSERT INTO `students`(`id`, `name`, `score`, `gender` ) VALUES (nu11,'kerwin',100,1)
//可以不设置idcreate_time
```

更新

```mysql
UPDATE `students`SET `name`='tiechui', `score`=20, `gender` =0 WHERE id=2;
```

删除

```mysql
DELETE FROM `students` WHERE id=2;
```

查询

```mysql
查所有的数据所有的字段
SELECT * FROM `students` WHERE 1;

查所有的数据某个字段
SELECT `id`, `name`, `score`, `gender` FROM `students` WHERE 1;

条件查询
SELECT * FROM studentsWHERE score>=80;
SELECT*FROM students where score>=80 AND gender=1

模糊查询 I 
SELECT* FROM `students` where name like'%k%' //名字中包含k的
SELECT* FROM `students` where name like'k%'  //第一个字母是k的

排序
SELECT id, name, gender score FROM students ORDER BY score;
SELECT id, name, gender, score FROM students ORDER BY score DESC;

分页查询
SELECT id, name, gender, score FROM students LIMIT 50 OFFSET O //OFFSET偏移量

记录条数
SELECT COUNT(*) FROM students;
SELECTCOUNT(*) kerwinnum FROM students;

多表查询
SELECT*FROM students,c1asses;(这种多表查询又称笛卡尔查询，使用笛卡尔查询时要非常小心，由于结果集是目标表的行数乘积，对两个各自有100行记录的表进行笛卡尔查询将返回1万条记录，对两个各自有1万行记录的表进行笛卡尔查询将返回1亿条记录) 
SELECT
students.id sid,
students.name, 
students.gender, 
students.score,
classes.id cid.
c1asses.name cname
FROM students,c1asses;(要使用表名，列名这样的方式来引用列和设置别名，这样就避免了结果集的列名重复问题。)

SELECT
s.id sid,
s.name, 
s.gender, 
s.score,
c.id cid.
c.name cname
FROM students s,c1asses c;(SQL允许给表设置一个别名 )

联表查询
SELECT
s.id ,
s.name, 
s.class_id, 
s.score,
s.gender,
c.name class_name
FROM students s
INNER JOIN c1asses c
ON s.class_id=c.id(连接查询对多个表进行JOIN运算，简单来说，就是先确定一个主表作为结果集，然后把其他表的行选择性地连接在主表的结果集上)。
```

<img src="D:\typora_photo\image-20230911093346217.png" alt="image-20230911093346217" style="zoom:80%;" />

![image-20230911093655635](D:\typora_photo\image-20230911093655635.png)

##### 注意

1.InnoDB支持事务，MyISAM不支持事务。这是MySQL将默认存储引擎从MylSAM变成InnoDB的重要原因之一;

2.InnoDB支持外键，而MyISAM 不支持。对一个包含外键的InnoDB表转为MYISAM 会失败;

##### 外键约束 

**CASCADE**
在父表上update/delete记录时，同步update/delete掉子表的匹配记录 。

**SET NULL**
在父表上update/delete记录时，将子表上匹配记录的列设为null(要注意子表的外键列不能为not null)。

**NO ACTION**
如果子表中有匹配的记录，则不允许对父表对应候选键进行update/delete操作 。

**RESTRICT**
同no action,都是立即检查外键约束。

#### 4.nodejs操作数据库

##### 连接数据库

安装数据库模块 npm i mysql2

```js
const express = require("express");
const app = express();
const mysql2 = require("mysql2");
app.get("/", async(req, res) => {
    const config = getDBConfig();
    const promisePool = mysql2.createPool(config).promise();
    var name = "ddd";
    var user = await promisePool.query(`select * from users`);
    console.log(user[0]);
    // [
    //     [ { name: 'ddd', id: 1 }, { name: 'ddss', id: 2 } ],  user[0]
    //     [ `name` VARCHAR(255), `id` INT NOT NULL PRIMARY KEY ]   user[1]
    //   ]
    res.send(user[0]);
})
app.listen(5000)
function getDBConfig() {
    return {
        host: '127.0.0.1',
        port: 3306,
        user: "root",
        password: "123456",
        database: "studentd",
        connectionLimit:1 //限制连接个数
    }
}
```

##### 查询语句

```js
var user = await promisePool.query(`select * from users where name="${name}"`);
//注意引号必须加上
var user = await promisePool.query(`select * from users where name=? and id=?`,[name,1]);
//相当于传参
```

##### 插入语句

```js
var user = await promisePool.query(`insert into users (name,id) values (?,?)`, ["hgh", 3]);
```

##### 删除语句

```js
var user = await promisePool.query(`delete from users where id=?`, [4]);
```

**更新语句**

```js
var user = await promisePool.query(`update users set name=? where id=?`, ["kerwin", 2]);
```

## 24.socket编程

#### 1.websocker介绍

![image-20230911164636391](D:\typora_photo\image-20230911164636391.png)

##### 应用场景:

- 弹幕

- 媒体聊天

- 协同编辑
- 基于位置的应用
- 体育实况更新
- 股票基金报价实时更新

WebSocket并不是全新的协议，而是利用了HTTP协议来建立连接。我们来看看WebSocket连接是如何创建的首先，WebSocket连接必须由浏览器发起，因为请求协议是一个标准的HTTP请求，格式如下:

```js
GET ws://1oca7host:3000/ws/chat HTTP/1.1 
Host:1oca1host
Upgrade: websocket 
Connection: Upgrade I
origin:http://1oca1host:3000
Sec-websocket-Key:c1ient-random-string 
Sec-Websocket-Version:13
```

该请求和普通的HTTP请求有几点不同:
1.GET请求的地址不是类似/path/，而是以ws://开头的地址;
2.请求头upgrade:websocket和Connection:Upgrade表示这个连接将要被转换为WebSocket连接;
3.Sec-websocket-Key是用于标识这个连接，并非用于加密数据;
4.Sec-websocket-Version指定了WebSocket的协议版本。
随后，服务器如果接受该请求，就会返回如下响应:

```js
HTTP/1.1 101 Switching Protocols 
Upgrade:websocket
Connection: Upgrade
Sec-websocket-Accept:server-random-string
```

该响应代码**101表示本次连接的HTTP协议**即将被更改，更改后的协议就是Upgrade:websocket指定的

WebSocket协议。

版本号和子协议规定了双方能理解的数据格式，以及是否支持压缩等等。如果仅使用WebSocket的API，就不需要关心这些。

现在，**一个WebSocket连接就建立成功，浏览器和服务器就可以随时主动发送消息给对方。**

消息有两种，一种是文本，一种是二进制数据。通常，我们可以发送JSON格式的文本，这样，在浏览器处理起来就十分容易。

为什么WebSocket连接可以实现全双工通信而HTTP连接不行呢?实际上HTTP协议是建立在TCP协议之上的，**TCP协议本身就实现了全双工通信**，但是HTTP协议的请求-应答机制限制了全双工通信。WebSocket连接建立以后，其实只是简单规定了一下:接下来，咱们通信就不使用HTTP协议了，直接互相发数据吧。

安全的WebSocket连接机制和HTTPS类似。首先，浏览器用wss://xxx创建WebSocket连接时，会先通过HTTPS创建安全的连接，然后，该HTTPS连接升级为WebSocket连接，底层通信走的仍然是安全的SSL/TLS协议。

#### 2.使用

**安装ws模块：npm i ws**

```js
//index.js
const express = require("express");
const app = express();
app.use(express.static("./public"));
//http服务响应
app.get("/", (req, res) => {
    res.send("hello");
})
app.listen(3000)
//websocket服务响应
const WebSocket = require("ws");
const WebSocketServer = WebSocket.WebSocketServer;
const wss = new WebSocketServer({ port: 8080 });//设定端口号
wss.on('connection', function connection(ws) {
    ws.on('error', console.error);
    ws.on('message', function message(data, isBinary) {
        console.log('received: %s', data);//received: 11111
        wss.clients.forEach(function each(client) { // wss.clients所有连接服务器的客户端
            if (client !== ws && client.readyState === WebSocket.OPEN) { //排除给自己发
                client.send(data, { binary: isBinary });
            }
        });
    });
    ws.send('欢迎来到聊天室');//向客户端发送信息
});
//其中ws表示当前用户，wss表示后台服务器
```

```html
//chat.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
   <h1>聊天室</h1>
   <script>
    var ws=new WebSocket("ws://localhost:8080");
    ws.onopen=()=>{
        console.log("连接成功");
    }
    ws.onmessage=(msgObj)=>{
        console.log(msgObj.data);//后端返回的数据
    }
    ws.onerror=()=>{
        console.log("error");
    }
   </script>
</body>
</html>
```

![image-20230912100848577](D:\typora_photo\image-20230912100848577.png)

#### 3.小案例

为chat页面设置token以及获取聊天用户信息

主要思想：（1）建立socket连接，将localStorage里的token值放在连接ws://localhost:8080?后面,接着后端进行token校验，如若token存在则发送欢迎来到聊天室的封装信息，其中该封装信息包含一个函数的调用，传入聊天类型，便于后续判断，接着将解密后的参数payload赋值给当前用户ws的user属性。

（2）当用户添加进入时，群发聊天用户信息的对象，封装一个sendAll（）方法，当有用户登录进入时，发送用户信息到登录用户的控制台，其中WebSocketType为GroupList类型，此时前端通过对后端发送消息进行解析，利用switch()对WebSocketType的不同发出不同响应：其中当为GroupList时，就动态创建下拉框，显示用户名。

（3）当触发send按钮发送消息时，当选择群发时，后端响应ws.send发送的GroupChat，通过wss.clients所有连接服务器的客户端将信息发送给每一个连接的用户，前端响应GroupChat，设置数据显示格式。相反，若为私聊，则通过client.user.username===msgObj.touser设置私聊用户，将信息发送给它，前端响应SingleChat，设置数据显示格式。

```js
//引入chat路由 chat.js
var express = require('express');
var router = express.Router();
/* GET home page. */
router.get('/', function (req, res, next) {
  if(req.url=="/favicon.ico")return
  res.render('chat');
});
module.exports = router;
```

```js
//app.js
var chatRouter = require('./routes/chat');
app.use('/chat', chatRouter);
```

```ejs
//chat.ejs
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>聊天室</h1>
    <input type="text" id="text"><button id="send">send</button>
    <!-- 动态创建 -->
    <select id="select">
    </select>
    <script>
        var select = document.querySelector("#select");
        var send = document.querySelector("#send");
        var text = document.querySelector("#text");
        const WebSocketType = {
            Error: 0,//错误
            GroupList: 1,
            GroupChat: 2,
            SingleChat: 3
        }
        //建立socket连接，带着token,后端验证
        var ws = new WebSocket(`ws://localhost:8080?token=${localStorage.getItem("token")}`);
        ws.onopen = () => {
            console.log("连接成功");
        }
        ws.onmessage = (msgObj) => {
            // console.log(JSON.stringify(msgObj.data));
            try {
                msgObj = JSON.parse(msgObj.data);
            } catch (error) {
                console.log(error);
            }
            switch (msgObj.type) {
                case WebSocketType.Error:
                    localStorage.removeItem("token");
                    location.href = "/login";
                    break;
                case WebSocketType.GroupList://对于后端返回的聊天类型制定对应对话框
                    console.log(JSON.parse(msgObj.data));
                    const onlineList = JSON.parse(msgObj.data);
                    select.innerHTML = "";//先清空之前的数据
                    select.innerHTML = `<option value="all">all</option>` +              onlineList.map(item => `
                    <option value="${item.username}">${item.username}</option>
                    `).join("");
                    break;
                case WebSocketType.GroupChat:
                    //为了避免与刚开始进入聊天室发送的GroupChat区分
                    var title = msgObj.user ? msgObj.user.username : "广播";
                    console.log(title + ":" + msgObj.data);
                    break;
                case WebSocketType.SingleChat:
                    console.log(msgObj.user.username + ":" + msgObj.data);
                    break;
            }
        }
        ws.onerror = () => {
            console.log("error");
        }
        send.onclick = function () {
            if (select.value === "all") {
                //console.log("群发");
                ws.send(createMessage(WebSocketType.GroupChat, text.value));
            } else {
                //console.log("私聊");
                ws.send(createMessage(WebSocketType.SingleChat, text.value, select.value));
            }
        }
        function createMessage(type, data, touser) {
            return JSON.stringify({
                type, data, touser//touser为给谁发的信息
            })
        }
    </script>
</body>
</html>
```

```js
//WebSocketServer.js
//websocket服务响应
const WebSocket = require("ws");
const JWT = require("../util/JWT");
const WebSocketServer = WebSocket.WebSocketServer;
const wss = new WebSocketServer({ port: 8080 });
wss.on('connection', function connection(ws, req) {
    //原生http解析
    //console.log(req.url);//可以获取到路径后面的？值
    const myURL = new URL(req.url, "http://127.0.0.1:3000");
    //console.log(myURL.searchParams.get("token"));  //得到token的对象值
    //校验token
    const payload = JWT.verify(myURL.searchParams.get("token"));
    if (payload) {
        ws.send(createMessage(WebSocketType.GroupChat, null, "欢迎来到聊天室"));//只能传JSON或者string
        ws.user = payload;//添加用户信息到客户端
        //群发
        sendALL();
    } else {
        ws.send(createMessage(WebSocketType.Error, null, "token过期"));
    }
    ws.on('error', console.error);
    ws.on('message', function message(data, isBinary) {
        const msgObj = JSON.parse(data);
        switch (msgObj.type) {
            case WebSocketType.GroupList:
                //console.log(Array.from(wss.clients).map(item=>item.user));
                 ws.send(createMessage(WebSocketType.GroupList,null,JSON.stringify(Array.from(wss.clients).map(item=>item.user))))
                break;
            case WebSocketType.GroupChat:
                //console.log(msgObj.data);
                wss.clients.forEach(function each(client) {
                    // wss.clients所有连接服务器的客户端
                     if (client.readyState === WebSocket.OPEN) { //排除给自己发
              client.send(createMessage(WebSocketType.GroupChat,ws.user,msgObj.data),{                 binary: false });
         }
          });
                break;
            case WebSocketType.SingleChat:
                wss.clients.forEach(function each(client) {
                    // wss.clients所有连接服务器的客户端
                 if (client.user.username===msgObj.touser&&client.readyState ===                             WebSocket.OPEN) { //排除给自己发
          client.send(createMessage(WebSocketType.SingleChat,ws.user,msgObj.data), {               binary: false });
                     }
                 });
                break;
            default:
                break;
        }
    });
    ws.send('欢迎来到聊天室');
    //用户断联
    ws.on("close", () => {
        wss.clients.delete(ws.user);//删除用户
        // console.log(ws.user);
        sendALL();
    })
});
const WebSocketType = {
    Error: 0,//错误
    GroupList: 1,
    GroupChat: 2,
    SingleChat: 3
}
function createMessage(type, user, data) {
    return JSON.stringify({
        type, user, data
    })
}
function sendALL() {
    wss.clients.forEach(function each(client) {
        if (client.readyState === WebSocket.OPEN) {
            client.send(createMessage(WebSocketType.GroupList, null, JSON.stringify(Array.from(wss.clients).map(item => item.user))))
        }
    })
}
```

```js
 //打印所有连接的用户信息
console.log(Array.from(wss.clients).map(item=>item.user));
```

![image-20230912102702721](D:\typora_photo\image-20230912102702721.png)

![image-20230912165622122](D:\typora_photo\image-20230912165622122.png)



![image-20230912165730695](D:\typora_photo\image-20230912165730695.png)



## 附录

#### （1）转义html函数

![image-20230821211020540](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230821211020540.png)

#### （2）SPA

**SPA**，即**单页面应用**(Single Page Application)。所谓单页 `Web` 应用，就是只有一张 `Web` 页面的应用。单页应用程序 (SPA) 是加载单个 `HTML` 页面并在**用户与应用程序交互时**动态更新该页面的 `Web` 应用程序。浏览器一开始会加载必需的 `HTML` 、 `CSS` 和 `JavaScript` ，所有的操作都在这张页面上完成，都由 `JavaScript` 来控制。

#### (3)正则表达式

正则表达式的语法中两条斜线中间是正则主体，这部分可以有很多字符组成；

![image-20230903111330855](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230903111330855.png)

匹配中文字符的正则表达式： [\u4e00-\u9fa5]

#### （4）token过期

Token是指代表着用户身份的字符串，当用户进行登录认证后，系统会生成并返回一个Token，以后用户的每一次请求都需要携带该Token以便服务器对其进行身份校验。

##### Token过期的原因

1、用户长时间未进行操作，导致Token失效；
2、Token设置的过期时间到期；
3、服务器端的Token存储出现异常。

#### （5）cookie

cookie其实就是一些数据信息，类型为“小型文本文件”，存储于电脑上的文本文件中。
           当我们打开一个网站时，如果这个网站我们曾经登录过，当我们再次打开网站时，发现就不需要再次登录了，而是直接进入了首页。其实就是游览器保存了我们的cookie，里面记录了一些信息，当然，这些cookie是服务器创建后返回给游览器的。游览器只进行了保存。下面展示bilibili网站保存的cookie。
           一般情况下，cookie是以键值对进行表示的(key-value)

#### （6）列表的join方法

list.join("");将列表中数据变成字符串

#### （7）表单input

```html
<input type="file" class="form-control" id="avatar" placeholder="avatar">
var avatar=document.querySelector("#avatar");
```

如果需要**批量**选择文件，可以加上：

```html
<input type="file" class="form-control" id="avatar" placeholder="avatar" multiple>
```

其中：avatar.files的结果是：

<img src="C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230909164920225.png" alt="image-20230909164920225"  />

avatar.value的结果是：C:\fakepath\2.png

对于后端来说则需要在req中获取一个req.file文件对象，来解析获取前端发送的avatar.files[0]例如：

![image-20230909171013588](D:\typora_photo\image-20230909171013588.png)

