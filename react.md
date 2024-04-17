#                               react教程

## 一、入门

### 1.1框架说明

### ![6JCTWHzQ5vCgtp7SBMrvzw](D:\typora_photo\6JCTWHzQ5vCgtp7SBMrvzw.png)

![image-20231227101747894](D:\typora_photo\image-20231227101747894.png)

![image-20231227102547128](D:\typora_photo\image-20231227102547128.png)

![image-20231227103018221](D:\typora_photo\image-20231227103018221.png)

##### react高效的原因

（1）使用向虚拟DOM，不总是直接操作页面的真实DOM

（2）DOM Diffing算法，最小化页面重绘

### 1.2 React的基本使用

![image-20231227110023362](D:\typora_photo\image-20231227110023362.png)

#### 1.2.1 写一个hello react

相关 JS 库：

- `react.development.js` ：React 核心库
- `react-dom.development.js` ：提供 DOM 操作的 React 扩展库
- `babel.min.js` ：解析 JSX 语法，转换为 JS 代码

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>hello react</title>
</head>
<body>
    <div id="test"></div>
    <!-- 引入核心库 -->
    <script type="text/javascript" src="../js/react.development.js"></script>
    <!-- 引入react-dom，使react支持dom -->
    <script type="text/javascript" src="../js/react-dom.development.js"></script>
    <!-- 引入babel，将jsx转为js -->
    <script type="text/javascript" src="../js/babel.min.js"></script>
    <!-- 此处一定要写babel -->
    <script type="text/babel">
        //创建虚拟DOM
        const VDOM = <h1>hello react</h1>  //此处不用写引号，因为不是字符串，是jsx的写法
        //渲染虚拟DOM到页面
        // 导入核心库和扩展库后，会有 React 和 ReactDOM 两个对象
        ReactDOM.render(VDOM, document.getElementById('test'))
    </script>
</body>
</html>
```

#### 1.2.2 创建虚拟 DOM 的两种方式：JS 和 JSX

- 使用 JS 创建虚拟 DOM 比 JSX 繁琐
- JSX 可以让程序员更加简单地创建虚拟 DOM，相当于语法糖
- 最终 babel 会把 JSX 语法转换为 JS

示例代码

```js
//js创建
<body>
    <div id="test"></div>
    <!-- 引入核心库 -->
    <script type="text/javascript" src="../js/react.development.js"></script>
    <!-- 引入react-dom，使react支持dom -->
    <script type="text/javascript" src="../js/react-dom.development.js"></script>
    <!-- 此处一定要写babel -->
    <script type="text/javascript">
        //创建虚拟DOM
        //const VDOM=React.createElement(标签名，标签属性，标签内容)
        const VDOM = React.createElement('h1', {id:'title'},React.createElement('span',{},'hello react'))
        //渲染虚拟DOM到页面
        ReactDOM.render(VDOM,document.getElementById('test'))
    </script>
</body>

//jsx创建
<body>
    <div id="test"></div>
    <!-- 引入核心库 -->
    <script type="text/javascript" src="../js/react.development.js"></script>
    <!-- 引入react-dom，使react支持dom -->
    <script type="text/javascript" src="../js/react-dom.development.js"></script>
    <!-- 引入babel，将jsx转为js -->
    <script type="text/javascript" src="../js/babel.min.js"></script>
    <!-- 此处一定要写babel -->
    <script type="text/babel">
        //创建虚拟DOM
        //此处不用写引号，因为不是字符串，是jsx的写法
        const VDOM = (
            <h1 id="title">
                <span>hello react</span>
            </h1>  
        )
        //渲染虚拟DOM到页面
        ReactDOM.render(VDOM, document.getElementById('test'))
    </script>
</body>
```

#### 1.2.3 虚拟 DOM && 真实 DOM

关于虚拟 DOM：

1. 本质是 Object 类型的对象（一般对象）
2. 虚拟 DOM 比较“轻”，真实 DOM 比较“重”，因为虚拟 DOM 是 React 内部在用，无需真实 DOM 上那么多的属性。
3. 虚拟 DOM 最终会被 React 转化为真实 DOM，呈现在页面上。

```js
<body>
    <div id="test"></div>
    <div id="demo"></div> 
    <!-- 此处一定要写babel -->
    <script type="text/babel">
        //创建虚拟DOM
        //此处不用写引号，因为不是字符串，是jsx的写法
        const VDOM = (
            <h1 id="title">
                <span>hello react</span>
            </h1> 
        )
        //渲染虚拟DOM到页面
        ReactDOM.render(VDOM, document.getElementById('test'))
        const TDOM=document.getElementById('demo')
        console.log('虚拟DOM',VDOM);
        console.log('真实DOM',TDOM);
        console.log(typeof VDOM); //Object
        console.log(VDOM instanceof Object);//true
    </script>
</body>
```

![image-20231227131724387](D:\typora_photo\image-20231227131724387.png)

### 1.3 JSX简介

- 全称：JavaScript XML
- React 定义的类似于 XML 的 JS 扩展语法；本质是 `React.createElement()` 方法的语法糖
- 作用：简化创建虚拟 DOM

#### JSX 语法规则

- 定义虚拟 DOM 时，不要写引号

  ```js
  const VDOM = (
              <h1 id="title">
              <span>hello react</span>
              </h1> 
          )
  ```

- 标签中混入 JS 表达式需要使用 `{}`

  ```js
  const myID = 'AtguiGu'
          const myData = 'Hello ReAct'
          const VDOM = (
              <h2 id={myID.toLowerCase()}>
                  <span>{myData.toLowerCase()}</span>
              </h2>
          )
  ```

- 指定类名不用 `class`，使用 `className`

  ```js
  const VDOM = (
       <h2 className="title" id={myID.toLowerCase()}>
       <span>{myData.toLowerCase()}</span>
       </h2>
   )
  ```

- 内联样式，使用 `style={{ key: value }}` 的形式

- 只能有一个根标签

- 标签必须闭合，单标签结尾必须添加 `/`：`<input type="text" />`

- 标签首字母小写，则把标签转换为 HTML 对应的标签，若没有，则报错

- 标签首字母大写，则渲染对应组件，若没有定义组件，则报错

综合示例

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>jsx语法规则</title>
    <!-- 引入核心库 -->
    <script type="text/javascript" src="../js/react.development.js"></script>
    <!-- 引入react-dom，使react支持dom -->
    <script type="text/javascript" src="../js/react-dom.development.js"></script>
    <!-- 引入babel，将jsx转为js -->
    <script type="text/javascript" src="../js/babel.min.js"></script>
    <style>
        .title {
            background-color: yellowgreen;
            width: 200px;
        }
    </style>
</head>
<body>
    <div id="test"></div>
    <script type="text/babel">
        const myID = 'AtguiGu'
        const myData = 'Hello ReAct'
        const VDOM = (
            <div>
                <h2 className="title" id={myID.toLowerCase()}>
                <span style={{color:'red',fontSize:'30px'}}>{myData.toLowerCase()}</span>
            </h2>
            <input type="text"></input>
            </div>
        )
        ReactDOM.render(VDOM, document.getElementById('test'))
    </script>
</body>
</html>
```

#### JSX 例子

注意区分：**【JS 语句(代码)】** 与 **【JS 表达式】**：

1、表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方

```js
a
a+b
demo(1)
arr.map()
function test () {}
```

2、语句(代码)：

```js
if(){}
for(){}
switch(){case:xxxx}
```

![image-20231227140735178](D:\typora_photo\image-20231227140735178.png)

```js
<body>
    <div id="test">
    </div>
    <script type="text/babel">
        const list=['Angular','React','Vue']
        const VDOM=(
            <div>
                <h1>前端js框架列表</h1>
                <ul>  
                {
                    list.map((item,index)=>{
                        return <li key={index}>{item}</li>
                    })   //标签中混入 JS 表达式需要使用 `{}`
                }
            </ul>
            </div>
        )
        ReactDOM.render(VDOM,document.getElementById('test'))
    </script>
</body>
```

需要设置唯一的key，否则会报错

![image-20231227141014441](D:\typora_photo\image-20231227141014441.png)

**注意**

Fragment 标签 就是一个简单的标签，在 react 项目中就充当组件根节点的 div 使用。只要使用 Fragment 标签，那么在 react 中渲染的时候，都会被自动忽略掉，不会被渲染。（可以看成是vue中的template）

![image-20240415215356978](D:/typora_photo/image-20240415215356978.png)

### 1.4 **模块与组件、模块化与组件化的理解**

#### 1.4.1 模块

（1）向外提供特定功能的js程序，一般就是一个js文件

（2）为什么要拆分成模块：随着业务逻辑增加，代码越来越多且 复杂

（3）作用：复用js,简化js的编写，提高js的运行效率

#### 1.4.2 组件

（1）用来实现局部功能效果的代码和资源的集合（html/css/js/video/图片资源等等）

（2）为什么要拆分成组件：一个界面的功能更复杂

（3）作用：复用编码，简化项目编码，提高运行效率

#### 1.4.3 模块化

当应用的js文件都以模块来编写，这个应用就是一个模块化的应用了

#### 1.4.4 组件化

当应用是以多组件的方式实现，这个应用就是一个组件化的应用了

## 二、React面向组件编程

### 2.1 基本理解和使用

#### 2.1.1 函数式组件

```html
 <div id="test"></div>
    <script type="text/babel">
        //1.创建函数式组件
        function MyComponent() {
            console.log(this);//undefined 因为babel编译后开启了严格模式
            return <h2>我是用函数定义的组件（适用于简单组件）</h2>
        }
    ReactDOM.render(<MyComponent/>,document.getElementById('test'))
    </script>
```

要点：

- 组件名称首字母必须大写，否则会解析成普通标签导致报错（[JSX 语法规则](https://brucecai55520.gitee.io/my-notes/#/React/React入门?id=jsx-语法规则)）
- 函数需返回一个虚拟 DOM
- 渲染组件时需要使用标签形式，同时标签必须闭合<demo/>

渲染组件的过程：

- React 解析标签，寻找对应组件，如果找不到就会报错
- 发现组件是函数式组件，则调用函数，将返回的虚拟 DOM 转换为真实 DOM ，并渲染到页面中

#### 2.2.2 类式组件

##### 2.1.2.1 类基础知识复习

总结:
1.类中的构造器不是必须写的，要对实例进行一些初始化的操作，如添加指定属性时才写。
2.如果A类继承了B类，且A类中写了构造器，那么A类构造器中的super是必须要调用的。
3.类中所定义的方法，都是放在了类的原型对象上，供实例去使用

```js
<script>
    //定义Person类
        class Person {
            //构造器中的this指向实例对象
            constructor(name, age) {
                this.name = name
                this.age = age
            }
            //speak 方法放在类的原型对象上，供给实例使用
            //通过person实例调用speak时，speak中的this指向Person的实例
            speak() {
                console.log(this);
                console.log(`我是${this.name}，我${this.age}了`);
            }
        }
        const p1 = new Person('张三', 13)
        const p2 = new Person('李四', 12)
        p1.speak()
        p2.speak()
        p1.speak.call({ a: '1', b: '2' })//改变this指向，实例身上就没有name和age了
   //定义Student类
        class Student extends Person {
            constructor(name, age, grade) {
                super(name, age)
                this.grade = grade
            }
            //重写继承父类的方法
            speak() {
                console.log(`我是${this.name}，我${this.age}了,我上${this.grade}了`);
            }
            study() {
                console.log('努力');
            }
        }
        const s1 = new Student('小张', 15, '大一')
        console.log(s1);
    </script>
```

![image-20231227163630652](D:\typora_photo\image-20231227163630652.png)

##### 2.1.2.2 类式组件说明

```js
<body>
    <div id="test"></div>
    <script type="text/babel">
        class MyComponent extends React.Component {
        //render是放在哪里的？—— MyComponent的原型对象上，供实例使用。
        //render中的this是谁？—— MyComponent的实例对象 <=> MyComponent组件实例对象
            render() {
                console.log('render中的this',this);
                return <h2>我是用类式定义的组件（适用于复杂组件）</h2>
            }
        }
        ReactDOM.render(<MyComponent />, document.getElementById('test'))
    </script>
</body>
```

组件渲染过程：

- React 解析组件标签，寻找组件
- 发现是类式组件，则 `new` 该类的实例对象，通过实例调用原型上的 `render` 方法
- 将 `render` 返回的虚拟 DOM 转为真实 DOM ，渲染到页面上

一般在react叫组件实例对象是类式组件因为函数严格模式下没有this，故没有实例。

### 2.2 组件(实例）三大属性----state

注意：三大核心出现在类式组件的实例对象身上

![image-20231227170551564](D:\typora_photo\image-20231227170551564.png)

#### 2.2.1 理解

1. state是组件对象最重要的属性, 值是对象(可以包含多个key-value的组合)

2. 组件被称为"状态机", 通过更新组件的state来更新对应的页面显示(重新渲染组件)

#### 2.2.2 强烈注意

1. 组件中render方法中的this为组件实例对象

2. 组件自定义的方法中this为undefined，如何解决？

​      a) 强制绑定this: 通过函数对象的bind()

​      b) 箭头函数

3. 状态数据，不能直接修改或更新，需要借助setState({})来更改

案例：点击切换炎热和凉爽

![image-20231228094747340](D:\typora_photo\image-20231228094747340.png)

完整版state

```js
<body>
    <div id="test"></div>
    <script type="text/babel">
        class Weather extends React.Component {
            //构造器-----调用了1次
            constructor(props) {
                console.log('constructor');
                super(props)
                this.state = { isHot: true,wind:'微风' }
                //解决changeWeather中this指向问题 方法二
                //this.changeWeather=this.changeWeather.bind(this)
            }
             //render函数-----调用了1+n次,1为初始化，n为每点一次调用一次即状态改变次数
            render() {
                console.log('render')
                return <h2 onClick={this.changeWeather.bind(this)}>今天天气很{this.state.isHot ? '炎热' : '凉爽'},{this.state.wind}</h2>
            }
             //changeWeather函数-----调用了n次
            changeWeather() { 
               //changeWeather是放在哪里的？——Weather的原型对象上，供实例使用。
               //由于changeWeather作为onClick的回调，所以不是通过实例，是直接调用
               //类中方法默认开启局部的严格模式，所以changeWeather中的this是undefined

               //状态state不能直接更改,下面这行就是直接更改
               // this.state.isHot=!isHot 错误写法
               
               //状态必须通过setState进行修改更新，且是更新时一种合并，不是替换
               const isHot=this.state.isHot
               this.setState({isHot:!isHot})  
            }
        }
        ReactDOM.render(<Weather/>, document.getElementById('test'))

        //绑定点击事件--繁琐法
        // const div = document.getElementById('test')
        // div.addEventListener('click', ()=> {
        //     alert('hhh')
        // })
    </script>
</body>
```

简化版state

```js
<body>
    <div id="test"></div>
    <script type="text/babel">
        class Weather extends React.Component {
            state = { isHot: true, wind: '微风' }
            render() {
                return <h2 onClick={this.changeWeather}>今天天气很{this.state.isHot ? '炎热' : '凉爽'},{this.state.wind}</h2>
            }
            //自定义方法——赋值语句+箭头函数 
            //Weather原型对象上就没有changeWeather,转而到实例对象身上了
            //箭头函数无this，找外层就是实例对象了
            changeWeather = () => {
                console.log(this);//weather实例
                const isHot = this.state.isHot
                this.setState({ isHot: !isHot })
            }
            //  changeWeather=function () { 
            //     console.log(this);//undefined
            // }
        }
        ReactDOM.render(<Weather />, document.getElementById('test'))
    </script>
</body>
```

### 2.3 组件三大属性----props

#### 2.3.1 理解

1. 每个组件对象都会有props(properties的简写)属性
2.  组件标签的所有属性都保存在props中

#### 2.3.2 作用

1. 通过标签属性从组件外向组件内传递变化的数据

2. 注意: 组件内部不要修改props数据

#### 2.3.4 编码操作

1. 内部读取某个属性值---props是只读的，不可修改

![img](D:\typora_photo\wps1.png)

2. 对props中的属性值进行类型限制和必要性限制

   在 `React 15.5` 以前，`React` 身上有一个 `PropTypes` 属性可直接使用，即 `name: React.PropTypes.string.isRequired` ，没有把 `PropTypes` 单独封装为一个模块。

   从 `React 15.5` 开始，把 `PropTypes` 单独封装为一个模块，需要额外导入使用。

​      第一种方式（React v15.5 开始已弃用）：

![img](D:\typora_photo\wps2.png)

​     第二种方式（新）：使用prop-types库进限制（需要引入prop-types库）

​                                         ![img](D:\typora_photo\wps9.png)

​    3.  从外部传递数据给到类里面

​      方法一：扩展属性: 将对象的所有属性通过props传递

![img](D:\typora_photo\wps4.png)

​       方法二：直接在ReactDOM.render渲染的组件上添加key-value键值对

​                          ![img](D:\typora_photo\wps7.png)

4. 默认属性值：

![img](D:\typora_photo\wps5.png)

5. 组件类的构造函数

   ![img](D:\typora_photo\wps6.png)

  6、函数式组件的props——通过函数的参数传递

![image-20231228145807415](D:\typora_photo\image-20231228145807415.png)

![image-20231228145817705](D:\typora_photo\image-20231228145817705.png)

7、对于从外部传递的Number与函数数据，使用{}表示，用引号会默认为字符串

![image-20231228145930215](D:\typora_photo\image-20231228145930215.png)

8、在类中，直接在某个类添加属性，采用static 属性名=属性值的写法 static wheel=4

​     在类中，为某个类的实例对象添加属性，采用直接赋值的形式如a=1

![image-20231228150114579](D:\typora_photo\image-20231228150114579.png)

#### **案例：** **自定义用来显示一个人员信息的组件**

***1.* 姓名必须指定，且为字符串类型；**

***2.* 性别为字符串类型，如果性别没有指定，默认为男**

***3.* 年龄为字符串类型，且为数字类型，默认值为18**

![image-20231228150634287](D:\typora_photo\image-20231228150634287.png)

完整版

```js
<body>
    <div id="test"></div>
    <div id="test1"></div>
    <script type="text/babel">
        class Person extends React.Component {
            render() {
                const { name, sex, age } = this.props
                //props是只读的，不可修改
                // this.props.name="jack" 报错
                return (
                    <ul>
                        <li>姓名：{name}</li>
                        <li>性别：{sex}</li>
                        <li>年龄：{age + 1}</li>
                    </ul>
                )
            }
        }
        Person.propTypes = {
            name: PropTypes.string.isRequired, //react的15.xxxx版本使用
            sex: PropTypes.string,
            age: PropTypes.number,
            speak:PropTypes.func
        }
        Person.defaultProps = {
            sex: '男or女',
            age: 10
        }
        ReactDOM.render(<Person name="tom" sex="女" age={12} speak={speak} />, document.getElementById('test'))
        const p = { name: 'jerry', sex: '女', age: 15 }
        ReactDOM.render(<Person {...p} />, document.getElementById('test1'))
        //这里的<Person {...p}/>中的{...p}不是复制对象，其中{}是作为分隔符，有babel和react加持，...p在react中展开对象是支持的，仅在标签中支持
        function speak() {
            console.log('说话')
        }
    </script>
</body>
```

简易版

`Person.propTypes` 和 `Person.defaultProps` 可以看作在类身上添加属性，利用 `static` 关键词就能在类内部进行声明。因此所谓简写只是从类外部移到类内部。

```js
<body>
    <div id="test"></div>
    <div id="test1"></div>
    <script type="text/babel">
        class Person extends React.Component {
            static propTypes = {
                name: PropTypes.string.isRequired, //react的15.xxxx版本使用
                sex: PropTypes.string,
                age: PropTypes.number,
                speak: PropTypes.func
            }
            static defaultProps = {
                sex: '男or女',
                age: 10
            }
            render() {
                const { name, sex, age } = this.props
                return (
                    <ul>
                        <li>姓名：{name}</li>
                        <li>性别：{sex}</li>
                        <li>年龄：{age + 1}</li>
                    </ul>
                )
            }
        }
        ReactDOM.render(<Person name="tom" sex="女" age={12} speak={speak} />, document.getElementById('test'))
        const p = { name: 'jerry', sex: '女', age: 15 }
        ReactDOM.render(<Person {...p} />, document.getElementById('test1'))
        function speak() {
            console.log('说话')
        }
    </script>
</body>
```

#### 类式组件的构造器与 props

[官网文档说明](https://zh-hans.reactjs.org/docs/react-component.html#constructor)

构造函数一般用在两种情况：

- 通过给 `this.state` 赋值对象来初始化内部 `state`
- 为事件处理函数绑定实例

```js
constructor(props) {
  super(props)
  // 初始化 state
  this.state = { isHot: true, wind: '微风' }
  // 解决 this 指向问题---为事件处理函数绑定实例
  this.changeWeather = this.changeWeather.bind(this)
}
```

因此构造器一般都不需要写。如果要在构造器内使用 `this.props` 才声明构造器，并且需要在最开始调用 `super(props)` ：

```js
constructor(props) {
  super(props)
  console.log(this.props)
}
```

#### 函数式组件使用 props

由于函数可以传递参数，因此函数式组件可以使用 `props` 。

```js
<body>
    <div id="test"></div>
    <script type="text/babel">
       function Person(props) {
        const { name, sex, age } = props
        console.log(props);
                return (
                    <ul>
                        <li>姓名：{name}</li>
                        <li>性别：{sex}</li>
                        <li>年龄：{age + 1}</li>
                    </ul>
                )
        }
        Person.propTypes = {
            name: PropTypes.string.isRequired, //react的15.xxxx版本使用
            sex: PropTypes.string,
            age: PropTypes.number
        }
        Person.defaultProps = {
            sex: '男',
            age: 10
        }
     ReactDOM.render(<Person name="tom" sex="女" age={18}/>, document.getElementById('test'))
    </script>
</body>
```

### 2.4 组件三大属性----refs

通过定义 `ref` 属性可以给标签添加标识——ref相当于是标识id

回调函数满足的三个特点：（1）自己定义 （2）自己没有调用 （3）函数执行了（别人调用的）

**案例：**

自定义组件, 功能说明如下:

1. 点击按钮, 提示第一个输入框中的值

2. 当第2个输入框失去焦点时, 提示这个输入框中的值

   ![image-20231228202856379](D:\typora_photo\image-20231228202856379.png)

**三种实现方法**：

#### 2.4.1 字符串形式的ref

这种形式已过时，效率不高，[官方](https://zh-hans.reactjs.org/docs/refs-and-the-dom.html#legacy-api-string-refs)不建议使用。

```js
<body>
    <div id="test"></div>
    <script type="text/babel">
        class Demo extends React.Component{
            render(){
                console.log(this);
                return (
                    <div>
                    <input type="text" ref="ip1" placeholder="点击提示数据"/>&nbsp;&nbsp;
                    <button id="btn" onClick={this.getData}>点击提示数据</button>
                    <input onBlur={this.showData} ref="ip2" type="text"  placeholder="失去焦点提示数据" />    
                    </div>
                )
            }
            getData=()=>{
                alert(this.refs.ip1.value)
                console.log(this.refs.ip1);//获取到input真实DOM
            }
            showData=()=>{
                alert(this.refs.ip2.value)
            }
        }
        ReactDOM.render(<Demo/>,document.getElementById('test'))
    </script>
</body>
```

打印console.log(this.refs)时结果为：一个DOM标识对象

![image-20231228153945965](D:\typora_photo\image-20231228153945965.png)

#### 2.4.2 回调函数形式的ref

**两种形式：**

##### （1）内联函数

```js
<body>
    <div id="test"></div>
    <script type="text/babel">
        class Demo extends React.Component {
            getData = () => {
                alert(this.input1.value)
            }
            showData = () => {
                const { input2 } = this
                alert(input2.value)
            }
            render() {
                console.log(this);
                return (
                    <div>
                        {/*其中得到的currentNode是真实的DOM元素input*/}
                        <input type="text" ref={currentNode => this.input1 = currentNode} placeholder="点击提示数据" />&nbsp;&nbsp;
                        <button id="btn" onClick={this.getData}>点击提示数据</button>
                        <input onBlur={this.showData} ref={c => this.input2 = c} type="text" placeholder="失去焦点提示数据" />
                    </div>
                )
            }
        }
        ReactDOM.render(<Demo />, document.getElementById('test'))
    </script>
</body>
```

要点：

- `c => this.input1 = c` 就是给组件实例添加 `input1` 属性，值为节点
- 由于是箭头函数，因此 `this` 是 `render` 函数里的 `this` ，即组件实例

##### （2）class的绑定函数

```js
<body>
    <div id="test"></div>
    <script type="text/babel">
        class Demo extends React.Component {
            state = { isHot: true }
            getData = () => {
                alert(this.input1.value)
            }
            changeWeather = () => {
                let ishot = this.state.isHot
                this.setState({ isHot: !ishot })
            }
            //方法二：外部引入写法
            saveInput = (currentNode) => {
                this.input1 = currentNode
                console.log(currentNode);
            }
            render() {
                const { isHot } = this.state
                return (
                    <div>
                     <h2>今天天气很{isHot ? '炎热' : '凉爽'}</h2>
                     <button onClick={this.changeWeather}>点击切换天气</button><br /><br />
                     <input type="text" ref={this.saveInput} placeholder="点击提示数据" />
                     <button onClick={this.getData}>点击提示数据</button>&nbsp;&nbsp;
                    </div>
                )
            }
        }
        ReactDOM.render(<Demo />, document.getElementById('test'))
    </script>
</body>
```

关于回调 `ref` 执行次数的问题，[官网](https://zh-hans.reactjs.org/docs/refs-and-the-dom.html#caveats-with-callback-refs)描述：

> 如果 `ref` 回调函数是以内联函数的方式定义的，在更新过程中它会被执行两次，第一次传入参数 `null`，然后第二次会传入参数 DOM 元素。这是因为在每次渲染时会创建一个新的函数实例，所以 React 清空旧的 `ref` 并且设置新的。通过将 `ref` 的回调函数定义成 `class` 的绑定函数的方式可以避免上述问题，但是大多数情况下它是无关紧要的。

即内联函数形式，在更新过程中 `ref` 回调会被执行两次，第一次传入 `null` ，第二次传入 DOM 元素。若是用类的绑定函数，则只执行一次。但是对功能实现没有影响，因此一般也是用内联函数形式。

#### 2.4.3 利用 createRef API

该方式通过调用 `React.createRef` 返回一个容器用于存储节点，且一个容器只能存储一个节点。其他节点想用只能自己定义一个。

```js
<body>
    <div id="test"></div>
    <script type="text/babel">
        class Demo extends React.Component {
      /*React.createRef()调用后可以返回一个容器，该容器可以存储被ref所标识的节点，该容器是专人专用的*/
            myRef = React.createRef()
            myRef2 = React.createRef()
            getData = () => {
                console.log(this.myRef);
                const g = this.myRef.current
                alert(g.value)
            }
            showData = () => {
                console.log(this.myRef2); //返回{current:input对象}
                const k = this.myRef2.current
                alert(k.value)
            }
            render() {
                return (
                    <div>
                     {/*其中得到的currentNode是真实的DOM元素input*/}
                     <input ref={this.myRef} type="text" placeholder="点击提示数据" />
                     <button onClick={this.getData}>点击提示数据</button>&nbsp;&nbsp;
                     <input onBlur={this.showData} ref={this.myRef2} type="text" placeholder="失去焦点提示数据" />
                    </div>
                )
            }
        }
        ReactDOM.render(<Demo />, document.getElementById('test'))
    </script>
</body>
```

### 2.5 事件处理

1.通过onXxx属性指定事件处理函数(注意大小写)

​        a.React使用的是自定义(合成)事件如onClick,onBlur, 而不是使用的原生DOM事件如onclick,onblur——为了更好的兼容性

​        b.React中的事件是通过**事件委托方式**处理的(委托给组件最外层的元素[事件冒泡]) ——为了高效

2.通过event.target得到发生事件的DOM元素对象 —— 不要过度调用ref

**当触发事件的元素和需要操作的元素为同一个时，**可以不使用 `ref` ：

```js
class Demo extends React.Component {  
    showData2 = (event) => {    
        alert(event.target.value)  
    }   
    render() {    
        return ( 
         <div>        
         <input onBlur={this.showData2} type="text" placeholder="失去焦点提示数据" />       
         </div>    
    )  
} }
```

### 2.6 收集表单数据

包含表单的组件分类：

- 非受控组件：现用现取。即需要使用时，再获取节点得到数据。
- 受控组件：类似于 Vue 双向绑定的从视图层绑定到数据层，将需要的表单数据存储在state状态中，需要的时候再取出来使用。

**尽量使用受控组件，因为非受控组件需要使用大量的 `ref` 。**

**案例： 定义一个包含表单的组件**

 **输入用户名密码后, 点击登录提示输入信息**

![image-20231229105625292](D:\typora_photo\image-20231229105625292.png)

```js
//非受控组件
<body>
    <div id="test"></div>
    <script type="text/babel">
        class Login extends React.Component {
            handleSubmit = (event) => {
                event.preventDefault();//阻止表单默认行为提交与刷新跳转 
                const { uname, password } = this
                alert('用户名是：' + uname.value + '，密码是' + password.value)
            }
            render() {
             return (
               <form onSubmit={this.handleSubmit}> 
               用户名: <input ref={c => this.uname = c} type="text" name="uname" />
               密码:<input ref={c => this.password = c} type="password" name="password" />
               <button>登录</button>
               </form>
             )
          }
      }
        ReactDOM.render(<Login />, document.getElementById('test'))
    </script>
</body>
```

```js
//受控组件
<body>
    <div id="test"></div>
    <script type="text/babel">
        class Login extends React.Component {
            state = { uname: '', password: '' }
            handleSubmit = (event) => {
                event.preventDefault();//阻止表单默认行为提交与刷新跳转 
                const { uname, password } = this.state
                alert('用户名是：' + uname + '，密码是' + password)
            }
            saveUsername = (event) => {
                //console.log(event.target.value);
                this.setState({ uname: event.target.value })
                //console.log(this.state);
            }
            savePassword = (event) => {
                this.setState({ password: event.target.value })
            }
           render() {
              return (
               <form onSubmit={this.handleSubmit}>
               用户名: <input onChange={this.saveUsername} type="text" name="uname" />
               密码:<input onChange={this.savePassword} type="password" name="password" />
                   <button>登录</button>
               </form>
              )
          }
        }
        ReactDOM.render(<Login />, document.getElementById('test'))
    </script>
</body>
```

### 2.7 高阶函数--函数柯里化

对上述受控组件的代码进行优化，希望把 `saveUsername` 和 `savePassword` 合并为一个函数。

```js
注意：不断输入能够不断地调用这个保存数据的函数，因此onChange必须将一个函数作为事件的回调，才能够在input改变时收集每一次的改变值，有三种情况：
a. 不加参数，把saveUsername的函数交给onChange，作为onChange的回调，例如上面受控组件的写法 
onChange={this.saveUsername}
b. 加参数，并将一个函数的返回值设置为一个函数，返回函数作为onChange的回调,如高阶函数写法
onChange={this.saveFormData('username')
c. 内联函数写法，接收参数event，并在内联回调函数中调用另一个函数，并传入参数，不用柯里化写法
onChange={event=>this.saveFormData('username',event)} 

//若为onChange={this.saveUsername(3)}传入参数了，但是在函数saveUsername中没有返回一个函数，于是还没有等输入框改变值就已经调用了这个函数了，达不到效果
```

要点：

- 高阶函数（如果一个函数符合下面2个规范中的任何一个，那该函数 就是高阶函数）：

  ​         （1）若A函数，接收的参数为函数，称为高阶函数

  ​        （2）若A函数，调用的返回值一个函数，如 `Promise、setTimeout、Array.map()`

- 函数柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码形式

  ![image-20231229110318457](D:\typora_photo\image-20231229110318457.png)

```js
//柯里化实现
<body>
    <div id="test"></div>
    <script type="text/babel">
        class Login extends React.Component {
            state={uname:'',password:''}
            handleSubmit = (event) => {
                event.preventDefault();//阻止表单默认行为提交与刷新跳转 
                const { username, password } = this.state
                alert('用户名是：' + username + '，密码是' + password)
            }
            saveFormData=(dataType)=>{
                return (event)=>{
                    // console.log(event.target.value);
                    this.setState({[dataType]:event.target.value})
                }
            }
            render() {
                return (
   <form onSubmit={this.handleSubmit}> 
  用户名: <input onChange={this.saveFormData('username')} type="text" name="uname" />
  密码:<input onChange={this.saveFormData('password')}  type="password" name="password" />
  <button>登录</button>
  </form>
                )
            }
        }
        ReactDOM.render(<Login />, document.getElementById('test'))
    </script>
</body>
```

```js
//不用柯里化实现
<body>
    <div id="test"></div>
    <script type="text/babel">
        class Login extends React.Component {
            state={uname:'',password:''}
            handleSubmit = (event) => {
                event.preventDefault();//阻止表单默认行为提交与刷新跳转 
                const { username, password } = this.state
                alert('用户名是：' + username + '，密码是' + password)
            }
            saveFormData=(dataType,event)=>{
                event.preventDefault()
                this.setState({[dataType]:event.target.value})
            }
            render() {
                return (
                    <form onSubmit={this.handleSubmit}> 
                     用户名: <input onChange={event=>this.saveFormData('username',event)} type="text" name="uname" />
                     密码:<input onChange={event=>this.saveFormData('password',event)}  type="password" name="password" />
                    <button>登录</button>
                    </form>
                )
            }
        }
        ReactDOM.render(<Login />, document.getElementById('test'))
    </script>
</body>
```

### 2.8 组件的生命周期

​    **生命周期回调函数 <=>  生命周期钩子函数  <=>  生命周期函数  <=>  生命周期钩子**

当把定时器放在render函数里面，

![image-20231229114209672](D:\typora_photo\image-20231229114209672.png)

#### 2.8.1 理解

1. 组件从创建到死亡它会经历一些特定的阶段。

2. React组件中包含一系列勾子函数(生命周期回调函数), 会在特定的时刻调用。
3.  我们在定义组件时，会在特定的生命周期回调函数中，做特定的工作。

#### 2.8.2 生命周期流程图(旧)

![React Lifecycle](D:\typora_photo\react-lifecyle-old.png)

**初始化阶段**：`ReactDOM.render()` 触发的初次渲染

- `constructor`
- `componentWillMount`： 组件将要挂载的钩子
- `render`：初始化渲染，状态更新之后调用的
- `componentDidMount`： 组件挂载完毕的钩子

**更新阶段**

1. 父组件重新 `render` 触发的更新

- `componentWillReceiveProps`：可以接收一个参数props，为传入的值，此钩子只有在第二次新的props才调用

  ![image-20231229153355368](D:\typora_photo\image-20231229153355368.png)

- `shouldComponentUpdate` ：控制组件是否更新的阀门，返回值为布尔值，默认为 `true` 。若返回 `false` ，则后续流程不会进行。

  ![image-20231229152959457](D:\typora_photo\image-20231229152959457.png)

- `componentWillUpdate`： 组件将要更新的钩子

- `render`

- `componentDidUpdate`： 组件更新完毕的钩子

2. 组件内部调用 `this.setState()` 修改状态

- `shouldComponentUpdate`
- `componentWillUpdate`
- `render`
- `componentDidUpdate`

3. 组件内部调用 `this.forceUpdate()` 强制更新

- `componentWillUpdate`
- `render`
- `componentDidUpdate`

**卸载阶段**：`ReactDOM.unmountComponentAtNode()` 触发

- `componentWillUnmount`： 组件将要卸载的钩子，React 会在你的组件被移除屏幕（**卸载**）之前调用它

**常用的钩子：**

componentDidMount： 一般在这个钩子中做一些初始化的事，例如：开启定时器、发送网络请求、订阅消息

componentWillUnmount：般在这个钩子中做一些收尾的事，例如：关闭定时器、取消订阅消息

**案例解析各个钩子：**

```js
<body>
    <div id="test"></div>
    <script type="text/babel">
        class Count extends React.Component {
            constructor(props) {
                console.log('Count-constructor');
                super(props)
                this.state = { count: 0 }
            }
            getSum = () => {
                const { count } = this.state
                this.setState({ count: count + 1 })
            }
            delCom=()=>{
                ReactDOM.unmountComponentAtNode(document.getElementById('test'))
            }
            force=()=>{
                this.forceUpdate()
            }
            //组件将要挂载的钩子
            componentWillMount() {
                console.log('Count-componentWillMount');
            }
           //组件挂载完毕的钩子
            componentDidMount(){
                console.log('Count-componentDidMount');
            }
             //组件将要卸载的钩子
             componentWillUnmount(){
                console.log('Count-componentWillUnmount');
            }
            //控制组件更新的阀门
            shouldComponentUpdate(){
                console.log('Count-shouldComponentUpdate');
                return true
            }
            //组件将要更新的钩子
            componentWillUpdate() {
                console.log('Count-componentWillUpdate');
            }
            //组件更新完毕的钩子
            componentDidUpdate(){
                console.log('Count-componentDidUpdate');
            }
            //组件渲染的钩子
            render() {
                console.log('Count-render');
                const { count } = this.state
                return (
                    <div>
                        <h2>当前求和为：{count}</h2>
                        <button onClick={this.getSum}>点我加1</button><br/><br/>
                        <button onClick={this.delCom}>卸载组件</button><br/><br/>
                        <button onClick={this.force}>强制更新，不更改任何状态中的数据</button>
                    </div>
                )
            }
        }
        ReactDOM.render(<Count />, document.getElementById('test'))
    </script>
</body>
```

页面加载时出现：

![image-20231229152826611](D:\typora_photo\image-20231229152826611.png)

点击加1按钮触发this.setState():

![image-20231229152913860](D:\typora_photo\image-20231229152913860.png)

点击强制刷新时：

![image-20231229152939304](D:\typora_photo\image-20231229152939304.png)

**案例实现父子组件——父组件的render流程：**

```js
<body>
    <div id="test"></div>
    <script type="text/babel">
        //父组件A
        class A extends React.Component {
            state = { carName: '奔驰' }
            changeCar = () => {
                this.setState({ carName: '宝马' })
            }
            render() {
                console.log('A----render');
                return (
                    <div>
                        <div>A</div>
                        <button onClick={this.changeCar}>换车</button><br /><br />
                        <B carName={this.state.carName} />
                    </div>
                )
            }
        }
        //子组件B
        class B extends React.Component {
            //控制组件更新的阀门
            shouldComponentUpdate() {
                console.log('B-shouldComponentUpdate');
                return true
            }
            //组件将要更新的钩子
            componentWillUpdate() {
                console.log('B-componentWillUpdate');
            }

            //组件更新完毕的钩子
            componentDidUpdate() {
                console.log('B-componentDidUpdate');
            }
            //组件将要接收新的props的钩子
            componentWillReceiveProps(props) {
                console.log('B--componentWillReceiveProps', props);
            }
            render() {
                return (
                    <div>
                        <div>B，接收到的车型是：{this.props.carName}</div>
                    </div>
                )
            }
        }
        ReactDOM.render(<A />, document.getElementById('test'))
    </script>
</body>
```

点击换车按钮：

![image-20231229153711718](D:\typora_photo\image-20231229153711718.png)

#### 2.8.3 生命周期流程图(新)

新旧对比：废弃了三个，新增了两个

[更改内容](https://zh-hans.reactjs.org/blog/2018/03/27/update-on-async-rendering.html)：

- 废弃三个钩子：`componentWillMount` 、`componentWillReceiveProps` 、 `componentWillUpdate` 。在新版本中这三个钩子需要加 `UNSAFE_` 前缀才能使用，后续可能会废弃。

- 新增两个钩子（实际场景用得很少）：`getDerivedStateFromProps` 、`getSnapshotBeforeUpdate`

  （1）[static getDerivedStateFromProps(props, state)](https://zh-hans.reactjs.org/docs/react-component.html#static-getderivedstatefromprops)：

  - 需使用 `static` 修饰
  - 需返回一个对象更新 `state` 或返回 `null`
  - 适用于如下情况：`state` 的值任何时候都取决于 `props`
  - ![image-20231229175015685](D:\typora_photo\image-20231229175015685.png)

  （2）[getSnapshotBeforeUpdate(prevProps, prevState)](https://zh-hans.reactjs.org/docs/react-component.html#getsnapshotbeforeupdate)：

  - 在组件更新之前获取快照
  - 得组件能在发生更改之前从 DOM 中捕获一些信息（如滚动位置）
  - 返回值将作为参数传递给 `componentDidUpdate()`
  - 注意： `componentDidUpdate()`可以传入三个参数，preProps为外部传递的值，preState为状态更新前一刻的值，snapshotValue为快照值
  - ![image-20231229175031505](D:\typora_photo\image-20231229175031505.png)

在新版本17中为啥子要在componentWillMount，componentWillupdate,componentWillReceiveProps前面加上前缀USAFE_呢？https://zh-hans.legacy.reactjs.org/blog/2018/03/27/update-on-async-rendering.html

**新版生命周期**

![React LIfecycle New](D:\typora_photo\react-lifecycle-new.png)

**初始化阶段**：`ReactDOM.render()` 触发的初次渲染

- `constructor`
- getDerivedStateFromProps
- `render`：初始化渲染，状态更新之后调用的
- `componentDidMount`： 组件挂载完毕的钩子

**更新阶段：**由组件内部this.setSate()或父组件重新render触发

- getDerivedStateFromProps

- shouldComponentUpdate()

- render()

- getSnapshotBeforeUpdate

-  componentDidUpdate()

**卸载阶段**：`ReactDOM.unmountComponentAtNode()` 触发

- `componentWillUnmount`： 组件将要卸载的钩子，React 会在你的组件被移除屏幕（**卸载**）之前调用它

案例

```js
<body>
    <div id="test"></div>
    <script type="text/babel">

        class Count extends React.Component {
            constructor(props) {
                console.log('Count-constructor');
                super(props)
                this.state = { count: 0 }
            }

            getSum = () => {
                const { count } = this.state
                this.setState({ count: count + 1 })
            }
            delCom = () => {
                ReactDOM.unmountComponentAtNode(document.getElementById('test'))
            }
            force = () => {
                this.forceUpdate()
            }

            //组件将要挂载的钩子
            // UNSAFE_componentWillMount() {
            //     console.log('Count-componentWillMount');
            // }

            //组件挂载完毕的钩子
            componentDidMount() {
                console.log('Count-componentDidMount');
            }
            //组件将要卸载的钩子
            componentWillUnmount() {
                console.log('Count-componentWillUnmount');
            }

            //控制组件更新的阀门
            shouldComponentUpdate() {
                console.log('Count-shouldComponentUpdate');
                return true
            }

            //组件将要更新的钩子
            // UNSAFE_componentWillUpdate() {
            //     console.log('Count-componentWillUpdate');
            // }
            
            //若 state 的值在任何时候都取决于 props，可以使用此钩子
            static getDerivedStateFromProps(props, state) {
                //props接收从外部传过来的值<Count age={12} />
                console.log('Count---getDerivedStateFromProps', props, state);
                //返回一个状态对象{属性：值}，相当于改变了state的值，以后永远改变不了了
                // return {count:108}
                //return null 就无影响
                // return props  使state更新受阻
                return null
            }
            
            // getSnapshotBeforeUpdate() 在最近一次渲染输出（提交到 DOM 节点）之前调用。
            //它使得组件能在发生更改之前从 DOM 中捕获一些信息（例如，滚动位置）。
            //在更新之前获取快照
            getSnapshotBeforeUpdate() {
                console.log('Count----getSnapshotBeforeUpdate');
                return 'atguigu'
            }
            //组件更新完毕的钩子 snapshotValue快照 就是 getSnapshotBeforeUpdate的返回值
            componentDidUpdate(perProps, perState,snapshotValue) {
                console.log('Count-componentDidUpdate', perProps, perState,snapshotValue);
            }
            //组件渲染的钩子
            render() {
                console.log('Count-render');
                const { count } = this.state
                return (
                    <div>
                        <h2>当前求和为：{count}</h2>
                        <button onClick={this.getSum}>点我加1</button><br /><br />
                        <button onClick={this.delCom}>卸载组件</button><br /><br />
                        <button onClick={this.force}>强制更新，不更改任何状态中的数据</button>
                    </div>
                )
            }
        }
        ReactDOM.render(<Count count={12} />, document.getElementById('test'))
    </script>
</body>
```

**getSnapshotBeforeUpdate的使用场景：获取滚动位置**

```js
<body>
    <div id="test"></div>
    <script type="text/babel">
        class NewList extends React.Component {
            state={newArr:[]}
            componentDidMount(){
                setInterval(() => {
                    const {newArr} = this.state
                    const news='新闻'+(newArr.length+1)
                    this.setState({newArr:[news,...newArr]})
                }, 1000);
            }
            getSnapshotBeforeUpdate(){
                return this.refs.list.scrollHeight
            }
            componentDidUpdate(preProps,preState,height){
                this.refs.list.scrollTop+=this.refs.list.scrollHeight-height
            }
            render() {
                return (
                    <div className="list" ref="list">
                       {
                       this.state.newArr.map((n,index)=>{
                        return  <div key={index} className="new">{n}</div>
                       })
                     }
                    </div>
                )
            }
        }
        ReactDOM.render(<NewList/>, document.getElementById('test'))
    </script>
</body>
```

![image-20231229175541394](D:\typora_photo\image-20231229175541394.png)

#### 2.8.4 主要的钩子

1. render：初始化渲染或更新渲染调用

2. componentDidMount：开启监听, 发送ajax请求

3. componentWillUnmount：做一些收尾工作, 如: 清理定时器

#### 2.8.5  18版本后即将废弃的勾子

1. componentWillMount

2. componentWillReceiveProps

3. componentWillUpdate

现在使用会出现警告，下一个大版本需要加上UNSAFE_前缀才能使用，以后可能会被彻底废弃，不建议使用。

### 2.9 虚拟DOM与Diffing算法

![Diff](D:\typora_photo\Diff.png)

DOM对比的最小粒度是标签，嵌套层对比

  **经典面试题:**

   **1). react/vue中的key有什么作用？（key的内部原理是什么？）**

​       虚拟DOM中key的作用：

​          1). 简单的说: **key是虚拟DOM对象的标识**, 在更新显示时key起着极其重要的作用。

​          2). 详细的说: 当状态中的数据发生变化时，react会根据【新数据】生成【新的虚拟DOM】,

​                        随后React进行【新虚拟DOM】与【旧虚拟DOM】的diff比较，比较规则如下：

​                  a. 旧虚拟DOM中找到了与新虚拟DOM相同的key：

​                        (1).若虚拟DOM中**内容没变**, **直接使用**之前的**真实DOM**

​                        (2).若虚拟DOM中**内容变了**, 则**生成新的真实DOM**，随后替换掉页面中之前的真实DOM

​                  b. 旧虚拟DOM中未找到与新虚拟DOM相同的key：

​                        根据数据创建新的真实DOM，随后渲染到到页面

   **2). 为什么遍历列表时，key最好不要用index?**

​         用index作为key可能会引发的问题：

​                1. 若对数据进行：**逆序添加、逆序删除等破坏顺序操作**:

​                        会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。

​                2. 如果结构中还**包含输入类**如input等的DOM元素：

​                        会产生错误DOM更新 ==> **界面有问题**。

​                3. 注意！如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，

​                  仅用于渲染列表用于展示，使用index作为key是没有问题的。

​      **3. 开发中如何选择key?**

​           （1）**最好使用每条数据的唯一标识作为key, 比如id、手机号、身份证号、学号等唯一值。**

​           （2）如果确定只是简单的展示数据，用index也是可以的。

案例：

![image-20231229202847655](D:\typora_photo\image-20231229202847655.png)

```js
body>
    <div id="test"></div>
    <script type="text/babel">
    /*
        慢动作回放----使用index索引值作为key
            初始数据：
                    {id:1,name:'小张',age:18},
                    {id:2,name:'小李',age:19},
            初始的虚拟DOM：
                    <li key=0>小张---18<input type="text"/></li>
                    <li key=1>小李---19<input type="text"/></li>
            更新后的数据：
                    {id:3,name:'小王',age:20},
                    {id:1,name:'小张',age:18},
                    {id:2,name:'小李',age:19},
            更新数据后的虚拟DOM：
                    <li key=0>小王---20<input type="text"/></li>
                    <li key=1>小张---18<input type="text"/></li>
                    <li key=2>小李---19<input type="text"/></li>
    -----------------------------------------------------------------
    慢动作回放----使用id唯一标识作为key
            初始数据：
                    {id:1,name:'小张',age:18},
                    {id:2,name:'小李',age:19},
            初始的虚拟DOM：
                    <li key=1>小张---18<input type="text"/></li>
                    <li key=2>小李---19<input type="text"/></li>
            更新后的数据：
                    {id:3,name:'小王',age:20},
                    {id:1,name:'小张',age:18},
                    {id:2,name:'小李',age:19},
            更新数据后的虚拟DOM：
                    <li key=3>小王---20<input type="text"/></li>
                    <li key=1>小张---18<input type="text"/></li>
                    <li key=2>小李---19<input type="text"/></li>
     */
        class Person extends React.Component {
            state = {
                persons: [
                    { id: 1, name: '小张', age: 18 },
                    { id: 2, name: '小李', age: 19 },
                ]
            }
            addPerson=()=>{
                const {persons} =this.state
                const p={id:persons.length+1,name:'小王',age:20}
                this.setState({persons:[p,...persons]})
            }
            render() {
                return (
                   <div>
                    <h2>展示人员信息</h2>
                    <button onClick={this.addPerson}>添加一个小王</button>
                    <h3>使用index索引值作为key</h3>
                    <ul>
                        {
                        this.state.persons.map((item, index) => {
                 return <li key={index}>{item.name}-{item.age} <input type="text"/></li>
                            })
                        }
                    </ul>
                    <hr/><hr/>
                    <h3>使用id(数据唯一标识)作为key</h3>
                    <ul>
                        {
                        this.state.persons.map((item) => {
                return <li key={item.id}>{item.name}-{item.age} <input type="text"/></li>
                            })
                        }
                    </ul>
                    </div>
                )
            }
        }
        ReactDOM.render(<Person />, document.getElementById('test'))
    </script>
</body>
```

![image-20231229203015523](D:\typora_photo\image-20231229203015523.png)

## 三、React 脚手架

1. xxx脚手架: 用来帮助程序员快速创建一个基于xxx库的模板项目

   2.包含了所有需要的配置（语法检查、jsx编译、devServer…）

   3.下载好了所有相关的依赖

4. 可以直接运行一个简单效果

   5.react提供了一个用于创建react项目的脚手架库: **create-react-app**

6. **项目的整体技术架构为:  react + webpack + es6 + eslint**

7. 使用脚手架开发的项目的特点: **模块化、组件化、 工程化**

### 3.1、创建react项目

- 全局安装 React 脚手架：`npm i -g create-react-app`
- 创建项目：`create-react-app 项目名称`
- 进入文件夹：`cd 项目名称`
- 启动项目：`npm start` /yarn start

### 3.2、React 脚手架项目结构

​                                   ![image-20240101111205782](D:\typora_photo\image-20240101111205782.png)     ![image-20240101111235315](D:\typora_photo\image-20240101111235315.png)

`public` ：静态资源文件

- `manifest.json` ：应用加壳（把网页变成安卓/IOS 软件）的配置文件
- `robots.txt` ：爬虫协议文件

`src` ：源码文件

- `App.test.js` ：用于给 `App` 组件做测试，一般不用
- `index.js` ：入口文件
- `reportWebVitals.js` ：页面性能分析文件，需要 `web-vitals` 库支持
- `setupTests.js` ：组件单元测试文件，需要 `jest-dom` 库支持

`index.html` 代码分析：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <!-- %PUBLIC_URL% 代表 public 文件夹的路径 -->
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <!-- 开启理想视口，用于做移动端网页的适配 -->
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <!-- 用于配置浏览器页签+地址栏的颜色(仅支持安卓手机浏览器) -->
    <meta name="theme-color" content="red" />
    <!-- 网站描述 -->
    <meta name="description" content="Web site created using create-react-app" />
    <!-- 用于指定网页添加到手机主屏幕后的图标 -->
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <!-- 应用加壳时的配置文件 -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <title>React App</title>
  </head>
  <body>
    <!-- 若浏览器不支持 js 则展示标签中的内容 -->
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```

### 3.3 样式的模块化

样式的模块化可用于解决样式冲突的问题。该方法比较麻烦，实际开发用的比较少。用 `less` 就能解决了。

`component/Hello` 文件下的 `index.css` 改名为 `index.module.css` 。

```css
.title {
  background-color: orange;
}
```

`Hello` 组件导入样式：

```jsx
import { Component } from 'react'
import hello from './index.module.css'

export default class Hello extends Component {
  render() {
    return <h2 className={hello.title}>Hello,React!</h2>
  }
}
```

vscode 的插件----方便书写代码块

![image-20240101152343984](D:\typora_photo\image-20240101152343984.png)

### 3.4 功能界面的组件化编码流程（通用）

1. 拆分组件: 拆分界面,抽取组件

2. 实现静态组件: 使用组件实现静态页面效果

3. 实现动态组

   动态显示初始化数据

   - 数据类型

   - 数据名称
   - 保存在哪个组件?

​      交互(从绑定事件监听开始)

### 3.5 ToDoList案例

![image-20240102153757968](D:\typora_photo\image-20240102153757968.png)

#### 案例总结：

1. 拆分组件、实现静态组件，注意：`className` 、`style` 的写法
2. 动态初始化列表，如何确定将数据放在哪个组件的 `state` 中？

- 某个组件使用：放在其自身的 `state` 中
- 某些组件使用：放在他们共同的父组件 `state` 中，即**状态提升**

  3.关于父子之间通信：

- 父传子：直接通过 `props` 传递
- **子传父**：父组件通过 `props` 给子组件**传递一个函数**，子组件调用该函数
- 父传孙：先父传子再子传孙

```react
// 父组件
class Father extends Component {
  state: {
    todos: [{ id: '001', name: '吃饭', done: true }],
    flag: true,
  }
  addTodo = (todo) => {
    const { todos } = this.state
    const newTodos = [todo, ...todos]
    this.setState({ todos: newTodos })
  }
  render() {
    return <List todos={this.state.todos} addTodo={this.addTodo} />
  }
}
// 子组件
class Son extends Component {
  // 由于 addTodo 是箭头函数，this 指向父组件实例对象，因此子组件调用它相当于父组件实例在调用
  handleClick = () => {
    this.props.addTodo({ id: '002', name: '敲代码', done: false })
  }
  render() {
    return <button onClick={this.handleClick}>添加</button>
  }
}
```

4.input框的checkbox的defaultChecked与checked

-   defaultChecked:一上来就判断是否勾选，后续可以更改勾选状态，但是如果传入判断条件，则只对第一次加载的判断有效果，后续达到判断条件就不再有效果了。

- checked则不能在后续更改状态，需要更改通过onchange()方法来操作

  5.注意 `defaultChecked` 和 `checked` 的区别，类似的还有：`defaultValue` 和 `value`

  6.状态在哪里，操作状态的方法就在哪里

  8.更改对象中的某个属性写法

```javascript
let obj={a:1,b:2}
let obj2={...obj,b:3}
console.log(obj2) //{a:1,b:3}
```

 9.e.target.checked获取checkbox的勾选状态，e.keyCode获取键盘按键的代码

10.生成世界唯一id:uuid库与nanoid库

```jsp
安装：npm i nanoid
使用：import {nanoid} from 'nanoid'
     nanoid()
```

### 3.6 react脚手架配置代理总结

**跨域：数据能发送但是请求的数据不回来**

#### 3.6.1方法一

> 在package.json中追加如下配置

```json
"proxy":"http://localhost:5000"
```

![image-20240102163331581](D:\typora_photo\image-20240102163331581.png)

说明：

1. 优点：配置简单，前端请求资源时可以不加任何前缀。
2. 缺点：**不能配置多个代理。**
3. 工作方式：上述方式配置代理，当请求了3000不存在的资源时，那么该请求会转发给5000 （优先匹配前端资源）

#### 3.6.2 方法二

1. 第一步：创建代理配置文件

   ```
   在src下创建配置文件：src/setupProxy.js
   ```

2. 编写setupProxy.js配置具体代理规则：

   ```js
   const proxy = require('http-proxy-middleware')
   
   module.exports = function(app) {
     app.use(
       proxy('/api1', {  //api1是需要转发的请求(所有带有/api1前缀的请求都会转发给5000)
         target: 'http://localhost:5000', //配置转发目标地址(能返回数据的服务器地址)
         changeOrigin: true, //控制服务器接收到的请求头中host字段的值
         /*
         	changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
         	changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:3000
         	changeOrigin默认值为false，但我们一般将changeOrigin值设为true
         */
         pathRewrite: {'^/api1': ''} //去除请求前缀，保证交给后台服务器的是正常请求地址(必须配置)
       }),
       proxy('/api2', { 
         target: 'http://localhost:5001',
         changeOrigin: true,
         pathRewrite: {'^/api2': ''}
       })
     )
   }
   ```

说明：

1. 优点：**可以配置多个代理**，可以灵活的控制请求是否走代理。
2. 缺点：配置繁琐，前端请求资源时必须加前缀。

### 3.7消息订阅-发布机制

即 React 中兄弟组件或任意组件之间的通信方式。

使用的工具库：[PubSubJS](https://www.npmjs.com/package/pubsub-js)

下载安装 `PubSubJS` ：`npm install pubsub-js --save`

基础用法：

```js
import PubSub from 'pubsub-js'

// 订阅消息
var token = PubSub.subscribe('topic', (msg, data) => {
  console.log(msg, data)
})

// 发布消息
PubSub.publish('topic', 'hello react')

// 取消订阅
PubSub.unsubscribe(token)
```

案例：github搜索案例---pubsub

### 3.8 Fetch（**关注分离**的设计思想）

#### 3.8.1 文档

1. https://github.github.io/fetch/

2. https://segmentfault.com/a/1190000003810652

#### 3.8.2 特点

1. fetch: 原生函数，不再使用XmlHttpRequest对象提交ajax请求

2. 老版本浏览器可能不支持

#### 3.8.3 相关API

1) **GET请求**

```js
//未优化版本
fetch(`https://api.github.com/search/users?q=${keyword}`).then(
                response => {
                    console.log('联系服务器成功了');
                    return response.json()
                },
                error => {
                    console.log('联系服务器失败了', error);
                    return new Promise(() => { })
                }
            ).then(
                response => {
                    console.log('获取数据成功了', response);
                },
                error => {
                    console.log('获取数据失败了', error);
                }
            )
        }
        
//优化版本
        fetch(`https://api.github.com/search/users?q=${keyword} `).then(
            response => {
                console.log('联系服务器成功了');
                return response.json()
            }
        ).then(
            response => {
                console.log('获取数据成功了', response);
            }
        ).catch(
            (error) => {
                console.log('请求出错', error);
            }
        )
```

 **async /await 优化写法**

```js
try {
   const response = await fetch(`https://api.github.com/search/users?q=${keyword} `)
   const data = await response.json()
   PubSub.publish('atguigu', { isLoading: false, avatar: data.items })
} catch (error) {
   console.log('请求出错了');
   PubSub.publish('atguigu', { isLoading: false, Error: error.message })
}
```

2) **POST请求**

```javascript
 fetch(url, { 
     method: "POST",  
     body: JSON.stringify(data),
     })
     .then(function(data) {  
     console.log(data) 
 }).catch(function(e) { 
     console.log(e) }
   )
```

### 3.9  github案例总结 （看代码）

1. 设计状态时要考虑全面，例如带有网络请求的组件，要考虑请求失败怎么办。
2. ES6 知识点：解构赋值 + 重命名

```js
let obj = { a: { b: 1 } }
//传统解构赋值
const { a } = obj
//连续解构赋值
const {
  a: { b },
} = obj
//连续解构赋值 + 重命名
const {
  a: { b: value },
} = obj
```

   3.消息订阅与发布机制

- **先订阅，再发布（隔空对话）**
- 适用于**任意组件间**通信
- 要在 `componentWillUnmount` 钩子中取消订阅

 4.`fetch` 发送请求（**关注分离**的设计思想）

```js
try {
  // 先看服务器是否联系得上
  const response = await fetch(`/api1/search/users2?q=${keyWord}`)
  // 再获取数据
  const data = await response.json()
  console.log(data)
} catch (error) {
  console.log('请求出错', error)
}
```

![image-20240110154036848](D:\typora_photo\image-20240110154036848.png)

## 四、React路由

### 4.1. 相关理解

#### 4.1.1. SPA的理解（单页面多组件）

1. 单页Web应用（single page web application，SPA）。

2. 整个应用**只有一个完整的页面**。

3. 点击页面中的链接**不会刷新页面**，只会做页面的**局部更新**。
4.  数据都需要通过ajax请求获取, 并在前端异步展现。

#### 4.1.2 路由的理解

**1.** **什么是路由？**

1. 一个路由就是一个映射关系(key:value)

2. key为路径, value可能是function或component

**2**. **路由分类**

1. 后端路由：

（1）理解： **value是function**, 用来处理客户端提交的请求。

（2）注册路由： router.get(path, function(req, res))

（3）工作过程：当node接收到一个请求时, 根据请求路径找到匹配的路由, 调用路由中的函数来处理请求, 返回响应数据

2. 前端路由：

（1） 浏览器端路由，**value是component**，用于展示页面内容。

（2）注册路由: <Route path="/test" component={Test}>

（3）工作过程：当浏览器的path变为/test时, 当前路由组件就会变为Test组件

#### 4.1.3 路由原理history

借助window身上的history属性实现，与浏览器历史记录进行交互。

![image-20240110210505327](D:\typora_photo\image-20240110210505327.png)

<img src="D:\typora_photo\image-20240110210627122.png" alt="image-20240110210627122" style="zoom: 67%;" />

![image-20240110210734291](D:\typora_photo\image-20240110210734291.png)

![image-20240110210744140](D:\typora_photo\image-20240110210744140.png)

**history利用listen方法监听路径的变化。**

方法二实现类似于**锚点**

![image-20240110210857478](D:\typora_photo\image-20240110210857478.png)

![image-20240110210938435](D:\typora_photo\image-20240110210938435.png)

### 4.2  react路由

react中有三种路由：有不同用途（WEB、Native、Any)

#### 4.2.1 react-router-dom的理解

1. react的一个插件库。

2. 专门用来实现一个SPA应用。

3. 基于react的项目基本都会用到此库。

安装 `react-router-dom` ：

```
// 安装 5.X 版本路由
npm install react-router-dom@5.2.0 -S

// 最新已经 6.X 版本，用法和 5.X 有所不同
npm install react-router-dom -S
```

`6.x` 版本的用法参考[文章](https://zhuanlan.zhihu.com/p/191419879)

以 `5.x` 版本为例展示基本使用：

```js
// App.jsx
import React, { Component } from 'react'
import { Link, Route } from 'react-router-dom'
import Home from './components/Home'
import About from './components/About'

export default class App extends Component {
  render() {
    return (
      <div>
        <div className="list-group">
          <Link className="list-group-item" to="/about">
            About
          </Link>
          <Link className="list-group-item" to="/home">
            Home
          </Link>
        </div>
        <div className="panel-body">
          <Route path="/about" component={About} />
          <Route path="/home" component={Home} />
        </div>
      </div>
    )
  }
}
```

`<App>` 的最外侧包裹 `<BrowserRouter>` 或 `<HashRouter>` ：

```js
// index.js
import React from 'react'
import ReactDOM from 'react-dom'
import { BrowserRouter } from 'react-router-dom'
import App from './App'

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
)
```

![image-20240111155325020](D:\typora_photo\image-20240111155325020.png)

注意点：

 1.明确好界面中的导航区、展示区 
 2.导航区的a标签改为Link标签 

```js
<Link to="/xxxxx">Demo</Link> 
```

 3.展示区写Route标签进行路径的匹配 

```js
<Route path='/xxxx'component={Demo}/> 
```


 4.<App>的最外侧包裹了一个<BrowserRouter>或<HashRouter>

 5.在react中路由使用Link链接，在运行后的浏览器页面中还是会转化为a标签的方式实现跳转

![image-20240111154738552](D:\typora_photo\image-20240111154738552.png)

6、使用HashRouter，在路径上加上#

![image-20240111155224199](D:\typora_photo\image-20240111155224199.png)



#### 4.4.2 路由组件和一般组件

1. 写法不同：

- 一般组件：`<Demo/>`
- 路由组件：`<Route path="/demo" component={Demo}/>`

2. 存放位置不同：

- 一般组件：`components`
- 路由组件：`pages`

  3.接收到的 `props` 不同：

- 一般组件：标签属性传递
- 路由组件：接收到三个固定的属性

```js
history:
  go: ƒ go(n)
  goBack: ƒ goBack()
  goForward: ƒ goForward()
  push: ƒ push(path, state)
  replace: ƒ replace(path, state)

location:
  pathname: "/home/message/detail/2/hello"
  search: ""
  state: undefined

match:
  params: {}
  path: "/home/message/detail/:id/:title"
  url: "/home/message/detail/2/hello"
```

![image-20240111210733536](D:\typora_photo\image-20240111210733536.png)

#### 4.2.3 NavLink 的使用

`NavLink` 可以实现路由链接的高亮，通过 `activeClassName` 指定样式名，默认追加类名为 `active` 。如果要追加一个样式，用activeClassName。

```html
<NavLink activeClassName="demo" to="/about">About</NavLink>

<NavLink activeClassName="demo" to="/home">Home</NavLink>
```

封装 `NavLink` 组件：由于 `NavLink` 组件中重复的代码太多，因此进行二次封装。

※ 细节点：组件标签的内容会传递到 `this.props.children` 属性中，反过来通过指定标签的 `children` 属性可以修改组件标签内容

```js
// MyNavLink 组件
import React, { Component } from 'react'
import { NavLink } from 'react-router-dom'

export default class MyNavLink extends Component {
  render() {
    // this.props.children 可以取到标签内容，如 About, Home
    // 反过来通过指定标签的 children 属性可以修改标签内容
    return <NavLink activeClassName="demo" className="list-group-item" {...this.props} />
  }
}
```

```js
// App.js
class App extends Component {
    render() {
        return (
            <div>
                <div className="list-group">
                 {/* 路由中使用Link路由链接跳转页面  */}
                  {/* <NavLink activeClassName="demo" className="list-group-item" to="/about">About</NavLink>
                  <NavLink activeClassName="demo" className="list-group-item" to="/home">Home</NavLink> */}
                  <MyNavLink to='/about'>About</MyNavLink>
                  <MyNavLink to='/home'>Home</MyNavLink>
                   {/* <NavLink activeClassName="demo" className="list-group-item" to="/home" children="Home" /> */}//相当于在闭合标签体中写Home
                 </div>
            </div>
        );
    }
}
```

注意：

- NavLink可以实现路由链接的高亮，通过**activeClassName**指定样式名

- **标签体内容是一个特殊的标签属性**
- 通过this.props.children可以获取标签体内容

![image-20240112144644011](D:\typora_photo\image-20240112144644011.png)





![image-20240112101303820](D:\typora_photo\image-20240112101303820.png)

![image-20240112101247912](D:\typora_photo\image-20240112101247912.png)

#### 4.2.4 Switch 的使用

通常情况下，path和component是一一对应的关系，Switch可以提高路由匹配效率（单一匹配）。

`Switch` 可以提高路由匹配效率，如果匹配成功，则不再继续匹配后面的路由，即单一匹配。

```html
<!-- 只会展示 Home 组件 -->
<Switch>
  <Route path="/about" component="{About}" />
  <Route path="/home" component="{Home}" />
  <Route path="/home" component="{Test}" />
</Switch>
```

#### 4.2.5 解决多级路径刷新页面样式丢失的问题

多级路径/at/home,当刷新时，浏览器会认为多级路径是localhost中的一个路径，刷新时，请求bootstrap变成http://localhost:3000/at/css/bootstrap.css，页面显示的就是public文件夹下的Index。**304表示走缓存**

三种解决方法：

- `public/index.html` 中 引入样式时不写 `./` 写 `/` （常用）。表示不要在当前目录的上一层中查找，而是直接在localhost:3000下寻找。
- `public/index.html` 中 引入样式时不写 `./` 写 `%PUBLIC_URL%` （只在react中用，其他框架不可用）
- 使用 `HashRouter，HashRouter会认为#后面的内容属于前端的，当给3000发请求时自动忽略#之后的路径就不带给3000

```html
方法一：<link rel="stylesheet" href="/bootstrap.css" />
方法二：<link rel="stylesheet" href="%PUBLIC_URL%/bootstrap.css" />
//index.js
方法三：
import { HashRouter } from 'react-router-dom'
ReactDOM.render(
    <HashRouter>
        <App />
    </HashRouter>,
document.getElementById('root'))
```

#### 4.2.6 路由的严格匹配与模糊匹配

- 默认使用的是模糊匹配(简单记:【输入的路径】必须包含要【匹配的路径】，且顺序要一致)

  ![image-20240112150046770](D:\typora_photo\image-20240112150046770.png)

- 开启严格匹配

  ```js
  <Route exact={true} path="/about"component={About}/>
  //简单写法
  <Route exact path="/about"component={About}/>
  ```

- **严格匹配不要随便开启，需要再开，有些时候开启会导致无法继续匹配二级路由**

#### 4.2.7 Redirect 的使用

- 一般写在所有路由注册的**最下方**，当所有路由都无法匹配时，跳转到 Redirect 指定的路由

```html
<Switch>
  <Route path="/about" component="{About}" />
  <Route path="/home" component="{Home}" />
  <Redirect to="/about" />
</Switch>
```

### 4.3 嵌套路由（二级路由/多级路由）

路由的匹配是按照路由注册的先后顺序从前往后开始匹配的。

- 注册子路由需写上父路由的 `path`
- 路由的匹配是按照注册路由的顺序进行的

```jsx
// Home/index.jsx
class index extends Component {
    render() {
        console.log('Home---', this.props);
        return (
            <div>
                <h2>Home组件内容</h2>
                <div>
                    <ul className="nav nav-tabs">
                        <li>
                            <MyNavLink to="/home/news">News</MyNavLink>
                        </li>
                        <li>
                            <MyNavLink to="/home/message">Message</MyNavLink>
                        </li>
                    </ul>
                    <Switch>
                        <Route path="/home/news" component={News}/>
                        <Route path="/home/message" component={Message} />
                        <Redirect to="/home/news"/>
                    </Switch>
                </div>
            </div>
        );
    }
}
export default index;
```

```jsx
// News/index.jsx
import React, { Component } from 'react';
class index extends Component {
    render() {
        return (
            <div>
                <ul>
                    <li>news001</li>
                    <li>news002</li>
                    <li>news003</li>
                </ul>
            </div>
        );
    }
}
export default index;
```

```jsx
// Message/index.jsx
import React, { Component } from 'react';
class index extends Component {
    render() {
        return (
            <div>
                <ul>
                    <li>
                        <a href="/message1">message001</a>&nbsp;&nbsp;
                    </li>
                    <li>
                        <a href="/message2">message002</a>&nbsp;&nbsp;
                    </li>
                    <li>
                        <a href="/message/3">message003</a>&nbsp;&nbsp;
                    </li>
                </ul>
            </div>
        );
    }
}
export default index;
```

![image-20240112153348613](D:\typora_photo\image-20240112153348613.png)

### 4.4 路由传参

##### 方式一：params参数

```jsx
路山链接(携带参数):<Link to='/demo/test/tom/18'}>详情</Link>
注册路由(声明接收):<Route path="/demo/test/:name/;age" component={Test}/>
接收参数:const {id,title} = this.props.match.params
```

当用params传参给另一个子组件时，此时子组件的props是：

![image-20240112161355790](D:\typora_photo\image-20240112161355790.png)

```jsx
//Message/index.jsx
<li key={item.id}>
{/* 向路由组件传递params参数 */}
<Link to={`/home/message/detail/${item.id}/${item.title}`}>{item.title}</Link>
// 写法二
<Link to={{ pathname: `/home/message/detail/${item.id}/${item.title}` }}>{item.title}</Link>
</li>

{/* 声明接收params参数 */}
<Route path="/home/message/detail/:id/:title" component={Details} />
```

```jsx
// Details /index.jsx
//接收params参数
const { id, title } = this.props.match.params
const findResult = data.find((obj) => {
      return obj.id === id
})
```

![image-20240112162105661](D:\typora_photo\image-20240112162105661.png)

##### 方式二：search参数

```jsx
路由链接(携带参数):<Link to='/demo/test?name=tom&age=18'}>详情</Link>
注册路由(无需声明，正常注册即可):<Route path="/demo/test" component={Test}/>
接收参数:this.props.location.search
备注:获取到的search是urlencoded编码字符串，需要借助querystring解析
qs.stringify()将对象转为urlencoded编码字符串(id=1&name=2)
qs.parse()将urlencoded编码字符串(id=1&name=2)转为对象形式
```

当用search传参给另一个子组件时，此时子组件的props是：

![image-20240112165716023](D:\typora_photo\image-20240112165716023.png)

```jsx
// Message /index.jsx
<li key={item.id}>
 {/* 向路由组件传递search参数 */}
<Link to={`/home/message/detail/?id=${item.id}&title=${item.title}`}>{item.title}</Link>
<Link to={{ pathname: `/home/message/detail/?id=${item.id}&title=${item.title}` }}>{item.title}</Link>
</li>

{/* search参数无需声明接收，只需要注册路由即可 */}
<Route path="/home/message/detail" component={Details} />
```

```jsx
// Details /index.jsx
//接收search参数
const { search } = this.props.location
const qsdata = qs.parse(search.slice(1)) //转换为对象并截取掉问号？
console.log(qsdata);
const { id, title } = qsdata
const findResult = data.find((obj) => {
    return obj.id === id
})
```

![image-20240112165754315](D:\typora_photo\image-20240112165754315.png)

##### 方式三：state参数

```jsx
路由链接(携带参数):<Link to={{pathname: "/demo/test",state: {id: item.id}}}>详情</Link>
注册路由(无需声明，正常注册即可):<Route path="/demo/test" component={Test}/>
接收参数:this.props.location.state
备注:刷新也可以保留住参数，在接收参数时设置|| {}
```

```jsx
// Message /index.jsx
<li key={item.id}>     
 <Link to={{ pathname: "/home/message/detail", state: { id: item.id, title: item.title } }}>{item.title}</Link>
</li>

{/* state参数无需声明接收，只需要注册路由即可 */}
<Route path="/home/message/detail" component={Details} />
```

```jsx
//Details index.jsx
//接收state参数
const { id,title } = this.props.location.state || {}
const findResult =objdata.find((obj) => {
      return obj.id === id
 }) || {}
```

![image-20240112171026793](D:\typora_photo\image-20240112171026793.png)

复制当前路径，清空浏览记录缓存时，再次粘贴进入页面会出现找不到id和content的错误，此时需要在

接收参数设置默认值为空对象，放置报错。

![image-20240112201255802](D:\typora_photo\image-20240112201255802.png)

![image-20240112170952694](D:\typora_photo\image-20240112170952694.png)

三种方式对比：

- `state` 方式当前页面刷新可保留参数，**但在新页面打开不能保留**。前两种方式由于参数保存在 URL 地址上，因此都能保留参数。
- `params` 和 `search` 参数都会变成字符串

### 4.5 push和replace模式

push模式：将当前路径推入栈中，可退回当前路径的上一步

replace模式：会替换当前路径，退回一步为当前路径的上一步的上一步

```html
//replace模式
<Link  replace={true} to={{ pathname: "/home/message/detail", state: { id: item.id, title: item.title } }}>{item.title}</Link>

<Link  replace to={{ pathname: "/home/message/detail", state: { id: item.id, title: item.title } }}>{item.title}</Link>}
                                
```

### 4.6 编程式导航

编程式导航是使用路由组件 `this.props.history` 提供的 API 进行路由跳转：

```jsx
this.props.history.push(path, state)
this.props.history.replace(path, state)
this.props.history.goForward()
this.props.history.goBack()
this.props.history.go(n)
// 编程式导航传参
<button onClick={() => this.replaceShow(item.id, item.title)}>replace查看</button>
this.props.history.push(`/home/message/detail/${id}/${title}`)
this.props.history.replace(`/home/message/detail/${id}/${title}`)
this.props.history.push(`/home/message/detail?id=${id}&title=${title}`)
this.props.history.replace(`/home/message/detail?id=${id}&title=${title}`)
this.props.history.push(`/home/message/detail`, { id: id, title: title })
this.props.history.replace(`/home/message/detail`, { id: id, title: title })
this.props.history.push(`/home/message/detail`, { id, title })
```

![image-20240113102624000](D:\typora_photo\image-20240113102624000.png)

### 4.7 withRouter 的使用

`withRouter` 的作用：加工一般组件，让其拥有路由组件的 API ，如 `this.props.history.push` 等。

withRouter的返回值是一个新组件。

```js
import React, {Component} from 'react'
import {withRouter} from 'react-router-dom'

class Header extends Component {
  ...
}

export default withRouter(Header)
```

![image-20240113110200240](D:\typora_photo\image-20240113110200240.png)

### 4.8 BrowserRouter 和 HashRouter

底层原理不一样：

- `BrowserRouter` 使用的是 H5 的 history API，不兼容 IE9 及以下版本。
- `HashRouter` 使用的是 URL 的哈希值。

路径表现形式不一样

- `BrowserRouter` 的路径中没有 `#` ，如：`localhost:3000/demo/test`
- `HashRouter` 的路径包含#，如：`localhost:3000/#/demo/test`

刷新后对路由 `state` 参数的影响

- `BrowserRouter` 没有影响，因为 `state` 保存在 `history` 对象中。总是借助history这个对象来保存一些历史浏览路径信息。
- **`HashRouter` 刷新后会导致路由 `state` 参数的丢失！**（因为hashrouter没有保留记录的history，只是借助锚点）

备注：`HashRouter` 可以用于解决一些路径错误相关的[问题](https://brucecai55520.gitee.io/my-notes/#/React/React路由?id=解决多级路径刷新页面样式丢失的问题)。（即多级路由刷新样式丢失问题）

## 五、React UI 组件库

### 5.1 material-ui(国外)

1. 官网: [http://www.material-ui.com/#/](#/)

2. github: https://github.com/callemall/material-ui

### 5.2. ant-design(国内蚂蚁金服)

1. 官网: https://ant.design/index-cn
2. Github: https://github.com/ant-design/ant-design/

### 5.3 Ant Design 配置按需引入和自定义主题

> 以下配置是 `3.x` 版本，`4.x` 版本见[官网](https://3x.ant.design/index-cn)

1. 安装依赖：

```powershell
npm install react-app-rewired customize-cra babel-plugin-import less less-loader
```

1. 修改 `package.json`

```js
"scripts": {
  "start": "react-app-rewired start",
  "build": "react-app-rewired build",
  "test": "react-app-rewired test",
  "eject": "react-scripts eject"
}
```

1. 根目录下创建 `config-overrides.js`

```js
//配置具体的修改规则
const { override, fixBabelImports, addLessLoader } = require('customize-cra')

module.exports = override(
  fixBabelImports('import', {
    libraryName: 'antd',
    libraryDirectory: 'es',
    style: true,
  }),
  addLessLoader({
    lessOptions: {
      javascriptEnabled: true,
      modifyVars: { '@primary-color': 'green' },
    },
  })
)
```

1. 备注：不用在组件里引入样式，`import 'antd/dist/antd.css'` 删掉

### 5.4 ant-design5.x主题定制

https://ant.design/docs/react/customize-theme-cn

1、通过 ConfigProvider 进行暗黑模式主题配置：

```jsx
import React from 'react';
import { Button, ConfigProvider, Input, Space, theme } from 'antd';
const App: React.FC = () => (
  <ConfigProvider
    theme={{
      // 1. 单独使用暗色算法
      algorithm: theme.darkAlgorithm,
      // 2. 组合使用暗色算法与紧凑算法
      // algorithm: [theme.darkAlgorithm, theme.compactAlgorithm],
    }}
  >
    <Space>
      <Input placeholder="Please Input" />
      <Button type="primary">Submit</Button>
    </Space>
  </ConfigProvider>
);
export default App;
```

2、通过 ConfigProvider 修改主题变量：

通过 `theme` 中的 `token` 属性，可以修改一些主题变量。部分主题变量会引起其他主题变量的变化，我们把这些主题变量称为 Seed Token。

```jsx
import { Button, ConfigProvider, Space } from 'antd';
import React from 'react';
const App: React.FC = () => (
  <ConfigProvider
    theme={{
      token: {
        // Seed Token，影响范围大
        colorPrimary: '#00b96b',
        borderRadius: 2,

        // 派生变量，影响范围小
        colorBgContainer: '#f6ffed',
      },
    }}
  >
    <Space>
      <Button type="primary">Primary</Button>
      <Button>Default</Button>
    </Space>
  </ConfigProvider>
);
export default App;
```

![image-20240113172443104](D:\typora_photo\image-20240113172443104.png)

## 六、Redux 概述

### 6.1 Redux 为何物

- Redux 是用于做 **状态管理** 的 JS 库
- 可用于 React、Angular、Vue 等项目中，常用于 React
- 集中式管理 React 应用多个组件共享的状态

### 6.2 何时用 Redux

- 某个组件的状态，需要让其他组件拿到（状态共享）
- 一个组件需要改变另一个组件的状态（通信）
- 使用原则：不到万不得已不要轻易动用

### 6.3 Redux 工作流程

![image-20240114201848255](D:\typora_photo\image-20240114201848255.png)

- 组件想操作 Redux 中的状态：把动作类型和数据告诉 `Action Creators`
- `Action Creators` 创建 `action` ：同步 `action` 是一个普通对象，异步 `action` 是一个函数
- `Store` 调用 `dispatch()` 分发 `action` 给 `Reducers` 执行
- `Reducers` 接收 `previousState` 、`action` 两个参数，对状态进行加工后返回新状态
- `Store` 调用 `getState()` 把状态传给组件

### 6.4 redux求和案例精简版

1、去除Count组件自身的状态

2、src下建立:

```jsx
-redux
-store.js
-couht_reducer.js
```

3、store.js:

```jsx
(1).引入redux中的createStore函数，创建一个store
(2).createStore调用时要传入一个为其服务的reducer
(3).记得暴露store对象
```

4、count_reducer.js:

```jsx
（1）reducer的本质是一个函数，接收:preState,action，返回加工后的状态
（2）reducer有两个作用:初始化状态，加工状态
（3).reducer被第一次调用时，是store自动触发的，传递的preState是undefined,传递的action是{type:'@@React/INT_a.2.b.3'}
```

5、在index.js中检测store中状态的改变，一旦发生改变重新渲染<App/>,或者在组件中的ComponentDidMount()中检测状态的改变
**备注:redux只负责管理状态，至于状态的改变驱动着页面的展示，要靠我们自己写。**

```js
// Redux store.js
//暴露一个store对象，整个应用只有一个store
//引入createtore 专门用于创建redux中最为核心的store
//redux旧版本写法，5.0版本已经弃用了
// import { createStore } from 'redux'
import { legacy_createStore as createStore } from 'redux'
//引入为Count组件服务的reducer
import countReducer from './countReducer'
const store = createStore(countReducer)
export default store
```

```js
// Redux countReducer.js
//创建一个为count组件服务的reducer，本质是一个函数
//reducer函数接收两个参数:之前的状态，动作对象
const initState=0 //初始化状态
export default function countReducer(preState = initState, action) {
    // if (preState === undefined) preState = 0 方法一
    //从action对象中获取type和data
    const { type, data } = action
    switch (type) {
        case 'increment':
            return preState + data
        case 'decrement':
            return preState - data
        //初始化
        default:
            return preState
    }
}
```

```jsx
// Component Count.jsx
import React, { Component } from 'react';
//引入store，用于保存redux中的状态
import store from '../../redux/store'
class index extends Component {
    //写法一
    // componentDidMount() {
    //     //监视redux的状态变化，只要变化就调用render（render中数据的改变不会驱动视图变化，要调用render一下才可以）
    //     //当状态改变回调函数就执行
    //     store.subscribe(() => {
    //         this.setState({})
    //     })
    // }
    increment = () => {
        const { value } = this.selectNumber
        //通知redux加value
        store.dispatch({ type: 'increment', data: value * 1 })
    }
    decrement = () => {
        const { value } = this.selectNumber
        store.dispatch({ type: 'decrement', data: value * 1 })
    }
    incrementIdOdd = () => {
        const { value } = this.selectNumber
        const count  = store.getState()
        if (count % 2 !== 0) {
            store.dispatch({ type: 'increment', data: value * 1 })
        }
    }
    incremenAsync = () => {
        const { value } = this.selectNumber
        setTimeout(() => {
            store.dispatch({ type: 'increment', data: value * 1 })
        }, 500);
    }
    render() {
        return (
            <div>
                <h1>当前求和为:{store.getState()}</h1>
                <select ref={c => this.selectNumber = c}>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                </select>&nbsp;&nbsp;
                <button onClick={this.increment}>+</button>&nbsp;&nbsp;
                <button onClick={this.decrement}>-</button>&nbsp;&nbsp;
                <button onClick={this.incrementIdOdd}>奇数再加</button>&nbsp;&nbsp;
                <button onClick={this.incremenAsync}>异步加</button>
            </div>
        );
    }
}
export default index;
```

```js
//index.js
import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'
import store from './redux/store'
ReactDOM.render(<App />, document.getElementById('root'))
store.subscribe(() => {
    ReactDOM.render(<App />, document.getElementById('root'))
})
```

![image-20240115155846893](D:\typora_photo\image-20240115155846893.png)

### 6.5 redux求和案例完整版

新增文件：

- countAction.js 专门用于创建Action对象

- constant.js 放置由于编码疏忽写错action中的type

```js
// countAction.js
import { INCREMENT, DECREMENT } from './constant'
export const createIncrementAction = (data) => ({ type: INCREMENT, data })
export const createDecrementAction = (data) => ({ type: DECREMENT, data })
```

```js
// constant.js 
//该模块用于定义type类型常量值，防止程序员单词写错
export const INCREMENT = 'increment'
export const DECREMENT = 'decrement'
```

箭头函数返回一个对象的简单写法：

![image-20240115160723641](D:\typora_photo\image-20240115160723641.png)

### 6.6 redux的异步action

action中有两种数据形式：对象（同步）、函数（异步）

安装异步中间件：

```jsx
npm install redux-thunk 
```

要点：

- 延迟的动作不想交给组件，而是 `action`
- 当操作状态所需数据要靠异步任务返回时，可用异步 `action`
- 创建 `action` 的函数不再返回一般对象，而是返回一个函数，该函数中写异步任务
- 异步任务完成后，分发一个同步 `action` 去真正操作数据
- 异步 `action` 不是必要的，完全可以在组件中等待异步任务结果返回在分发同步 `action`

```js
// countAction.js
//专门为Count组件生成action对象
// function createIncrementAction(data) {
//     return { type: 'increment', data }
// }
import { INCREMENT, DECREMENT } from './constant'
//异步action，就是指action值为Object类型的一般对象
export const createIncrementAction = (data) => ({ type: INCREMENT, data })
export const createDecrementAction = (data) => ({ type: DECREMENT, data })
//异步action，就是指action值为函数,异步action中一般都会调用同步action,异步action不是必须要用的
export const createIncrementAsyncAction = (data, time) => {
    return (dispatch) => {
        setTimeout(() => {
            dispatch(createIncrementAction(data))
        }, time);
    }
}
```

```jsx
// store.js
//暴露一个store对象，整个应用只有一个store
//引入createtore 专门用于创建redux中最为核心的store
//redux旧版本写法，5.0版本已经弃用了
// import { createStore } from 'redux'
import { legacy_createStore as createStore ,applyMiddleware} from 'redux'
//引入为Count组件服务的reducer
import countReducer from './countReducer'
//引入redux-thunk 用于支持异步action
import { thunk } from 'redux-thunk'
const store = createStore(countReducer,applyMiddleware(thunk))
export default store
```

```jsx
// Count .jsx
import React, { Component } from 'react';
//引入store，用于保存redux中的状态
import store from '../../redux/store'
import { createIncrementAction, createDecrementAction, createIncrementAsyncAction } from '../../redux/countAction'
class index extends Component {
    increment = () => {
        const { value } = this.selectNumber
        //通知redux加value
        store.dispatch(createIncrementAction(value * 1))
    }
    decrement = () => {
        const { value } = this.selectNumber
        store.dispatch(createDecrementAction(value * 1))
    }
    incrementIdOdd = () => {
        const { value } = this.selectNumber
        const count = store.getState()
        if (count % 2 !== 0) {
            store.dispatch(createIncrementAction(value * 1))
        }
    }
    incremenAsync = () => {
        const { value } = this.selectNumber
        store.dispatch(createIncrementAsyncAction(value * 1, 500))
    }
    render() {
        return (
            <div>
                <h1>当前求和为:{store.getState()}</h1>
                <select ref={c => this.selectNumber = c}>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                </select>&nbsp;&nbsp;
                <button onClick={this.increment}>+</button>&nbsp;&nbsp;
                <button onClick={this.decrement}>-</button>&nbsp;&nbsp;
                <button onClick={this.incrementIdOdd}>奇数再加</button>&nbsp;&nbsp;
                <button onClick={this.incremenAsync}>异步加</button>
            </div>
        );
    }
}
export default index;
```

## 七、React-Redux

> React-Redux 是一个**插件库**，用于简化 React 中使用 Redux 。

![React-Redux模型图](D:\typora_photo\react-redux.png)

React-Redux 将组件分为两类：

- UI 组件
  - 只负责 UI 呈现，不带有业务逻辑
  - 通过 `props` 接收数据
  - 不能使用 Redux 的 API
  - 保存在 `components` 文件夹下
- 容器组件
  - 负责管理数据和业务逻辑，和 Redux 通信，将结果交给 UI 组件
  - 可使用 Redux 的 API
  - 保存在 `containers` 文件夹下

###  7.1 求和案例react-redux的基本使用

(1).明确两个概念:

- UI组件：不能使用任何redux的api，只负责页面的呈现、交互等。

- 容器组件：负责和redux通信，将结果交给UI组件。

(2).如何创建一个容器组件一靠react-redux的connect函数

- connect(mapStateToProps,mapDispatchToProps)(UI组件)
- -mapStateToProps：映射状态，返回值是一个对象
- -mapDispatchToProps：**映射操作状态的方法**，返回值是一个对象
- **connect函数中的两个参数可以通过return对象或者方法传给子组件，子组件用props接收**
- ![image-20240116212427205](D:\typora_photo\image-20240116212427205.png)

(3).备注:容器组件中的store是靠props传进去的，而不是在容器组件中直接引入

```jsx
// Contain index.jsx
//引入Count的UI组件
import CountUI from '../../components/Count'
//引入connect用于连接组件和redux
import { connect } from 'react-redux'
import { createIncrementAction, createIncrementAsyncAction, createDecrementAction } from '../../redux/countAction'
//store由props传进来

//mapStateToProps函数的返回的对象中的key作为传递给UI组件props的key ,value就作为传递给UI组件props的value————传递状态
//相当于<CountUI n={900}/>
//映射状态
function mapStateToProps(state) {
    return { count: state }
}
// mapDispatchToProps函数的返回的对象中的key作为传递给UI组件props的key ,value就作为传递给UI组件props的value————传递操作状态的方法
//映射操作状态的方法
function mapDispatchToProps(dispatch) {
    return {
        add: number => dispatch(createIncrementAction(number)),
        sub: number => dispatch(createDecrementAction(number)),
        addAsync: (number, time) => dispatch(createIncrementAsyncAction(number, time))
    }
}
//使用connect()创建并暴露一个Count的容器组件
export default connect(mapStateToProps,mapDispatchToProps)(CountUI)
```

```jsx
// Count index.jsx
import React, { Component } from 'react';
class index extends Component {
    increment = () => {
        const { value } = this.selectNumber
        this.props.add(value * 1)
    }
    decrement = () => {
        const { value } = this.selectNumber
        this.props.sub(value * 1)
    }
    incrementIdOdd = () => {
        const { value } = this.selectNumber
        if (this.props.count % 2 !== 0) {
            this.props.add(value * 1)
        }
    }
    incremenAsync = () => {
        const { value } = this.selectNumber
        this.props.addAsync(value * 1)
    }
    render() {
        console.log('@@@11', this.props);
        return (
            <div>
                <h1>当前求和为:{this.props.count}</h1>
                <select ref={c => this.selectNumber = c}>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                </select>&nbsp;&nbsp;
                <button onClick={this.increment}>+</button>&nbsp;&nbsp;
                <button onClick={this.decrement}>-</button>&nbsp;&nbsp;
                <button onClick={this.incrementIdOdd}>奇数再加</button>&nbsp;&nbsp;
                <button onClick={this.incremenAsync}>异步加</button>
            </div>
        );
    }
}
export default index;
```

```js
//App.js
import React, { Component } from 'react'
import Count from './container/Count/index'
import store from './redux/store'
class App extends Component {
    render() {
        return (
            <div>
                {/* 给容器组件传递store */}
                <Count store={store} />
            </div>
        );
    }
}
export default App;
```

### 7.2 求和案例优化写法一

mapDispatchToProps可以是一个对象，由react-redux内部包装帮你自动调用dispatch

```jsx
// Contain index.jsx
import CountUI from '../../components/Count'
import { connect } from 'react-redux'
import { createIncrementAction, createIncrementAsyncAction, createDecrementAction } from '../../redux/countAction'

//使用connect()创建并暴露一个Count的容器组件
export default connect(
    state => ({ count: state }),

    //mapDispatchToProps的一般写法
    // dispatch => (
    // {
    //     add: number => dispatch(createIncrementAction(number)),
    //     sub: number => dispatch(createDecrementAction(number)),
    //     addAsync: (number, time) => dispatch(createIncrementAsyncAction(number, time))
    // })

    // mapDispatchToProps的简单写法 
    {
        add: createIncrementAction,
        sub:createDecrementAction,
        addAsync:createIncrementAsyncAction
    }
)(CountUI)
```

### 7.3 求和案例优化写法二

React-Redux 容器组件可以自动监测 Redux 状态变化，因此 `index.js` 不需要手动监听：

```js
store.subscribe(() => {
  ReactDOM.render(<App />, document.getElementById('root'))
})
```

`Provider` 组件的使用：让所有组件都能获得状态数据，不必一个一个传递

```js
// index.js
import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'
import { Provider } from 'react-redux'
import store from './redux/store'

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```

### 7.4  求和案例优化写法三

从文件结构入手，将Count组件和容器组件整合在一起

```jsx
import React, { Component } from 'react';
//引入connect用于连接组件和redux
import { connect } from 'react-redux'
import { createIncrementAction, createIncrementAsyncAction, createDecrementAction } from '../../redux/countAction'
//定义UI组件
class Count extends Component {
    increment = () => {
        const { value } = this.selectNumber
        this.props.add(value * 1)
    }
    decrement = () => {
        const { value } = this.selectNumber
        this.props.sub(value * 1)
    }
    incrementIdOdd = () => {
        const { value } = this.selectNumber
        if (this.props.count % 2 !== 0) {
            this.props.add(value * 1)
        }
    }
    incremenAsync = () => {
        const { value } = this.selectNumber
        this.props.addAsync(value * 1)
    }
    render() {
        console.log('@@@11', this.props);
        return (
            <div>
                <h1>当前求和为:{this.props.count}</h1>
                <select ref={c => this.selectNumber = c}>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                </select>&nbsp;&nbsp;
                <button onClick={this.increment}>+</button>&nbsp;&nbsp;
                <button onClick={this.decrement}>-</button>&nbsp;&nbsp;
                <button onClick={this.incrementIdOdd}>奇数再加</button>&nbsp;&nbsp;
                <button onClick={this.incremenAsync}>异步加</button>
            </div>
        );
    }
}

//使用connect()创建并暴露一个Count的容器组件
export default connect(
    state => ({ count: state }),
    {
        add: createIncrementAction,
        sub:createDecrementAction,
        addAsync:createIncrementAsyncAction
    }
)(Count)
```

优化总结：

```pascal
(1).容器组件和UI组件整合一个文件
(2).无需自己给容器组件传递store，给<App/>包裹一个<Provider store={store}>即可。
(3).使用了react-redux后也不用再自己检测redux中状态的改变了，容器组件可以自动完成这个工作。(4).mapDispatchToProps也可以简单的写成一个对象
(5).一个组件要和redux“打交道”要经过那几步?
	(1).定义好UI组件---不暴露
	(2).引入connect生成一个容器组件，并暴露，写法如下: connect(state => ({key:value})  {key:xxxxxAction})(UI组件)
(6).在UI组件中通过this.props.xxxxxxx读取和操作状态
```

### 7.5 求和案例数据共享版

(1).定义一个Pserson组件，和Count组件通过redux共享数据。
(2).为Person组件编写:reducer、action，配置constant常量。
(3).重点:Person的reducer和Count的Reducer要使用combineReducers进行合并，
合并后的总状态是一个对象!!!
(4).交给store的是总reducer，最后注意在组件中取出状态的时候，记得“取到位”。





![image-20240122103530411](D:\typora_photo\image-20240122103530411.png)





### 7.6 纯函数

1. 一类特别的函数: **只要是同样的输入(实参)，必定得到同样的输出(返回)**

2. 必须遵守以下一些约束 

- **不得改写参数数据**

- 不会产生任何副作用，例如网络请求，输入和输出设备

- 不能调用Date.now()或者Math.random()等不纯的方法 

3. **redux的reducer函数必须是一个纯函数**

   ```jsx
   case ADD_PERSON:
   //添加一个人后页面没有任何改变，因为redux底层对perState进行浅比较，如果perState地址不变就不会更新状态
   //在数组中添加一个元素，其地址是不会改变的，而重新生成一个数组才会引起redux的监测更新
   //这样子写导致perState被改写了就不是纯函数了
       perState.unshift(data) 
       return perState
   ```

### 7.7 高阶函数

1. 理解: 一类特别的函数

- 情况1: 参数是函数
- 情况2: 返回是函数

2. 常见的高阶函数: 

- 定时器设置函数
- 数组的forEach()/map()/filter()/reduce()/find()/bind()
-  promise

3.react-redux中的connect函数

- 作用: 能实现更加动态, 更加可扩展的功能

### 7.8 redux调试工具

### 7.8.1 chrome浏览器插件

![img](D:\typora_photo\wps1-1705891900439-1.jpg) 

### 7.8.2 下载工具依赖包才能使用开发者工具

​	npm install --save-dev redux-devtools-extension

```jsx
//最后在 store.js 进行配置：
import { composeWithDevTools } from 'redux-devtools-extension'
...
export default createStore(Reducers, composeWithDevTools(applyMiddleware(thunk)))
// 不需要异步中间件
export default createStore(Reducers, composeWithDevTools())
```

### 7.9 求和案例完整版

(1) 所有变量名字要规范，尽量触发对象的简写形式。
(2) reducers文件夹中，编写index.js专门用于汇总并暴露所有的reducer







### 7.10 项目打包运行

运行命令：`npm run build` 进行项目打包，生成 `build` 文件夹存放着打包完成的文件。

运行命令：`npm i serve -g` 全局安装 `serve` ，它能够以当前目录为根目录开启一台服务器，进入 `build` 文件夹所在目录，运行 `serve` 命令即可开启服务器查看项目效果。







ajax发送请求的方式jsx
1、xhr (jquery/axios是xhr的封装)

2、fetch与xhr并列
