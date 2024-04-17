# CMP架构简介

CMP 架构是基于移动原生与 H5 混合模式开发。

![CMP架构图](CMP(M3H5).assets/CMP架构图.pngrev=1.png)

整体总共分为4个部分：

## 核心层

主要是对 Android、iOS、Harmony(鸿蒙) 系统的基础能力进行规范统一的抽象封装如：网络请求、本地文件读写等。也是移动端运行环境的基础。M3 APP 的原生应用部分的开发也是基于此层开发。

都是基于Linux系统内核进行构建的上层应用系统，能够兼容AndroidOS。

## 移动平台CMP

主要通过原生程序结合 H5 混合方式开发对上层提供统一的基础 API，并且在移动平台层将第三方集成和跨平台的能力进行了封装，并且提供了统一的标准与开发规范。

Cordova CMP平台H5与原生程序间相互调用通讯的中间件

## 应用层

使用 S3 工具编译构建后生成 M3 APP 可运行的 ZIP 与微协同可运行的 HTML 静态资源。

一次编写构建，多端运行。

## 客户端

1. M3 APP：全部基于 H5 完成开发。并通过 S3 工具编译生成可运行与 M3 中的 ZIP 包。
2. 微协同：通过 H5 方式提供可集成到第三方系统的致远移动办公系统，目前标准已支持集成到微信、企业微信、钉钉、飞书和 Welink APP 中。

# [S3编辑工具的使用](https://opendoc.seeyoncloud.com/bin/view/technology/categoryOfTechnology/t_m3/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E5%9F%BA%E7%A1%80%E5%BC%80%E5%8F%91%E5%9F%B9%E8%AE%AD%E6%BC%94%E7%A4%BA/0205%20S3%E7%BC%96%E8%BE%91%E5%B7%A5%E5%85%B7%E7%9A%84%E4%BD%BF%E7%94%A8/)

## 作用

移动端H5的代码原则上是一套源代码，通过S3工具编辑后，能生成多端运行的代码。本质就是通过此工具将html、s3js、css三种后缀文件中的类似${data:dependencies.cmp}这种格式的静态资源路径进行一个替换，如：

<img src="CMP(M3H5).assets/image-20210913180252225.pngrev=1.png" alt="image-20210913180252225.png" style="zoom:150%;" />

**PS**：如果不通过此工具构建，相关的html、js、css是无法用程序运行的

## 构建标签

| 序号 |                   标签                    | 说明                                                         |
| :--: | :---------------------------------------: | :----------------------------------------------------------- |
|  1   |         ${data:dependencies.cmp}          | 常见的标签，对应单个应用模块的路径                           |
|  2   |    <s3:import type="css"></s3:import>     | 对于一些有共性的页面元素，可以抽取成组件模板，编辑的时候会将此标签对应的模型进行替换，相当于PC端JSP页面的include |
|  3   | <s3:data name='CollDatas.headerScript' /> | 同上，只是共性的模型更聚焦，比如此处就是协同模块的头部script标签的统一导入，因为在协同模块的每一个页面都会有这样的模板元素 |
|  4   |           ${data:buildversion}            | 对js、css等静态资源添加后缀，用于版本控制，更重要的是清除浏览器静态资源缓存 |

## 工具使用

### 组成结构

![11.png](https://opendoc.seeyoncloud.com/bin/download/technology/categoryOfTechnology/t_m3/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E5%9F%BA%E7%A1%80%E5%BC%80%E5%8F%91%E5%9F%B9%E8%AE%AD%E6%BC%94%E7%A4%BA/0205%20S3%E7%BC%96%E8%BE%91%E5%B7%A5%E5%85%B7%E7%9A%84%E4%BD%BF%E7%94%A8/WebHome/11.png?rev=1.1)

【java】：该工具由java语言开发，相关的功能使用由jar在此文件夹中，开发者无需关注此文件夹

【publishcmd】：应用构建脚本集合，所有的H5应用微协同版本和M3应用zip包版本的脚本集合，根据配置信息启动工具构建不同的静态文件版本

【publishoutput】：构建完成后的可运行文件的输出目录,此目录构建出来的文件是可以直接运行的

【workspace】：项目源码的开发路径，此文件夹的路径，开发者最好按照此文件夹结构将开发项目源码导入进去，这样减少其他的学习成本

【文档】：此工具的一些说明性文档，开发者可以不用过多关注

【batchbuild.cmd】：批量构建脚本，通过配置可以将多个模块进行构建，可以同时构建出zip包和微协同模式的运行代码，一般用于某个开发者同时涉及多个应用模块的开发，**开发者关注此文件**

### batchbuild 批量构建脚本

![1631628160337-480.png](CMP(M3H5).assets/1631628160337-480.pngrev=1.png)

# CMP API

## [路由 href](http://open.seeyon.com/seeyon/cmp2.0/v8.0-doc/index.html#cmp-href-next)

