#                                                                 Promise

### 一、准备

1、回调函数：我们自己定义，我们没有调用，最后执行了

2、同步回调函数：立即在主线程上执行，不会放入回调队列中

​     例子：数组遍历相关的回调函数/Promise的executor函数

3、异步回调函数：不会立即执行，会放入回调队列中以后执行

​     例子：定时器回调/ajax回调/Promise的成功和失败的回调

**setTimeout本身不是一个回调函数，是其回调是一个异步回调，不是说setTimeout是一个异步回调**

### 二、Promise是什么

1、抽象表达：

​    （1）Promise是一门新技术（ES6提出的）

​    （2）Promise是JS中异步编程的新方案（旧方案——纯回调函数）

2、具体表达：

​     （1）从语法上来说，Promise是一个内置的构造函数，不是回调，是程序员自己new调用的

​     （2）从功能上来说，Promise的实例对象可以用来封装一个异步操作，并可以获得其成功/失败的值

```html
1.Promise不是回调，是一个内置的构造函数，是程序员自己new调用的
2.new Promise的时候，要传入一个回调函数，它是同步回调函数，会立即在主线程上执行，它被称为executor执行器函数
3.每个Promise实例对象都有3种状态：初始化(pending)、成功(fullfilled)、失败(rejected)
4.每个Promise实例在刚被new出来的那一刻，状态都是初始化pending
5.executor函数接收两个参数，它们都是函数，分别用形参resolve和reject接收
  （1）调用resolve会让Promise实例状态变为成功(fullfilled),t同时可以指定成功的value
  （2）调用reject会让Promise实例状态变为失败(rejected),同时可以指定成失败的reason
```

![image-20240104104911896](D:\typora_photo\image-20240104104911896.png)

![image-20240104104919879](D:\typora_photo\image-20240104104919879.png)

![image-20240104105137242](D:\typora_photo\image-20240104105137242.png)

![image-20240104105144632](D:\typora_photo\image-20240104105144632.png)



**注意：**一个promise指定多个成功/失败的回调函数，都会调用。（原因：then中成功和失败的回调会压入队列，当执行成功后，就一次从队列中取出成功的回调显示）

![image-20240104124908275](D:\typora_photo\image-20240104124908275.png)

![image-20240104124936340](D:\typora_photo\image-20240104124936340.png)

不能单从const x = new Promise()通过x看promise的实例，因为这个实例x刚开始初始状态都是pending，不会改变的，即使已经请求到数据了，是fulfilled了，但是状态不会逆转改变，只输出第一次的，并不是输出最终状态，所以要用.then()方法去实现

### 三、Promise的主要语法

-  **Promise构造函数**：new Promise (executor) {}

-  **executor函数**：是同步执行的，(resolve,reject) => {}

- **resolve函数：**调用resolve将Promise实例内部状态改为成功(fulfilled)。                                                                                       **reject函数：**   调用reject将Promise实例内部状态改为失败(rejected)

**说明:excutor函数会在Promise内部立即同步调用，异步代码放在excutor函数中。**

-  **Promise.prototype.then方法:**

  Promise实例,then(onFulfilled,onRejected)

​       onFulfilled:成功的回调函数(value) => {}       

​       onRejected:失败的回调函数(reason) => {}

​     **then()方法在还没有调用前是放在promise实例的队列身上，等到调用了再执行**

**特别注意(难点):then方法会返回一个新的Promise实例对象**

- **Promise.prototype.catch方法:**

  Promise实例.catch(onRejected)

  onRejected:失败的回调函数(reason) => {}

  说明:catch方法是then方法的语法糖，相当于:then(undefined,onRejected)

  **两个问题点：**

  ![image-20240104211936222](D:\typora_photo\image-20240104211936222.png)

  ![image-20240104213458151](D:\typora_photo\image-20240104213458151.png)

  ```html
  执行reject时，then方法和catch方法中的成功和失败的回调(简称一组回调)会一次放入队列，没有的回调为undefined，当执行k.then时，此时失败回调是undefined，会抛出错误uncaught，再执行catch中的回调。
  ```

  ![image-20240104165957759](D:\typora_photo\image-20240104165957759.png)

![image-20240104213358162](D:\typora_photo\image-20240104213358162.png)

```html
执行resolve时，then方法和catch方法中的成功和失败的回调会一次放入队列，没有的回调为undefined，当执行k.then时，此时成功回调是function，再执行catch中的成功回调undefined，不影响程序运行，控制台无输出。
```

![image-20240104213433645](D:\typora_photo\image-20240104213433645.png)

![image-20240104213347127](D:\typora_photo\image-20240104213347127.png)

- **Promise.resolve方法:**

  Promise.resolve(value)

  说明:用于快速返回一个状态为fulfilled或rejected的Promise实例对象

- **Promise.reject方法:**

  Promise.reject方法(reason)

  说明:用于快速返回一个状态为fulfilled或rejected的Promise实例对象

- Promise.all方法:

  Promise.all(promiseArr)

  promiseArr: 包含**n个Promise实例的****数组**

  说明:返回一个新的Promise实例，只有所有的promise都成功才成功，只要有一个失败了就直接返回失败的value

  ![image-20240105113839998](D:\typora_photo\image-20240105113839998.png)

  ![image-20240105113816518](D:\typora_photo\image-20240105113816518.png)

  

  ![image-20240105113826166](D:\typora_photo\image-20240105113826166.png)

- Promise.race方法:

  Promise.race(promiseArr)

  promiseArr: 包含n个Promise实例的数组

  说明:返回一个新的Promise实例，**成功还是很失败?以最先出结果的promise为准**

### 四、Promise的几个关键问题

#### 1.如何改变一个Promise实例的状态?

```html
(1)执行resolve(value):如果当前是pending就会变为fulfilled
(2)执行reject(reason):如果当前是pending就会变为rejected
(3)执行器函数(executor)抛出异常:如果当前是pending就会变为rejected
```

第三点：通过引擎自动抛出异常或者编码异常验证，由于状态只能从pending转化，当执行了resolve后状态为fullfilled，不能再转换为rejected，所以不会调用失败了。

![image-20240105140630325](D:\typora_photo\image-20240105140630325.png)

![image-20240105143456625](D:\typora_photo\image-20240105143456625.png)

#### 2、改变Promise实例的状态和指定回调函数谁先谁后?

​     **都有可能，正常情况下是先指定回调再改变状态，但也可以先改状态再指定回调**

#### 3、如何先改状态再指定回调? 

​      延迟一会（设置一个定时器）再调用then()

#### 4、Promise实例什么时候才能得到数据?

- 如果先指定的回调，那当状态发生改变时，回调函数就会调用，得到数据
- 如果先改变的状态，那当指定回调时，回调函数就会调用，得到数据

#### 5、 Promise实例.then()返回的是一个[新的Promise实例]，它的值和状态由什么决定?

​      1.简单表达:由then()所指定的回调函数执行的结果决定

​      2.详细表达:

​        (1)如果then所指定的回调返回的是**非Promise值a**:

​             那么[新Promise实例]状态为:**成功(fulfilled)，成功的value为a**

​        (2)如果then所指定的回调返回的是一个**Promise实例p**:

​             那么[新Promise实例]的**状态、值，都与p一致**

​        (3)如果then所指定的回调**抛出异常**:

​             那么[新Promise实例]状态为**rejected,reason为抛出的那个异常的值**

![image-20240105145943197](D:\typora_photo\image-20240105145943197.png)

**.then()方法的链式调用**

![image-20240105150727981](D:\typora_photo\image-20240105150727981.png)

![image-20240105150741463](D:\typora_photo\image-20240105150741463.png)

#### 6、解决回调地狱问题

看 05纯回调封装一个ajax

#### 7、中断promise链

(1)当使用promise的then链式调用时，在中间中断，不再调用后面的回调函数。达到当一次请求成功后再进行下一次

(2)办法:**在失败的回调函数中返回一个pendding状态的Promise实例。**

![image-20240105163124046](D:\typora_photo\image-20240105163124046.png)

![image-20240105163132423](D:\typora_photo\image-20240105163132423.png)

![image-20240105164036381](D:\typora_photo\image-20240105164036381.png)

![image-20240105163749672](D:\typora_photo\image-20240105163749672.png)

#### 8、promise的错误穿透

(1)当使用promise的then链式调用时，**可以在最后用catch指定一个失败的回调**
(2)前面任何操作出了错误，都会传到最后失败的回调中处理了备注:如果不存在then的链式调用，就不需要考虑then的错误穿透。

![image-20240105165414666](D:\typora_photo\image-20240105165414666.png)

![image-20240105165422620](D:\typora_photo\image-20240105165422620.png)

![image-20240105203247142](D:\typora_photo\image-20240105203247142.png)

#### 9、promise的优势

**1.指定回调函数的方式更加灵活**
    旧的:必须在启动异步任务前指定
     promise:启动异步任务 => 返回promise对象 => 给promise对象绑定回调函数(可以在异步任务结束后指定)
**2.支持链式调用，可以解决回调地狱问题**

  （1）什么是回调地狱:
           **回调函数嵌套调用，外部回调函数异步执行的结果是嵌套的回调函数执行的条件**
  （2）回调地狱的弊病:
           代码不便于阅读、不便于异常的处理(回调地狱问题：代码结构不友好，不便于调试错误)
  （3）一个不是很优秀的解决方案:
           then的链式调用
  （4）终极解决方案:
            async/await(底层实际上依然使用then的链式调用)

### 五、async与await

#### 1、async修饰的函数

​      **函数的返回值为promise对象**
​     Promise实例的结果由async函数执行的返回值决定

#### 2、await表达式

await右侧的表达式一般为Promise实例对象，但也可以是其它的值

- 如果表达式是promise对象，await后的返回值是promise成功的值

- **如果表达式是其它值，直接将此值作为await的返回值**

  ![image-20240105214052834](D:\typora_photo\image-20240105214052834.png)

#### 3、注意:

await必须写在async函数中，但async函数中可以没有await
如果await的promise失败了，就会抛出异常，需要通过try...catch来捕获处理



![image-20240105213109819](D:\typora_photo\image-20240105213109819.png)

直接用一个变量接住promise的返回值是不行的，当是reject时会找失败的回调，没有回调就返回uncaught，并且状态保持最初始的pending，通过then()方法才可以调用

![image-20240105213119014](D:\typora_photo\image-20240105213119014.png)

#### 4、await原理

![image-20240106102722749](D:\typora_photo\image-20240106102722749.png)

#### 5、宏队列与微队列

宏队列：[宏任务1，宏任务2.....] 例如settimeout里面的回调任务

微队列：[微任务1，微任务2.....] 例如promise的resolve和reject任务

**要执行才进队列，如果是先指定回调再改变状态就是将回调先缓存在自身，等要用的时候再调用**

规则：每次要执行宏队列里的一个任务之前，先看微队列里是否有待执行的微任务

 （1）如果有，先执行微任务

（2）如果没有，按照宏队列里任务的顺序，依次执行。



##### 一个小例子

```js
 const p1 = new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve('a')
            }, 1000);
})
```

**当settimeout里面的定时器到点时才将回调任务推入宏队列，在定时器还没有到点之前是将resolve('a')放在浏览器的定时器模块由该模块进行管理**

##### 一个经典面试题

```javascript
 setTimeout(() => {
            console.log("0")
        }, 0)
        new Promise((resolve, reject) => {
            console.log("1")
            resolve()
        }).then(() => {
            console.log("2")
            new Promise((resolve, reject) => {
                console.log("3")
                resolve()
            }).then(() => {
                console.log("4")
            }).then(() => {
                console.log("5")
            })
        }).then(() => {
            console.log("6")
        })
        new Promise((resolve, reject) => {
            console.log("7")
            resolve()
        }).then(
            () => {
                console.log('8');
            }
        )
```

分析：当第一个then()[2代表的那一个]推进队列，执行时，先输出2和3，然后resolve()，便将  console.log("4")推进队列，因为  console.log("4")还没有执行，所以后面的  console.log("5")还不能推进队列，只能挂在上一个then返回的新的promise实例身上，等待4调用完再推进队列执行。

当4推进队列时，2的then执行完了，此时就把6的then推进队列

![image-20240106110745169](D:\typora_photo\image-20240106110745169.png)

![image-20240106110414614](D:\typora_photo\image-20240106110414614.png)

### 六、Promise总结---面试回答









### 零散知识点：

#### 1、包管理器对比

（1）cnpm

​        安装一个包：cnpm i jquery

​        卸载一个包：cnpm remove jquery

​    **cnpm当卸载一个包时，所有的包会被清除**

![image-20240104145231283](D:\typora_photo\image-20240104145231283.png)

（2）npm 

​     当你初始化后起的包名与主流库相同例如jquery,就会出现其他库能安装，就是安装不了与你起的包名一样的库

（3）yarn：较好用，无上述两个问题

#### 2、对象属性值

当遇到将一个值作为对象的属性时用**对象[属性名]**的形式

![image-20240104135731517](D:\typora_photo\image-20240104135731517.png)

#### 3、事件循环

javascript的特点：单线程（同一个时间只能做一件事），解释性语言。

javascript脚本语言诞生使命——为处理页面中用户的交互，以及操作DOM而诞生的。比如我们对某个DOM元素进行添加和删除操作，不能同时进行，应该先进行添加，之后再删除。单线程意味着所有任务需要排队，前一个任务结束才会执行后一个任务。如果JS执行时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。

js执行机制：

> js任务分为同步任务和异步任务，同步任务都在主线程上执行，形成一个执行栈。异步任务是通过回调函数实现的。一般而言的异步任务分为以下三种：普通事件（click、resize）、资源加载（Load、error)、定时器（setInterval、setTimeout)。异步任务添加到任务队列（消息队列）中。

（1）先执行执行栈中的同步任务

（2）异步任务放入任务队列中

（3）一旦执行栈中的所有同步任务执行完毕，系统就好按照次序读取任务队列中的异步任务，于是被读取的异步任务结束

等待状态，进入执行栈，开始执行。
