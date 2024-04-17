## 1. setState

### setState更新状态的2种写法

```
	(1). setState(stateChange, [callback])------对象式的setState
            1.stateChange为状态改变对象(该对象可以体现出状态的更改)
            2.callback是可选的回调函数, 它在状态更新完毕、界面也更新后(render调用后)才被调用
					
	(2). setState(updater, [callback])------函数式的setState
            1.updater为返回stateChange对象的函数。
            2.updater可以接收到state和props。
            4.callback是可选的回调函数, 它在状态更新、界面也更新后(render调用后)才被调用。
总结:
		1.对象式的setState是函数式的setState的简写方式(语法糖)
		2.使用原则：
				(1).如果新状态不依赖于原状态 ===> 使用对象方式
				(2).如果新状态依赖于原状态 ===> 使用函数方式
				(3).如果需要在setState()执行后获取最新的状态数据, 
					要在第二个callback函数中读取
		3.setState状态更新是异步的
```

案例：求和

```jsx
//1_setState/index.jsx
import React, { Component } from 'react'
export default class Demo extends Component {
    state = { count: 0 }
    add = () => {
        //写法一-----对象式setState
        // const { count } = this.state
        // this.setState({ count: count + 1 }, () => {
        //     console.log('（回调）求和：'+this.state.count); 
        // })
        // console.log('求和：',count);//点击一次添加后是0，没有改变值，因为setState引起react更新后续动作是异步的
       
        //写法二----函数式setState（新状态依赖旧状态函数式更方便）
        this.setState((state, props) => {
            // console.log(state, props);
            return { count: state.count + 1 }
        },
            () => {
                console.log('求和为' + this.state.count);
            })
        //简写形式
        this.setState(state => ({ count: state.count + 1 }))
    }
    render() {
        return (
            <div>
                <h2>当前求和为：{this.state.count}</h2>
                <button onClick={this.add}>点我加1</button>
            </div>
        )
    }
}
```

![image-20240122162604068](D:\typora_photo\image-20240122162604068.png)![image-20240122162946834](D:\typora_photo\image-20240122162946834.png)

- React 状态更新是异步的。下述代码打印的 `count` 值是上一次的值，而非更新后的。可在第二个参数回调中获取更新后的状态。

```js
add = () => {
  this.setState({ count: this.state.count + 1 })
  console.log(this.state.count)
}

add = () => {
  this.setState({ count: this.state.count + 1 }, () => {
    console.log(this.state.count)
  })
}
```

- `callback` 回调在 `componentDidMount` 钩子之后执行

## 2. 路由组件懒加载LazyLoad

```js
	//1.通过React的lazy函数配合import()函数动态加载路由组件 ===> 路由组件代码会被分开打包
	const Login = lazy(()=>import('@/pages/Login'))
	
	//2.通过<Suspense>指定在加载得到路由打包文件前显示一个自定义loading界面
	<Suspense fallback={<h1>loading.....</h1>}>
        <Switch>
            <Route path="/xxx" component={Xxxx}/>
            <Redirect to="/login"/>
        </Switch>
    </Suspense>
```

------

当点击一个路由导航时，第一次会在网络请求选项中出现，第二次则不会，是走缓存了。

![image-20240122205745892](D:\typora_photo\image-20240122205745892.png)

## 3. Hooks

在React 16.8.0版本之前函数式组件没有自己的this，不能使用state和ref，React 16.8.0版本之后就有可以解决的办法了。

#### 1. React Hook/Hooks是什么?

```
(1). Hook是React 16.8.0版本增加的新特性/新语法
(2). 可以让你在函数组件中使用 state 以及其他的 React 特性
```

#### 2. 三个常用的Hook

```
(1). State Hook: React.useState()
(2). Effect Hook: React.useEffect()
(3). Ref Hook: React.useRef()
```

React.useState()

![image-20240122211451205](D:\typora_photo\image-20240122211451205.png)![image-20240122211517839](D:\typora_photo\image-20240122211517839.png)

#### 3. State Hook

```
(1). State Hook让函数组件也可以有state状态, 并进行状态数据的读写操作
(2). 语法: const [xxx, setXxx] = React.useState(initValue)  
(3). useState()说明:
        参数: 第一次初始化指定的值在内部作缓存
        返回值: 包含2个元素的数组, 第1个为内部当前状态值, 第2个为更新状态值的函数
(4). setXxx()2种写法:
        setXxx(newValue): 参数为非函数值, 直接指定新的状态值, 内部用其覆盖原来的状态值
        setXxx(value => newValue): 参数为函数, 接收原本的状态值, 返回新的状态值, 内部用其覆盖原来的状态值
```

```jsx
const [count, setCount] = React.useState(0) 
const [name, setName] = React.useState('Tom') 
function add() {  
   setCount(count + 1)  
   setCount((count) => count + 1)
  }
 function changeName() {
   setName('jack')
}
```

#### 4. Effect Hook

```
(1). Effect Hook 可以让你在函数组件中执行副作用操作(用于模拟类组件中的生命周期钩子)
(2). React中的副作用操作:
        发ajax请求数据获取
        设置订阅 / 启动定时器
        手动更改真实DOM
(3). 语法和说明: 
        useEffect(() => { 
          // 在此可以执行任何带副作用操作
          return () => { // 在组件卸载前执行
          // 在此做一些收尾工作, 比如清除定时器/取消订阅等
          }
        }, [stateValue]) // 如果指定的是[], 回调函数只会在第一次render()后执行，
          //当stateValue的值改变时，就会触发useEffect函数里面的副作用操作
    
(4). 可以把 useEffect Hook 看做如下三个函数的组合
        componentDidMount()
        componentDidUpdate()
    	componentWillUnmount() 
```

一个坑：https://blog.csdn.net/weixin_38629529/article/details/126554759

react18版本卸载组件的方式：获取节点.unmount()

react16版本卸载组件的方式：ReactDOM.unmountComponentAtNode(获取节点)

​        在卸载组件的过程中，如果直接卸载根结点root是可以卸载成功的，那如果我新增一个`dom`节点，并且该节点并不是直接放在`ReactDOM.render`里渲染的，而是通过`appendChild`插入到`root`下的。这个节点在我卸载`root`的时候，**是不会被卸载掉**。

​       **总之，`unmountComponentAtNode`只对`ReactDOM.render`挂载在顶层的组件才生效，其余无关`render`方法永远返回的都是`false`，如果想要插入的元素也被卸载掉，可以插入到`App.js`的节点中，不要直接插入到根节点。**

- `React.useEffect` 第一个参数 `return` 的函数相当于 `componentWillUnmount` ，若有多个会按顺序执行

```js
// 语法
React.useEffect(() => {
  ...
  return () => {
    // 组件卸载前执行，即 componentWillUnmount 钩子
    ...
  }
}, [stateValue])

// 模拟 componentDidMount
// 第二个参数数组为空，表示不监听任何状态的更新
// 因此只有页面首次渲染会执行输出
React.useEffect(() => {
  console.log('DidMount')
  return () => {
    console.log('WillUnmount 1')
  }
}, [])

// 模拟全部状态 componentDidUpdate
// 若第二个参数不写，表示监听所有状态的更新
React.useEffect(() => {
  console.log('All DidUpdate')
  return () => {
    console.log('WillUnmount 2')
  }
})

// 模拟部分状态 componentDidUpdate
// 第二个参数数组写上状态，表示只监听这些状态的更新
React.useEffect(() => {
  console.log('Part DidUpdate')
  return () => {
    console.log('WillUnmount 3')
  }
}, [count, name])

// 若调用 ReactDOM.unmountComponentAtNode(document.getElementById('root'))
// 会输出 WillUnmount 1、2、3
```

```jsx
import React from 'react'
// import  ReactDOM  from 'react-dom'
import { root } from '../../index'
// 类式组件写法
// export default class Demo extends React.Component {
//     state = { count: 0 }
//     add = () => {
//         this.setState(state => ({ count: state.count + 1 }))
//     }
//     unmount = () => {
//         // ReactDOM.unmountComponentAtNode(document.getElementById('root')) 16版本写法
//         root.unmount()
//     }
//     addDom = () => {
//         const div = document.createElement('div');
//         div.innerHTML = '不可卸载组件'
//         document.getElementById('root').appendChild(div);
//     }
//     componentDidMount() {
//         this.timer = setInterval(() => {
//             this.setState(state => ({ count: state.count + 1 }))
//         }, 1000);
//     }
//     componentWillUnmount() {
//         clearInterval(this.timer)
//     }
//     render() {
//         return (
//             <div>
//                 <h2>当前求和为：{this.state.count}</h2>
//                 <button onClick={this.add}>点我加1</button>&nbsp;
//                 <button onClick={this.unmount}>卸载组件</button>&nbsp;
//                 <button onClick={this.addDom}>新增DOM</button>&nbsp;
//             </div>
//         )
//     }
// }

function Demo() {
    // console.log('DEMO');//调用1+n次（初始化+render)
    const [count, setCount] = React.useState(0)//后面会覆盖值
    const [name, setName] = React.useState(0)//后面会覆盖值

    React.useEffect(() => {
        let timer=setInterval(() => {
            setCount(count => count + 1)
        }, 1000);
        return () => {
           clearInterval(timer)
        }
    },[count])

    //加的回调
    function add() {
        //第一种写法
        // setCount(count+1)
        //第二种
        setCount(count => count + 1)
    }
    function changeName() {
        setName('jack')
    }
   function unmount() {
    root.unmount()
   }
    return (
        <div>
            <h2>当前求和为：{count}</h2>
            <h2>我的名字是：{name}</h2>
            <button onClick={add}>点我加1</button>&nbsp;
            <button onClick={changeName}>点我改名</button>
            <button onClick={unmount}>卸载组件</button>
        </div>
    )
}
export default Demo;
```

![image-20240123104027717](D:\typora_photo\image-20240123104027717.png)

#### 5. Ref Hook

```
(1). Ref Hook可以在函数组件中存储/查找组件内的标签或任意其它数据
(2). 语法: const refContainer = useRef()
(3). 作用:保存标签对象,功能与React.createRef()一样
```

```jsx
function Demo() {
  const myRef = React.useRef()

  function show() {
    console.log(myRef.current.value)
  }

  return (
    <div>
      <input type="text" ref={myRef} />
      <button onClick={show}>展示数据</button>
    </div>
  )
}
```

------

![image-20240123110725980](D:\typora_photo\image-20240123110725980.png)

## 4. Fragment

#### 使用

	<Fragment><Fragment>
	<></>

#### 作用

> 可以不用必须有一个真实的DOM根标签

<hr/>

## 5. Context

### 理解

> 一种组件间通信方式, 常用于【祖组件】与【后代组件】间通信

### 使用

```js
1) 创建Context容器对象：
	const XxxContext = React.createContext()  
	
2) 渲染子组时，外面包裹xxxContext.Provider, 通过value属性给后代组件传递数据：
	<xxxContext.Provider value={数据}>
		子组件
    </xxxContext.Provider>
    
3) 后代组件读取数据：

	//第一种方式:仅适用于类组件 
	  static contextType = xxxContext  // 声明接收context
	  this.context // 读取context中的value数据
	  
	//第二种方式: 函数组件与类组件都可以
	  <xxxContext.Consumer>
	    {
	      value => ( // value就是context中的value数据
	        要显示的内容
	      )
	    }
	  </xxxContext.Consumer>
```

### 注意

	在应用开发中一般不用context, 一般都用它的封装react插件

举个栗子：

```js
// context.js

import React from 'react'
export const MyContext = React.createContext()
export const { Provider, Consumer } = MyContext
// A.jsx
import React, { Component } from 'react'
import B from './B.jsx'
import { Provider } from './context.js'

export default class A extends Component {
  state = { username: 'tom', age: 18 }
  render() {
    const { username, age } = this.state
    return (
      <div>
        <h3>A组件</h3>
        <h4>用户名是:{username}</h4>
        <Provider value={{ username, age }}>
          <B />
        </Provider>
      </div>
    )
  }
}

// B.jsx
import React, { Component } from 'react'
import C from './C.jsx'
export default class B extends Component {
  render() {
    return (
      <div>
        <h3>B组件</h3>
        <C />
      </div>
    )
  }
}
// C.jsx

import React, { Component } from 'react'
import { MyContext } from './context.js'

export default class C extends Component {
  static contextType = MyContext
  render() {
    const { username, age } = this.context
    return (
      <div>
        <h3>C组件</h3>
        <h4>
          从A组件接收到的用户名:{username},年龄:{age}
        </h4>
      </div>
    )
  }
}
// C.jsx 为函数式组件

import { Consumer } from './context.js'
export default function C() {
  return (
    <div>
      <h3>我是C组件</h3>
      <h4>
        从A组件接收到的用户名:
        <Consumer>{(value) => `${value.username},年龄是${value.age}`}</Consumer>
      </h4>
    </div>
  )
}
```

<hr/>

![image-20240123134127810](D:\typora_photo\image-20240123134127810.png)

## 6. 组件优化

#### Component的2个问题 

> 1. **只要执行setState(),即使不改变状态数据, 组件也会重新render() ==> 效率低**
>
> 2. 只当前组件重新render(), 就会自动重新render子组件，纵使子组件没有用到父组件的任何数据 ==> 效率低

#### 效率高的做法

>  只有当组件的state或props数据发生改变时才重新render()

#### 原因

>  Component中的shouldComponentUpdate()总是返回true

#### 解决

	办法1: 
		重写shouldComponentUpdate()方法
		比较新旧state或props数据, 如果有变化才返回true, 如果没有返回false
		缺点:当state中数据太多时无法一一比较，效率低
	办法2:  
		使用PureComponent
		PureComponent重写了shouldComponentUpdate(), 只有state或props数据有变化才返回true
		注意: 
			只是进行state和props数据的浅比较, 如果只是数据对象内部数据变了, 返回false  
			不要直接修改state数据, 而是要产生新数据
	项目中一般使用PureComponent来优化

```jsx
//方式一 自己写逻辑 ——重写shouldComponentUpdate()方法，让阀门根据是否有state改变状态值再调用render()
changCar = () => {
     this.setState({})
}
shouldComponentUpdate(nextProps, nextState) {
        console.log(nextProps, nextState);//接下来变化的目标props和state
        console.log(this.props, this.state);//现在的目标props和state
        return ！this.state.carname === nextState.carname) 
```

![image-20240123143316229](D:\typora_photo\image-20240123143316229.png)

<hr/>

```jsx
//方式二
import React, { PureComponent } from 'react'

class Demo extends PureComponent {
  ...
  addStu = () => {
    // 不会渲染
    const { stus } = this.state
    stus.unshift('小刘')
    this.setState({ stus })
     
     const obj = this.state 
   //obj和state是同一个对象，PureComponent底层浅对比会认为没有改变状态，与unshift类似，没有办法改变值
     obj.carname = '奥拓'
     console.log(obj ===this.state);//true
     this.setState(obj)

    // 重新渲染
    const { stus } = this.state
    this.setState({ stus: ['小刘', ...stus] })
  }
  ...
}
```

![image-20240123144628098](D:\typora_photo\image-20240123144628098.png)

## 7. render props

#### 如何向组件内部动态传入带内容的结构(标签)?   插槽

	Vue中: 
		使用slot技术, 也就是通过组件标签体传入结构  <A><B/></A>
	React中:
		使用children props: 通过组件标签体传入结构,不能携带数据传给子组件
		使用render props: 通过组件标签属性传入结构,而且可以携带数据，一般用render函数属性

### children props方式

	<A>
	  <B>xxxx</B>
	</A>
	{this.props.children}
	问题: 如果B组件需要A组件内的数据, ==> 做不到 

- 组件标签体内容会存储到 `this.props.children` 中
- 缺点：A 组件无法向 B 组件传递数据

```js
import React, { Component } from 'react'

export default class Parent extends Component {
  render() {
    return (
      <div>
        <h3>Parent组件</h3>
        <A>
          <B />
        </A>
      </div>
    )
  }
}

class A extends Component {
  state = { name: 'tom' }
  render() {
    return (
      <div>
        <h3>A组件</h3>
        {this.props.children}
      </div>
    )
  }
}

class B extends Component {
  render() {
    return (
      <div>
        <h3>B组件</h3>
      </div>
    )
  }
}
```

### render props

	<A render={(data) => <C data={data}></C>}></A>
	A组件: {this.props.render(内部state数据)}
	C组件: 读取A组件传入的数据显示 {this.props.data} 

```jsx
import React, { Component } from 'react'

export default class Parent extends Component {
  render() {
    return (
      <div>
        <h3>Parent组件</h3>
        <A render={(name) => <B name={name} />} />
      </div>
    )
  }
}

class A extends Component {
  state = { name: 'tom' }
  render() {
    const { name } = this.state
    return (
      <div>
        <h3>A组件</h3>
        {this.props.render(name)}
      </div>
    )
  }
}

class B extends Component {
  render() {
    return (
      <div>
        <h3>B组件,{this.props.name}</h3>
      </div>
    )
  }
}
```

![image-20240123151017817](D:\typora_photo\image-20240123151017817.png)

<hr/>

## 8. 错误边界

#### 理解：

错误边界(Error boundary)：用来捕获后代组件错误，渲染出备用页面。

注意：只在生产环境（项目上线）起效

#### 特点：

只能捕获**后代组件生命周期产生的错误**，不能捕获自己组件产生的错误和其他组件在合成事件、定时器中产生的错误，**简单理解就是只能捕获后代组件生命周期钩子里面代码的错误**

##### 使用方式：

getDerivedStateFromError配合componentDidCatch

```js
import React, { Component } from 'react'
import Child from './Child'

export default class Parent extends Component {
  state = {
    //用于标识子组件是否产生错误
    hasError: '',
  }

  // 当子组件出现错误，会触发调用，并携带错误信息
  // 生命周期函数，一旦后台组件报错，就会触发
  static getDerivedStateFromError(error) {
    // render 之前触发
    // 返回新的 state
    return { hasError: error }
  }

  componentDidCatch(error, info) {
    console.log(error, info)
    // 统计页面的错误。发送请求发送到后台去
    console.log('此处统计错误，反馈给服务器')
  }
  render() {
    return (
      <div>
        <h2>Parent组件</h2>
        {this.state.hasError ? <h2>网络不稳定，稍后再试</h2> : <Child />}
      </div>
    )
  }
}
```
![image-20240123162735576](D:\typora_photo\image-20240123162735576.png)

## 9. 组件通信方式总结

#### 组件间的关系：

- 父子组件
- 兄弟组件（非嵌套组件）
- 祖孙组件（跨级组件）

#### 几种通信方式：

		1.props：
			(1).children props
			(2).render props
		2.消息订阅-发布：
			pubs-sub、event等等
		3.集中式管理：
			redux、dva等等
		4.conText:
			生产者-消费者模式

#### 比较好的搭配方式：
		父子组件：props
		兄弟组件：消息订阅-发布、集中式管理
		祖孙组件(跨级组件)：消息订阅-发布、集中式管理、conText(开发用的少，封装插件用的多)

