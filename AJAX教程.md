#                                                                                                       AJAX(Asynchronous Javascript And Xml)教程

笔记：https://blog.csdn.net/weixin_44972008/article/details/113772348

视频：https://www.bilibili.com/video/BV1WC4y1b78y/?p=16&spm_id_from=pageDriver&vd_source=68d62bca83c00beffe7ed7e574e02f6c

开源加速项目，例如jquery链接：https://www.bootcdn.cn/

ajax:xhr（jquery/axios）和fetch

## 传统请求以及缺点

##### 传统请求方式有哪些：

- 直接在浏览器地址栏上输入URL

- 点击超链接

- 提交form表单

- 使用JS代码发送请求

    window.open(url)

    document.location.href=url

​          window.location.href=url

##### 传统请求存在的问题

- 页面全部刷新导致了用户的体验较差。
- 传统的请求导致用户的体验有空白期。(用户的体验是不连贯的)

## ![image-20230820142038291](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820142038291.png)

### 1.AJAX简介

**AJAX 全称为Asynchronous Javascript And XML，就是 异步 JS和 XML** 
**通过 AJAX可以在浏览器中向服务器发送异步请求，最大的优势:*无刷新获取数据*。**

**AJAX 不是新的编程语言，不是新的一门独立的技术，而是一种使用现有标准的新方法。**

- AJAX 全称为Asynchronous JavaScript And XML，就是**异步**的 JS和XML。
- 通过 AJAX 可以在浏览器中向服务器发送异步请求，**最大的优势:无刷新获取数据。**
- AJAX 不是新的编程语言，而是一种将现有的标准组合在一起使用的新方式。
- AJAX不能称为一种技术，它是多种技术的综合产物。
- AJAX可以让浏览器发送一种特殊的请求，这种请求可以是：异步的。

- ###### 什么是异步，什么是同步？

  - 假设有t1和t2线程，t1和t2线程并发，就是异步。
  - 假设有t1和t2线程，t2在执行的时候，必须等待t1线程执行到某个位置之后t2才能执行，那么t2在等t1，显然他们是排队的，排队的就是同步。
  - AJAX是可以发送异步请求的。也就是说，在同一个浏览器页面当中，可以发送多个ajax请求，这些ajax请求之间不需要等待，是并发的。

- AJAX代码属于WEB前端的JS代码。和后端的java没有关系，后端也可以是php语言，也可以是C语言。

- AJAX 应用程序可能使用 XML 来传输数据，但将数据作为纯文本或 JSON 文本传输也同样常见。

- AJAX可以更新网页的部分，而不需要重新加载整个页面。（页面局部刷新）

- AJAX可以做到在同一个网页中同时启动多个请求，类似于在同一个网页中启动“多线程”，一个“线程”一个“请求”。![image-20230820143227952](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820143227952.png)

![image-20230820144221512](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820144221512.png)

![image-20230820144423738](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820144423738.png)

### 2.XML

- XML 可扩展标记语言。
- XML 被设计用来**传输和存储**数据。
- XML 和HTML 类似，不同的是**HTML中都是预定义标签，而XML中没有预定义标签**，
- 全都是自定义标签，用来表示一些数据。

比如说我有一个学生数据:   name"孙悟空";age=18;gender="男"
用XML 表示:

```xml
<student>
<name>孙悟空</name>
<age>18</age>
<gender>男</gender>
</student>
```

现在已经被JSON取代了。

```json
{"name":"孙悟空","age":18,"gender":"男"}
```

### 3.AJAX的特点

#### （1）优点

- 可以**无需刷新页面**而与服务器端进行通信。
- 允许你**根据用户事件来更新部分页面内容**。

#### （2)缺点

- 没有浏览历史，不能回退

- 存在跨域问题(同源)

- SEO 不友好

### 4.安装环境

（1）安装node.js

http://nodejs.cn/

(2)安装express（服务端框架）

https://www.expressjs.com.cn/

![img](https://img-blog.csdnimg.cn/20210209164615378.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjAwOA==,size_16,color_FFFFFF,t_70)

(1)   初始化环境

```shell
npm init --yes
```

(2)  下载express包

```shell
npm install express --save
```

### 5.XMLHttpRequest

- XMLHttpRequest对象是AJAX的核心对象，发送请求以及接收服务器数据的返回，全靠它了。

- XMLHttpRequest对象，现代浏览器都是支持的，都内置了该对象。直接用即可。

- 创建XMLHttpRequest对象

  - ```javascript
    var xhr = new XMLHttpRequest();
    ```

- XMLHttpRequest对象的方法

| 方法                                          | 描述                                                         |
| :-------------------------------------------- | :----------------------------------------------------------- |
| abort()                                       | 取消当前请求                                                 |
| getAllResponseHeaders()                       | 返回头部信息                                                 |
| getResponseHeader()                           | 返回特定的头部信息                                           |
| open(*method*, *url*, *async*, *user*, *psw*) | 规定请求method：请求类型 GET 或 POSTurl：文件位置async：true（异步）或 false（同步）user：可选的用户名称psw：可选的密码 |
| send()                                        | 将请求发送到服务器，用于 GET 请求                            |
| send(*string*)                                | 将请求发送到服务器，用于 POST 请求                           |
| setRequestHeader()                            | 向要发送的报头添加标签/值对                                  |

- XMLHttpRequest对象的属性

| 属性               | 描述                                                         |
| :----------------- | :----------------------------------------------------------- |
| onreadystatechange | 定义当 readyState 属性发生变化时被调用的函数                 |
| readyState         | 保存 XMLHttpRequest 的状态。0：请求未初始化     1：服务器连接已建立     2：请求已收到    3：正在处理请求    4：请求已完成且响应已就绪 |
| responseText       | 以字符串返回响应数据                                         |
| responseXML        | 以 XML 数据返回响应数据                                      |
| status             | 返回请求的状态号200: "OK"403: "Forbidden"404: "Not Found"    |
| statusText         | 返回状态文本（比如 "OK" 或 "Not Found"）                     |



### 6.HTTP协议

http（hypertext transport protocol）协议 [超文本传输协议]，协议详细规定了浏览器和万维网服务器之间互相通信的规则。

#### HTTP协议的特点

​    基于请求/响应模型的协议。请求和响应必须成对；必须先有请求,才会有响应
​    简单快捷, 因为发送请求的时候只需要发送请求方式和请求路径即可
​    无状态协议, 多次请求之间相互独立，不能交互数据

#### HTTP协议默认的端口:80

​        例如： http://www.lagou.com:80

#### Http协议的版本

​        HTTP/1.0，发送请求，创建一次连接，获得一个web资源，连接断开。
​        HTTP/1.1，发送请求，创建一次连接，获得多个web资源，连接断开。

#### HTTP协议有两种报文格式：

**请求报文：**由客户端向服务器端发出的报文。
**响应报文：**从服务端到客户端的报文。

#### HTTP请求头

**请求头:** 描述了客户端向服务器发送请求时使用的http协议类型，所使用的编码，以及发送内容的长度，referer，等等。请求头也是用的键值对key:value

#### 请求体

通常情况下，**只有post请求方式才会使用到请求体**，请求体中都是用户表单提交的数据，每一项数据都使用键值对key=value，多组值使用&相连。
例如；username=tom&password=1234

#### （1）请求报文  格式参数

🎯行      POST /s?ie=utf-8  HTTP/1.1

📚 头     Host：atguigu.com

​              Cookie: name=guigu

​             Content-type:application/x-www-form-urlencoded

​             User-Agent: chrome 83

空行

体         username=admin&password=admin

若是GET请求则请求体为空，若为POST请求，则请求体不为空。

**<u>请求体的作用: 存放客户端向服务器端传递的数据 .</u>***

#### （2）响应报文

🎯行      HTTP/1.1  200  OK

📚 头       Content-type:text/html;charset=utf-8

​                Content-length:2048

​                Content-encoding:gzip  (压缩方式)

空行

体         <html> <head></head>

​            <body> <h1>尚硅谷</h1></body></html>

**<u>响应体：服务端响应到客户端部分, 可能是HTML页面, JS文件,CSS文件, 图片</u>**

请求方式：GET  POST

https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/readyState

![image-20230818102916888](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230818102916888.png)

4：服务端发送回客户端此时，已经完成了HTTP响应的接收（所有结果已经返回）

![image-20230820145816476](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820145816476.png)

#### （3）注意事项

-  xhr.send('1234567654321');    **xhr.send**可以设置请求体内部格式为任意形式。


- xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')


其中 Content-Type是设置请求体类型，application/x-www-form-urlencoded是请求体参数类型写法，是固定的

- 若想要**自定义**请求头，例如：

 xhr.setRequestHeader('name', 'hujh');

需要在js文件的app.get()中设置响应头**response.setHeader('Access-Control-Allow-Headers', '*');**//表示任意类型头信息都可以接收，同时把app.post改为**app.all**便可实现(app.all  可以接收任意类型的请求)

- 服务端的响应结果response.send()里面传入**字符串类型和名词**，例如：

```js
const data = {
        name: 'anah'
    }
    let str = JSON.stringify(data);
    //设置响应体
 response.send(str);
//或者
 response.send('11123445');
```

- 对响应体数据手动转化为JSON格式

  ```js
  let data = JSON.parse(xhr.response);
  console.log(data);
  result.innerHTML = data.name;
  ```

  对响应体自动转换为JSON格式

  ```js
  //设置响应体数据的类型
  xhr.responseType = 'json';
  console.log(xhr.response);
  result.innerHTML = xhr.response.name;
  ```

### 7.安装nodemon自动重启工具

文件内容有修改自动重新启动服务，当保存代码Ctrl+S时会自动重启服务
https://www.npmjs.com/package/nodemon

![img](https://img-blog.csdnimg.cn/20210301205043799.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk3MjAwOA==,size_16,color_FFFFFF,t_70)

安装

```powershell
npm install -g nodemon
```

启动服务

```powershell
nodemon server.js
```

若出现报错说此系统上禁止运行脚本，则命令改为 

```powershell
npx nodemon server.js
```

### 8.理解

- 使用XMLHttpRequest (XHR)对象可以与服务器交互, 也就是发送ajax 请求。

- 前端可以获取到数据，而无需让整个的页面刷新。

- 这使得Web 页面可以只更新页面的局部，而不影响用户的操作。

  https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest

- XMLHttpRequest，AJAX 的所有操作都是通过该对象进行的

### 9.核心对象使用步骤

#### （1）创建XMLHttpRequest 对象

```js
var xhr = new XMLHttpRequest();
```

#### （2）设置请求信息（请求方法和url）

```js
xhr.open(method, url);
```

#### （3）可以设置请求头，一般不设置

```js
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
```

#### （4）发送请求

```js
xhr.send(body) //get请求不传 body 参数，只有post请求使用
```

#### （5）接收响应（事件绑定，处理服务端返回的结果）

```js
//xhr.responseXML 接收 xml格式 的响应数据
//xhr.responseText 接收 文本格式 的响应数据
xhr.onreadystatechange = function (){
	// readyState 是 xhr对象中的属性, 表示状态 0 1 2 3 4
	if(xhr.readyState == 4 && xhr.status == 200){
		var text = xhr.responseText;
		console.log(text);
	}
}
```

readyState的5个状态：

*0：xhr对象在实例化出来的那一刻，就已经是0状态，代表着xhr是初始化状态。*

1：send方法还没有被调用，即:请求没有发出去，此时**依然可以修改请求头**。

*2：send方法被调用了，即;请求已经发出去了，此时已经不可以再修改请求头。*

3：已经回来一部分数据了，如果是比较小的数据，会在此阶段一次性接收完毕。

4：数据完美的回来了。

#### （6）GET请求

AJAX get请求如何提交数据呢？

- get请求提交数据是在“请求行”上提交，格式是：url?name=value&name=value&name=value....
- 其实这个get请求提交数据的格式是HTTP协议中规定的，遵循协议即可。

点击返回响应信息

![image-20230818212033052](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230818212033052.png)

```js
<button>点击发送请求</button>
<div id="result"></div>
<script>
       const btn = document.querySelector('button');
       const result = document.querySelector('#result');
       btn.addEventListener("click", function () {
           //创建对象
           const xhr = new XMLHttpRequest();
           //初始化 设置请求方法和url
           xhr.open('GET', 'http://127.0.0.1:8000/server?a=200&b=300&c=400');
           //发送
           xhr.send();
           //事件绑定 处理服务端返回的结果
           //readystate 是xhr对象中的属性，表示状态0 1 2 3 4
           xhr.onreadystatechange = function () {
                //判断（服务端返回了所有结果）
                if (xhr.readyState === 4) {
                    //判断响应状态码 200 404 403 401 500
                    //2xx  成功（2开头表示成功）
                    if (xhr.status >= 200 && xhr.status < 300) {
                        //处理结果 行 头 空行 体
                        //1.响应行
                        console.log(xhr.status);//状态码
                        console.log(xhr.statusText);//状态字符串
                        console.log(xhr.getAllResponseHeaders);//所有响应头
                        console.log(xhr.response);//响应体
                        result.innerHTML = xhr.response;
                    } else {
                    }
                }
            }
        })
</script>
//server.js
app.get('/server', (request, response) => { //其中/server表示路径http://127.0.0.1:8000/server为启动网址
    //设置响应头 设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');//表示任意类型头信息都可以接收
    //设置响应体
    response.send('HELLO AJAX');
    //使用指定的回调函数将 HTTP GET 请求路由到指定路径
});
```

![image-20230818212406503](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230818212406503.png)

![image-20230818212606639](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230818212606639.png)

![image-20230818212521044](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230818212521044.png)

#### （7）POST请求

1、post请求的特殊请求头1——表示携带请求体是xhr.send('a=200&b=300&c=400')类型

  **xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')**

ajax-post-----在服务器端加上：解析post请求中以urlencoded形式编码的参数

( xhr.send('a=200&b=300&c=400');)

 **app.use(express.urlencoded({extended:true}))**   

2、post请求的特殊请求头2——表示携带请求体是xhr.send(JSON.Stringify({name:'张三',age:18}))类型

  **xhr.setRequestHeader('Content-Type', 'application/json')**

ajax-post-----在服务器端加上：解析post请求中以json形式编码的参数

 **app.use(express.json())**   

**3、form-post:form表单的post请求不用设置urlencoded，是因为form表单会自动加上这个特殊的请求头**

鼠标经过响应请求返回请求体

![image-20230818212735893](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230818212735893.png)

```js
 <div id="result"></div>
 <script>
       const result = document.querySelector('#result');
       result.addEventListener("mouseover", function () {
       // console.log("test");
       const xhr = new XMLHttpRequest();
       xhr.open('POST', 'http://127.0.0.1:8000/server');
       //设置请求头
       xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
       xhr.setRequestHeader('name', 'hujh');//后台显示该值为未预先定义的值，报错
       xhr.send('a=200&b=300&c=400');
        // xhr.send('a:200&b:300&c:400');
        //xhr.send('1234567654321');
       xhr.onreadystatechange = function () {
           if (xhr.readyState === 4) {
               if (xhr.status >= 200 && xhr.status < 300) {
                   //处理服务端返回结果
                   result.innerHTML = xhr.response;
                }
          }
       }
  });
</script>
//可以接收任意类型的请求  GET POST OPTIONS
app.all('/server', (request, response) => { 
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    response.send('HELLO AJAX POST');
});

```

![image-20230818212851843](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230818212851843.png)

![image-20230818212919758](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230818212919758.png)

#### (8) 解决IE发送get请求缓存问题

在重复发送网络请求时，由于IE浏览器是使用强缓存，当你的url没有变化时，IE默认接收的数据不变，走缓存，以至于你在服务器端修改了数据，IE检测不到，此时只需要在发送请求参数中加上时间戳，欺骗浏览器url是变化的。

注意：IE浏览器是不接受模板字符串的

![image-20240106210841054](D:\typora_photo\image-20240106210841054.png)

#### （9）取消上一次请求-----网络卡顿

**利用防抖节流解决不了，因为有可能是网络问题造成，无法估测到达服务器的时间。**

![image-20240107112216298](D:\typora_photo\image-20240107112216298.png)

![image-20240107112237837](D:\typora_photo\image-20240107112237837.png)

##### xhr方法：

关于xhr.abort（）：

（1）如果来得及，半路取消，请求根本没有到达服务器

（2）如果来不及，拒之门外，请求已经到达服务器，且服务器已经给出回应

（3）也存在根本不起作用的情况

##### axios方法：

（1）使用 CancelToken，在请求配置中直接提供 `cancelToken` 属性来关联取消标记，利用source.cancel('请求取消的原因');取消请求

（2）使用AbortController，在请求配置中提供  singal: controller.signal关联控制器controller和请求，当调用 controller.abort()取消请求时，会向关联controller控制器的请求发送一个取消信号，请求就会自动取消掉了。

**代码实现：**

##### 验证码问题

点击验证码10次，只要返回一次就行，怎么办呢？

取巧办法：在按钮点击一次后禁用60秒

真正解决办法：

```javascript
//xhr实现
let btn = document.getElementById('btn')
    let lastXhr
    btn.onclick = function () {
      if (lastXhr) lastXhr.abort()
      lastXhr = getCode()
    }

    function getCode() {
      let xhr = new XMLHttpRequest()
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
          console.log('验证码是：', xhr.response)
        }
      }
      xhr.open('get', 'http://localhost:3000/get_verify_code')
      xhr.send()
      return xhr
  }
//server.js
const express = require('express')
const app = express()
//使用内置中间件去解析post请求中以urlencoded形式编码的参数
app.use(express.urlencoded({extended:true}))
//暴露静态资源
app.use(express.static(__dirname+'/public'))

app.get('/get_verify_code',(req,res)=>{
  console.log('有人找我要验证码了')
  setTimeout(()=>{
    let code = Math.floor(Math.random()*8999 + 1000)
    res.send(code.toString())
  },1000)
})

app.listen(3000,(err)=>{
  if (err) console.log(err)
  else {
    console.log('兄弟不要不用编译器打开页面，会产生跨域问题')
    console.log('练习取消ajax请求的地址为：http://localhost:3000/code.html')
  }
})
```

```javascript
//axios实现方式一
let btn = document.getElementById('btn')
    let source
    btn.onclick = function () {
      if (source) source.cancel('请求取消的原因');
      source = getCode()
    }

    function getCode() {
      const source = axios.CancelToken.source()
      axios.get('http://localhost:3000/get_verify_code', {
        cancelToken: source.token
      }).then(response => {
        console.log(response.data);
      }).catch(error => {
        console.log(error);
      });
      return source
    }
//axios实现方式二
 let controller = null
    btn.onclick = function () {
      controller && controller.abort()
      controller = new AbortController();
      try {
        axios.get('http://localhost:3000/get_verify_code?', {
          singal: controller.signal
        })
          .then(response => {
            console.log(response.data);
          }).catch(error => {
            console.log(error);
          });
      } catch (error) {
        console.log('abort');
      }
    }
```

**注意：**

Math.random()的使用：要获得1000-9999之间的随机数

```js
Math.random()*8999+1000
Math.random()是获取0-1之间的随机数，当Math.random()是0时，就是1000，当Math.random()是1时就是8999+1000=9999
```



### 10.express

#### (1) 介绍

Express 是一个简洁而灵活的 [node.js](https://baike.baidu.com/item/node.js/7567977?fromModule=lemma_inlink) [Web应用框架](https://baike.baidu.com/item/Web应用框架/4262233?fromModule=lemma_inlink), 提供一系列强大特性帮助你创建各种Web应用。

#### (2）Express 框架核心特性：

可以设置中间件来响应 HTTP 请求。

定义了路由表用于执行不同的 HTTP 请求动作。

可以通过向模板传递参数来动态渲染 HTML 页面。

#### （3）参数

```js
//发送 HTTP 响应。body 参数可以是 Buffer 对象、String、对象、Boolean 或 Array。
res.send([body])
```

```js
//将响应 Location HTTP 标头设置为指定的 path 参数。
res.location(path)
```

```js
//在给定的 `path` 传输文件。设置文件路径并将文件发送到客户端, 根据文件名的扩展名设置 `Content-Type` 响应 HTTP 标头字段。 
res.sendFile(path [, options] [, fn])
app.get('/download',function(request, response) {
  response.sendFile(__dirname + '/files/myfile.txt');
});
这段代码会在服务器上查找位于 /files 目录下的 myfile.txt 文件，并将其发送到客户端。
注意，在使用 response.sendFile 方法时，文件路径必须是绝对路径。如果使用相对路径，可以使用 __dirname 变量，它会返回当前执行脚本所在的目录的绝对路径。
```

```js
//结束响应过程。用于在没有任何数据的情况下快速结束响应。 如果你需要用数据响应，请改用 res.send() 和 res.json() 等方法。
res.end([data] [, encoding])
```



### 11.解决 IE 缓存问题

问题：在一些浏览器中(IE),由于缓存机制的存在，ajax 只会发送的第一次请求，剩余多次请求不会在发送给浏览器而是直接加载缓存中的数据。

什么是AJAX GET请求缓存问题呢？

- **在HTTP协议中是这样规定get请求的：get请求会被缓存起来。**
- 发送AJAX GET请求时，在同一个浏览器上，前后发送的AJAX请求路径一样的话，对于低版本的IE来说，第二次的AJAX GET请求会走缓存，不走服务器。

**POST请求在HTTP协议中规定的是：POST请求不会被浏览器缓存。**

GET请求缓存的优缺点：

- 优点：直接从浏览器缓存中获取资源，不需要从服务器上重新加载资源，速度较快，用户体验好。
- 缺点：**无法实时获取最新的服务器资源。**

如果是低版本的IE浏览器，怎么解决AJAX GET请求的缓存问题呢？

- 浏览器的缓存是根据url 地址来记录的，所以我们只需要修改url 地址即可避免缓存问题

```js
xhr.open("get","http://127.0.0.1:8000/ie?t="+Date.now());
//即在请求网址后面加上？t="+Date.now()
```

- 可以在请求路径url后面添加一个时间戳，这个时间戳是随时变化的。所以每一次发送的请求路径都是不一样的，这样就不会走浏览器的缓存问题了。
- 可以采用时间戳："url?t=" + new Date().getTime()
- 或者可以通过随机数："url?t=" + Math.random()
- 也可以随机数+时间戳....

### 12.请求超时与网络异常设置

```js
// 超时设置 （2秒）
xhr.timeout = 2000;//表示2s后请求没有结果就取消请求。自动取消
// 超时回调
xhr.ontimeout = function(){
	alert('网络超时，请稍后重试')
}
// 网络异常回调
xhr.onerror = function(){
	alert('网络异常，请稍后重试')
}
```

### 13.取消请求

```javascript
// 手动取消
xhr.abort()
```

示例：

```javascript
<button>点击发送</button>
<button>点击取消</button>
<script>
     const btns = document.querySelectorAll('button');
     let xhr = null;
     btns[0].addEventListener("click", function () {
         xhr = new XMLHttpRequest();
         xhr.open("GET", 'http://127.0.0.1:8000/delay');
         xhr.send();
     })
     //abort 
     btns[1].onclick = function () {
         xhr.abort();
}
</script>
```

### 14.请求重复发送问题

定义一个变量用于标识是否正在发送AJAX请求

```js
<button>点击发送</button>
<script>
    const btns = document.querySelectorAll('button');
    let xhr = null;
    //标识变量
    let isSending = false;//是否正在发送AJAX请求
    btns[0].addEventListener("click", function () {
        if (isSending) {
            xhr.abort(); //如果正在发送就取消请求，创建一个新的请求
        }
    xhr = new XMLHttpRequest();
    //修改标识变量
    isSending = true;
    xhr.open("GET", 'http://127.0.0.1:8000/delay');
    xhr.send();
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
            isSending = false;
         }
    }
})
</script>
```

### 15.API总结

```php
XMLHttpRequest()：创建 XHR 对象的构造函数
status：响应状态码值，如 200、404
statusText：响应状态文本，如 ’ok‘、‘not found’
readyState：标识请求状态的只读属性 0-1-2-3-4
onreadystatechange：绑定 readyState 改变的监听
responseType：指定响应数据类型，如果是 ‘json’，得到响应后自动解析响应
response：响应体数据，类型取决于 responseType 的指定
timeout：指定请求超时时间，默认为 0 代表没有限制
ontimeout：绑定超时的监听
onerror：绑定请求网络错误的监听
open()：初始化一个请求，参数为：(method, url[, async])
send(data)：发送请求
abort()：中断请求 （发出到返回之间）
getResponseHeader(name)：获取指定名称的响应头值
getAllResponseHeaders()：获取所有响应头组成的字符串
setRequestHeader(name, value)：设置请求头
```

### 16.jQuery的AJAX请求

#### (1)完整版写法

使用jquery发送ajax请求的几个重要参数：
   *     1.url：请求的地址
   *     2.method：请求的方式
   *     3.data:携带的数据
   *     4.success:成功的回调
   *     5.error:失败的回调
   *     备注：jquery的ajax底层实际上是对xhr的高级封装

```javascript
 //完整写法
//使用jquery发送get请求
      $.ajax({
        url: 'http://localhost:3000/test_get',
        //发送请求的方法
        method: 'get',
        //发送请求携带的数据
        data: { name: 'kobe', age: 18 },
        //成功的回调
        success: (result) => {
          console.log(result)
        },
        //失败的回调
        error: (err) => {
          console.log(err)
        }
  })
```

```javascript
//精简写法
      $.get('http://localhost:3000/test_get', { name: 'kobe', age: 18 }, (data,statusText,xhr) => {
        console.log(data,statusText,xhr)
        //data:返回的数据
        //statusText:返回响应状态success和fail
        //xhr:xhr对象
      })
//另一种
 $.get('http://localhost:3000/test_get', { name: 'kobe', age: 18 }, (data) => {
        console.log(data)
})
```

GET和POST的参数对比：GET参数在Name后面，而POST参数在payload(Headers)中

![image-20230818195429017](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230818195429017.png)

#### (2)get请求

```javascript
$.get(url, [data], [callback], [type])
```

- url:请求的URL 地址
- data:请求携带的参数
- callback:载入成功时回调函数
- type:设置返回内容格式，xml, html, script, json, text, _default

#### （3）post请求

```javascript
$.post(url, [data], [callback], [type])
```

- url:请求的URL 地址
- data:请求携带的参数
- callback:载入成功时回调函数
- type:设置返回内容格式，xml, html, script, json, text, _default

#### （4）GET与POST请求

```js
 $('button').eq(0).click(function () {
     $.get('http://127.0.0.1:8000/jquery-server', { a: 100, b: 200 }, function (data) {
     console.log(data);
}, 'json');
})

$('button').eq(1).click(function () {
    $.post('http://127.0.0.1:8000/jquery-server', { a: 100, b: 200 }, function (data) {
    console.log(data);
});
})
//jQuery服务
app.all('/jquery-server', (request, response) => { 
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    const data = { name: '小哈' };
    response.send(JSON.stringify(data));
});
```

#### （5）AJAX请求---延时响应

```js
$('button').eq(2).click(function () {
    $.ajax({
        url: 'http://127.0.0.1:8000/delay',
        data: { a: 100, b: 200 },
        type: 'GET',
        //响应体结果
        dataType: 'json',
        //成功回调
        success: function (data) {
            console.log(data);
        },
        //超时时间
        timeout: 2000,
        error: function () {
            console.log('error出错了');
        },
         headers: {
             c: 300,
             d: 400,
         }
});
    
 //超时与网络异常
app.get('/delay', (request, response) => { //其中/server表示路径http://127.0.0.1:8000/server为启动网址
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    setTimeout(() => {
        response.send('延时响应');
    }, 3000);

});
```

![image-20230819100833495](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819100833495.png)

![image-20230819100818025](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819100818025.png)

#### （6）AJAX请求---正常响应

```js
$('button').eq(2).click(function () {
    $.ajax({
        url: 'http://127.0.0.1:8000/delay',
        data: { a: 100, b: 200 },
        type: 'GET',
        //响应体结果
        dataType: 'json',
        //成功回调
        success: function (data) {
            console.log(data);
        },
        //超时时间
        timeout: 2000,
        error: function () {
            console.log('error出错了');
        },
        headers: {
            c: 300,
            d: 400
        }
    });
})
//jQuery服务
app.all('/jquery-server', (request, response) => { 
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    const data = { name: '小哈' };
    response.send(JSON.stringify(data));
});
```

![image-20230819100652073](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819100652073.png)

![image-20230819100734395](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819100734395.png)

### 16.axios请求

#### （1）axios介绍

Axios 是一个基于 *[promise](https://javascript.info/promise-basics)* 网络请求库，作用于[`node.js`](https://nodejs.org/) 和浏览器中。 它是 *[isomorphic](https://www.lullabot.com/articles/what-is-an-isomorphic-application)* 的(即同一套代码可以运行在浏览器和node.js中)。在服务端它使用原生 node.js `http` 模块, 而在客户端 (浏览端) 则使用 XMLHttpRequests,   axios使用时获取的数据相对完整。

#### （2）参数介绍

##### 2-1   `baseURL` 

​       将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL。

```js
axios.defaults.baseURL = 'https://api.example.com';//全局 axios 默认值
```

##### 2-2  `params` 

是与请求一起发送的 URL 参数，必须是一个简单对象或 URLSearchParams 对象  

```js
params: {    ID: 12345  },
```

##### 2-3  headers

 自定义请求头 

```js
  headers: {'X-Requested-With': 'XMLHttpRequest'}
  headers: { name: 'atu',
             age: 20
           }
```

![image-20230819111150248](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819111150248.png)

##### 2-4  data

 `data` 是作为请求体被发送的数据  ,仅适用 'PUT', 'POST', 'DELETE 和 'PATCH' 请求方法 。

 在没有设置 `transformRequest` 时，则必须是以下类型之一: string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams 。

浏览器专属: FormData, File, Blob  。 Node 专属: Stream, Buffer 

```js
 data: {    firstName: 'Fred'  },
```

#### （3）GET请求

```js
axios.get(url[, config])
```

```js
axios.defaults.baseURL = 'http://127.0.0.1:8000';
const btns = document.querySelectorAll('button');
btns[0].onclick = function () {
    //GET请求
    axios.get('/axios-server', {
        params: {
            id: 100,
            vip: 7
        },
    //请求头信息
    headers: {
        name: 'atu',
        age: 20
    }
}).then(val => {
        console.log(val);//结果返回一个对象
   })
}
```

![image-20230819111621983](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819111621983.png)

#### (4)  POST请求

```js
axios.post(url[, data[, config]]) 
```

data:请求体； config:其他参数

```js
btns[1].onclick = function () {
    //GET请求
    axios.post('/axios-server', {
        username: 'admin',
        password: 'admin'
    }, {
        //url
    params: {
        id: 200,
        vip: 9
   },
    //请求头信息
   headers: {
        weight: 180,
        height: 170
    }
}).then(val => {
        console.log(val);
  })
}
//axios服务
app.all('/axios-server', (request, response) => { 
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    const data = { name: '小哈' };
    response.send(JSON.stringify(data));
});
```

![image-20230819112734532](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819112734532.png)

![image-20230819112831337](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819112831337.png)

#### （5）axios函数发送AJAX请求

以报文的形式书写

```js
btns[2].onclick = function () {
    axios({
        //请求方法
        method: 'POST',
        //url
        url: 'axios-server',
        params: {
            id: 200,
            vip: 9
        },
        //请求头信息
        headers: {
            a: 180,
            b: 170
        },
       data: {
           username: 'gh',
           password: 'ol'
       }
 }).then(val => {
        console.log(val);
        //响应状态码
        console.log(val.status);
        //响应字符串
        console.log(val.statusText);
        //响应头信息
        console.log(val.headers);
         //响应体
        console.log(val.data);
      })
}
```

![image-20230819113534336](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819113534336.png)

![image-20230819113545125](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819113545125.png)

![image-20230819113559351](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819113559351.png)

![image-20230819114316064](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819114316064.png)

### 17.fetch()函数发送AJAX请求

**注意：window内置的库**

#### （1）函数介绍

[`WindowOrWorkerGlobalScope`](http://mdn.asprain.cn/docs/Web/API/WindowOrWorkerGlobalScope)杂合体的`**fetch()**`方法开始从网络获取资源的过程，返回一个Promise，一旦响应可用，它就被满足。

[`fetch()`](http://mdn.asprain.cn/docs/Web/API/WindowOrWorkerGlobalScope/fetch)Promise只会在遇到网络错误时被驳回（这通常是因为存在权限问题或类似的问题）。[`fetch()`](http://mdn.asprain.cn/docs/Web/API/WindowOrWorkerGlobalScope/fetch)Promise不会因为HTTP错误（`404`等等）而被驳回。但是，必须有一个`then()`来检查[`Response.ok`](http://mdn.asprain.cn/docs/Web/API/Response/ok)属性和/或[`Response.status`](http://mdn.asprain.cn/docs/Web/API/Response/status)属性。

**`fetch()`方法的参数与[`Request()`](http://mdn.asprain.cn/docs/Web/API/Request/Request)构造器的参数是相同的。**

#### （2）函数的参数介绍

##### 2-1 语法

```js
const fetchResponsePromise = fetch(resource [, init])
```

##### 2-2 参数

resource：定义了你想要抓取的资源。它可以是：

- 一个[`USVString`](http://mdn.asprain.cn/docs/Web/API/USVString)，包含了你想要抓取的资源的方向URL。有些浏览器接受`blob:`和`data:`架构。
- 一个[`Request`](http://mdn.asprain.cn/docs/Web/API/Request)对象。

init：一个对象，它包含了任何你想要应用到请求上的自定义设置。可能的选项是：

```perl6
method： 请求的方法，例如：`GET`、`POST`。
headers：你想要添加到请求上的任何头，包含在Headers对象中，或一个利用ByteString字面量值实现的对象。
body：   添加到请求中的任何主体，这可以是Blob对象、BufferSource对象、FormData对象、URLSearchParams对         象、USVString对象或ReadableStream对象。
```

#### （3）示例

```js
<button>AJAX请求</button>
<script>
     const btn = document.querySelector('button');
     btn.onclick = function () {
         fetch('http://127.0.0.1:8000/fetch-server?vip=10', {
         //请求方法
         method: 'POST',
         //请求头
         headers: {
             name: 'atu'
         },
         //请求体
         body: 'username=admin&password=admin'
      }).then(response => {
             //return response.text();//{"name":"小哈"}
             return response.json();//{name: '小哈'}
      }).then(response => {
             console.log(response);
      });
}
</script>
//fetch服务
app.all('/fetch-server', (request, response) => {
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    const data = { name: '小哈' };
    response.send(JSON.stringify(data));
});
```

![image-20230819115119432](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819115119432.png)

​                                                                      console.log(response);返回值

![image-20230819115134455](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230819115134455.png)

### 18.跨域

**跨域：AJAX不能发送是一个错误说法，是AJAX可以发送但是无法获取服务端返回的数据**

#### （1）同源策略

- 同源策略(Same-Origin Policy)最早由Netscape 公司提出，是浏览器的一种安全策略
- 同源： 协议、域名、端口号必须完全相同
- 跨域： 违背同源策略就是**跨域**
- ajax是默认遵循同源策略的，不是同源策略无法发送请求。
- 即是页面的资源和响应都是来自同一个地址的

```js
<h1>哈哈哈</h1>
<button>点击获取用户数据</button>
<script>
      const btn = document.querySelector('button');
      btn.onclick = function () {
          const x = new XMLHttpRequest();
          x.open('GET', '/data');
          x.send();
          x.onreadystatechange = function () {
              if (x.readyState === 4) {
                  if (x.status >= 200 && x.status < 300) {
                      console.log(x.response);
                  }
              }
           }
    }
</script>
const express = require('express');
const app = express();
app.get('/home', (request, response) => {
    //响应一个页面
    response.sendFile(__dirname + '/index.html');
});
app.get('/data', (request, response) => {
    response.send('用户数据');
});
app.listen(9000, () => {
    console.log("服务已经启动....");
})
```

![image-20230820100817320](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820100817320.png)

![image-20230820100844139](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820100844139.png)

#### （2）跨域不同源

例如示例的axios请求中，其html跳转网址为D盘下的一个文件，该html能够显示出页面资源，而响应路径是

http://127.0.0.1:8000/axios-server，此时页面加载的资源是响应体response的内容。

#### （3） 如何解决跨域JSONP

##### 2-1   JSONP 是什么

JSONP(JSON with Padding)，是一个非官方的跨域解决方案，纯粹凭借程序员的聪明
才智开发出来，只支持get 请求。

##### 2-2   JSONP 怎么工作的？

在网页有一些标签天生具有跨域能力，比如：img link iframe script。
JSONP 就是利用script 标签的跨域能力来发送请求的。

##### 2-3 JSONP的使用

```js
//1.动态的创建一个script 标签
var script = document.createElement("script");

//2.设置script 的src，设置回调函数
script.src = "http://localhost:3000/testAJAX?callback=abc";
function abc(data) {
	alert(data.name);
};

//3.将script 添加到body 中
document.body.appendChild(script);

//4.服务器中路由的处理
router.get("/testAJAX" , function (req , res) {
	console.log("收到请求");
	var callback = req.query.callback;
	var obj = {
		name:"孙悟空",
		age:18
	}
	res.send(callback+"("+JSON.stringify(obj)+")");
});
```

##### 2-3 示例1

resopnse返回结果为函数的调用，而实参是想给客户端返回的数据，通过返回结果的js语句获得返回值

```js
<div id="result"></div>
<!--两个src都可以访问到页面，说明script可以跨域-->
<!--<script src="app.js"></script> -->
<script>
    //处理数据
 function handle(data) {
    const result = document.getElementById('result');
    result.innerHTML = data.name;
}
</script>
<!--<script src="http://127.0.0.1:5500/%E8%B7%A8%E5%9F%9F/JSONP/app.js"></script>-->
<script src="http://127.0.0.1:8000/jsonp-server"></script>

//JSONP服务 server.js
app.all('/jsonp-server', (request, response) => { 
    //response.send('console.log("hello")');
    const data = {
        name: '哈哈哈'
    };
    let str = JSON.stringify(data);
    response.end(`handle(${str})`);
});
```

![image-20230820102438289](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820102438289.png)

##### 2-4 示例2

```js
<div id="result"></div>
<!--两个src都可以访问到页面，说明script可以跨域-->
<!--<script src="app.js"></script> -->
<script>
      //处理数据
  function handle(data) {
    const result = document.getElementById('result');
    result.innerHTML = data.name;
}
</script>
<script src="http://127.0.0.1:5500/%E8%B7%A8%E5%9F%9F/JSONP/app.js"></script>

//app.js
const data = {
    name: '哈哈哈'
};
handle(data);
```

![image-20230820102924338](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820102924338.png)

##### 2-5 原生JSONP跨域案例

输入用户名，向服务端发起请求，当输入框失去焦点时，就返回用户名已经存在，并把输入框颜色改为红色

```js
用户名：<input type="text" id="username">
<p></p>
<script>
    const input = document.querySelector('input');
    const p = document.querySelector('p');
    function handle(data) {
        input.style.border = 'red 1px solid';
        p.innerHTML = data.msg;
    }
    input.addEventListener("blur", function () {
        let username = this.value;
         //向服务端发送请求，检查用户名是否存在
         //创建script标签
         const script = document.createElement('script');
         script.src = 'http://127.0.0.1:8000/check-name';
         //将script标签插入文档中
         document.body.appendChild(script);
      })
</script>
//server.js
//检测用户名是否存在
app.all('/check-name', (request, response) => {
    const data = {
        exist: 1,
        msg: '用户名已经存在'
    };
    let str = JSON.stringify(data);
    response.send(`handle(${str})`);
})
```

##### 2-6 jquery中使用JSONP

jQuery中的$.getJSON( )方法函数主要用来**从服务器加载json编码的数据**，它使用的是GET HTTP请求。要获得一个json文件的内容，就可以使用$.getJSON()方法，这个方法会在取得相应文件后对文件进行处理，并将处理得到的JavaScript对象提供给代码.

使用方法如下：

```js
$.getJSON( url [, data ] [, success(data, textStatus, jqXHR) ] )
```

- url是必选参数，表示json数据的地址；
- data是可选参数，用于请求数据时发送数据参数；
- success是可参数，这是一个回调函数，用于处理请求到的数据。

###### 示例 注意getJSON中的url需要加上?callback=?

```js
<button>点击发送</button>
<div id="result"></div>
<script>
 $('button').eq(0).click(function () {
    $.getJSON('http://127.0.0.1:8000/jquery-jsonp-server?callback=?', function (data) {
        $('#result').html(
            `名称:${data.name},<br>
              校区:${data.city}`
          )
     });
 });
</script>
//server.js   jquery-jsonp
app.all('/jquery-jsonp-server', (request, response) => {
    const data = {
        name: '张三',
        city: ['北京', '上海', '南京']
    };
    let str = JSON.stringify(data);
    //接收callback参数
    let cb = request.query.callback;
    response.send(`${cb}(${str})`);
})
```

![image-20230820114506785](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820114506785.png)

![image-20230820114525077](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820114525077.png)

#### (4)  CORS

https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS

##### 4-1CORS 是什么？

CORS（Cross-Origin Resource Sharing），跨域资源共享。CORS 是官方的跨域解决方
案，它的特点是不需要在客户端做任何特殊的操作，完全在服务器中进行处理，支持
get 和post 请求。跨域资源共享标准新增了一组HTTP 首部字段，允许服务器声明哪些
源站通过浏览器有权限访问哪些资源

##### 4-2 CORS 怎么工作的？

CORS 是通过设置一个响应头来告诉浏览器，该请求允许跨域，浏览器收到该响应
以后就会对响应放行。

##### 4-3 http响应头部字段

- `Access-Control-Allow-Origin` 参数指定了单一的源，告诉浏览器允许该源访问资源。

- Access-Control-Allow-Headers 将指定标头放入允许列表中，供浏览器的 JavaScript 代码获取。

在跨源访问时，`XMLHttpRequest` 对象的 [`getResponseHeader()`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/getResponseHeader) 方法只能拿到一些最基本的响应头，Cache-Control、Content-Language、Content-Type、Expires、Last-Modified、Pragma，如果要访问其他头，则需要服务器设置本响应头。

- Access-Control-Allow-Methods   标头字段指定了访问资源时允许使用的请求方法

##### 4-4 示例

```js
<button>点击发送请求</button>
<div id="result"></div>
<script>
      const btn = document.querySelector('button');
      const result = document.querySelector('button');
        btn.onclick = function () {
            const x = new XMLHttpRequest();
            x.open('GET', 'http://127.0.0.1:8000/cors-server');
            x.send();
            x.onreadystatechange = function () {
                if (x.readyState === 4) {
                    if (x.status >= 200 && x.status < 300) {
                        console.log(response);

                    }
                }
            }
  }
//server.js
//cors服务
app.all('/cors-server', (request, response) => {
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    response.setHeader('Access-Control-Allow-Methods', '*');
    //只允许http://127.0.0.1:5500端口发送请求
    //response.setHeader('Access-Control-Allow-Origin', 'http://127.0.0.1:5500');
    response.send('HELLO CORS');
});
```

![image-20230820134944590](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230820134944590.png)

## 附录：HTTP状态信息

### 1: 信息

| 消息:                   | 描述:                                                        |
| :---------------------- | :----------------------------------------------------------- |
| 100 Continue            | 服务器仅接收到部分请求，但是一旦服务器并没有拒绝该请求，客户端应该继续发送其余的请求。 |
| 101 Switching Protocols | 服务器转换协议：服务器将遵从客户的请求转换到另外一种协议。   |

### 2: 成功

| 消息:                             | 描述:                                                        |
| :-------------------------------- | :----------------------------------------------------------- |
| 200 OK                            | 请求成功（其后是对GET和POST请求的应答文档。）                |
| 201 Created                       | 请求被创建完成，同时新的资源被创建。                         |
| 202 Accepted                      | 供处理的请求已被接受，但是处理未完成。                       |
| 203 Non-authoritative Information | 文档已经正常地返回，但一些应答头可能不正确，因为使用的是文档的拷贝。 |
| 204 No Content                    | 没有新文档。浏览器应该继续显示原来的文档。如果用户定期地刷新页面，而Servlet可以确定用户文档足够新，这个状态代码是很有用的。 |
| 205 Reset Content                 | 没有新文档。但浏览器应该重置它所显示的内容。用来强制浏览器清除表单输入内容。 |
| 206 Partial Content               | 客户发送了一个带有Range头的GET请求，服务器完成了它。         |

### 3: 重定向

| 消息:                  | 描述:                                                        |
| :--------------------- | :----------------------------------------------------------- |
| 300 Multiple Choices   | 多重选择。链接列表。用户可以选择某链接到达目的地。最多允许五个地址。 |
| 301 Moved Permanently  | 所请求的页面已经转移至新的url。                              |
| 302 Found              | 所请求的页面已经临时转移至新的url。                          |
| 303 See Other          | 所请求的页面可在别的url下被找到。                            |
| 304 Not Modified       | 未按预期修改文档。客户端有缓冲的文档并发出了一个条件性的请求（一般是提供If-Modified-Since头表示客户只想比指定日期更新的文档）。服务器告诉客户，原来缓冲的文档还可以继续使用。 |
| 305 Use Proxy          | 客户请求的文档应该通过Location头所指明的代理服务器提取。     |
| 306 *Unused*           | 此代码被用于前一版本。目前已不再使用，但是代码依然被保留。   |
| 307 Temporary Redirect | 被请求的页面已经临时移至新的url。                            |

### 4: 客户端错误

| 消息:                             | 描述:                                                        |
| :-------------------------------- | :----------------------------------------------------------- |
| 400 Bad Request                   | 服务器未能理解请求。                                         |
| 401 Unauthorized                  | 被请求的页面需要用户名和密码。                               |
| 402 Payment Required              | 此代码尚无法使用。                                           |
| 403 Forbidden                     | 对被请求页面的访问被禁止。                                   |
| 404 Not Found                     | 服务器无法找到被请求的页面。                                 |
| 405 Method Not Allowed            | 请求中指定的方法不被允许。                                   |
| 406 Not Acceptable                | 服务器生成的响应无法被客户端所接受。                         |
| 407 Proxy Authentication Required | 用户必须首先使用代理服务器进行验证，这样请求才会被处理。     |
| 408 Request Timeout               | 请求超出了服务器的等待时间。                                 |
| 409 Conflict                      | 由于冲突，请求无法被完成。                                   |
| 410 Gone                          | 被请求的页面不可用。                                         |
| 411 Length Required               | "Content-Length" 未被定义。如果无此内容，服务器不会接受请求。 |
| 412 Precondition Failed           | 请求中的前提条件被服务器评估为失败。                         |
| 413 Request Entity Too Large      | 由于所请求的实体的太大，服务器不会接受请求。                 |
| 414 Request-url Too Long          | 由于url太长，服务器不会接受请求。当post请求被转换为带有很长的查询信息的get请求时，就会发生这种情况。 |
| 415 Unsupported Media Type        | 由于媒介类型不被支持，服务器不会接受请求。                   |
| 416                               | 服务器不能满足客户在请求中指定的Range头。                    |
| 417 Expectation Failed            |                                                              |

### 5: 服务器错误

| 消息:                          | 描述:                                              |
| :----------------------------- | :------------------------------------------------- |
| 500 Internal Server Error      | 请求未完成。服务器遇到不可预知的情况。             |
| 501 Not Implemented            | 请求未完成。服务器不支持所请求的功能。             |
| 502 Bad Gateway                | 请求未完成。服务器从上游服务器收到一个无效的响应。 |
| 503 Service Unavailable        | 请求未完成。服务器临时过载或当机。                 |
| 504 Gateway Timeout            | 网关超时。                                         |
| 505 HTTP Version Not Supported | 服务器不支持请求中指明的HTTP协议版本。             |
