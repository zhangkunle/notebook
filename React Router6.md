# React Router

**以下内容基于React Router6版本**

## 一.概述 

1. React Router 以三个不同的包发布到npm上，它们分别为:

  (1) react-router:路由的核心库，提供了很多的:组件、钩子。
  (2) react-router-dom:**包含react-router所有内容，并添加一些专门用于DOM 的组件**,<BrowserRouter>.
  (3) react-router-native:包括react-router所有内容，并添加一些专门用于ReactNative的API，例如:<NativeRouter>等。

  2.与React Router 5.x版本相比，改变了什么?
      (1) 内置组件的变化:移除<Switch/>，新增<Routes/>等。
      (2) 语法的变化:component={About}变为element={<About/>}等。
      (3) 新增多个hook: useParams、 useNavigate、 useMatch等。
      (4) **官方明确推荐函数式组件了!!!**



## 二、基础API

### 1、BrowserRouter

1.说明:<BrowserRouter>用于包裹整个应用。使用history模式

2.示例代码:

```js
import React from 'react'
import App from './App'
import { createRoot } from 'react-dom/client';
import { BrowserRouter } from 'react-router-dom'
export const root = createRoot(document.getElementById('root'));
root.render(<BrowserRouter><App /></BrowserRouter>);
```

### 2、HashRouter

1. 说明:作用与<BrowserRouter>一样，但<HashRouter>修改的是地址栏的hash值。使用hash模式
2. 备注:6.x版本中<HashRouter> 、<BrowserRouter> 的用法与5.x相同。

   3.Router中包含了对路径改变的监听，并且会将相应的路径传递给子组件

### 3、Routes与Route

```
1.v6版本中移出了先前的<switch>，引入了新的替代者:<Routes>；
2. <Routes>和<Route>要配合使用，且必须要用<Routes>包裹<Route>。
3.<Route>相当于一个if语句，如果其路径与当前URL 匹配，则呈现其对应的组件。
4.<Route casesensitive>属性用于指定:匹配时是否区分大小写(默认为false)。
5.当URL发生变化时，<Routes>都会查看其所有子<Route>元素以找到最佳匹配并呈现组件.
6.<Route>也可以嵌套使用，且可配合useRoutes()配置“路由表”，但需要通过<Outlet>组件来渲染其子路由。
```

```jsx
 import { Route, Routes } from 'react-router-dom'
<div class="panel-body">
     <Routes>
     <Route path="/ABOUT" caseSensitive element={<About />} /> {/*组件不显示*/}
     <Route path="/home" element={<Home />} />
     </Routes>
</div>
```

```jsx
<Routes>
/*path属性用于定义路径，element属性用于定义当前路径所对应的组件*/
    <Route path="/login" element={<Login />}></Route>
    
/*用于定义嵌套路由，home是一级路由，对应的路径/home*/
    <Route path="home"element={<Home />}>
/*test1 和 test2是二级路由,对应的路径是/home/test1或/home/test2*/
        <Route path="testl" element={<Test/>}></Route>
        <Route gath="test2" element={<Test2/>}></Route>
    </Route>
    
//Route也可以不写element属性，这时就是用于展示嵌套的路由,所对应的路径是/users/xxx
    <Route path="users">
      <Route path="xxx" element={<Demo/>} />
    </Route>
</Routes>
```

### 4、Navigate

1.作用:只要<Navigate>组件被渲染，就会修改路径，切换视图。
2.replace属性用于控制跳转模式(push或replace，默认是push)，即默认replace={false}

3.~~Redirect用于路由的重定向，当这个组件出现时，就会执行跳转到对应的to路径中~~ **6版本中已删除Redirect，改为Navigate**

4.示例代码:

```jsx
import React,{usestate} from "react'
import {Navigate} from 'react-router-dom'
export default function Home(){ 
    const [sum,setSum] = usestate(1) 
    return (
          <div>
          <h3>我是Home的内容</h3>
          {/*根据sum的值决定是否切换视图*/}
          {sum === 2 ? <h4>sum的值为{sum}</h4> : <Navigate to="/about" replace={true}/>}             <button onclick={()=>setsum(2)}>点我将sum变为2</button></div>
    )}
```

### 5、Link

通常路径的跳转是使用Link组件，最终会被渲染成a元素

### 6、NavLink

1.作用:与<Link>组件类似，且可实现导航的“高亮”效果。

NavLink是在Link基础之上增加了一些样式属性

- ~~activeStyle：活跃时（匹配时）的样式~~**6版本中已删除**
- ~~activeClassName：活跃时添加的class~~**6版本中已删除**
- ~~在默认匹配成功时，NavLink就会添加上一个动态的active class~~**6版本中已删除**
- 6版本中设置NavLink样式的方式为在className中设置函数，通过判断isActive的值来增加相关类型

```jsx
function computedClassName({ isActive }) {
    return isActive ? 'list-group-item atguigu' : 'list-group-item'
 }
 <div className="list-group">
  //写法一
   <NavLink className={computedClassName} to="/about">About</NavLink>
  //写法二
  <NavLink className={({isActive})=>isActive ? 'list-group-item atguigu' : 'list-group-item'} to="/about">About</NavLink>
  <NavLink className={computedClassName} to="/home">Home</NavLink>
</div>
```

```jsx
//注意:Navlink默认类名是active,下面是指定自定义的class
//自定义样式
<NavLink
   to="login"
   className={({ isActive }) =>{return isActive? 'base one' :'base'}}>login</NavLink>

//默认情况下，当Home的子组件匹配成功，Home的导航也会高亮，
//当NavLink上添加了end属性后，若Home的子组件匹配成功，则Home的导航没有高亮效果。
<NavLink to-"home" end >home</NavLink>
```

### 7、Outlet

1.当<Route>产生嵌套时，渲染其对应的后续子路由。

嵌套路由

- 在父组件内用`<Outlet />`来指定路由展示位置

- 嵌套路由在路由跳转时可简写to的值，即路由不需要写完整的路由，简写时自动将该路由拼接到当前路由下

  ```
  <NavLink className="list-group-item" to="news">News</NavLink>
  ```

2.示例代码:

```js
//根据路由表生成对应的路由规则 
//index.js
const routes = [
  {
    path: '/about',
    element: <About />
  },
  {
    path: '/home',
    element: <Home />,
    children: [
      {
        path: 'message',
        element: <Message />,
        children: [
          {
            path: 'detail',
            element: <Details />
          }
        ]
      },
  }
 ]
 //home.jsx
 import React from 'react'
import { NavLink, Outlet } from 'react-router-dom'
export default function Home() {
    return (
      <div>
         <h1>我是Home内容</h1>
         <div>
         <ul className="nav nav-tabs">
           <li>
            <NavLink className="list-group-item" to="news">News</NavLink>
           </li>
           <li>
             <NavLink className="list-group-item " to="message">Message</NavLink>
           </li>
         </ul>
        {/* 指定路由组件出现的位置*/}
         <Outlet />
      </div>
   </div>
    )
}
```

## 三、Hooks

### 1、useRoutes

作用：根据路由表，动态创建<Routes>和<Route>

1、定义路由文件。与vue-router类似，区别如下：

- element属性用来展示组件
- 在使用嵌套路由时，子路由的path最前面不加'/'

2、使用路由。在App.js文件内使用如下，其中routes为路由文件

- 声明路由

  ```
  const element = useRoutes(routes)
  ```

- 注册路由

  ```
  {element}
  ```


```js
import About from "../pages/About"
import Home from "../pages/Home"
import Message from "../pages/Message"
import Details from "../pages/Details"
import News from "../pages/News"
import { Navigate } from 'react-router-dom'
const routes = [
  {
    path: '/about',
    element: <About />
  },
  {
    path: '/home',
    element: <Home />,
    children: [
      {
        path: 'message',
        element: <Message />,
        children: [
          {
            path: 'detail',
            element: <Details />
          }
        ]
      },
      {
        path: 'news',
        element: <News />
      }
    ]
  },
  {
    path: '/',
    element: <Navigate to='/about' />
  }
]
export default routes;
```

```jsx
//App.js
import { NavLink, useRoutes } from 'react-router-dom'
import routes from './routes/index'
export default function App() {
  //根据路由表生成对应的规则
  const element = useRoutes(routes)
  return (
    <div>
      <div className="row">
        <div className="col-xs-offset-2 col-xs-8">
          <div className="page-header"><h2>React Router Demo</h2></div>
        </div>
      </div>
      <div className="row">
        <div className="col-xs-2 col-xs-offset-2">
          <div className="list-group">
            <NavLink className='list-group-item' to="/about">About</NavLink>
            <NavLink className='list-group-item' end to="/home">Home</NavLink>
          </div>
        </div>
        <div className="col-xs-6">
          <div className="panel">
            <div class="panel-body">
              {element}
            </div>
          </div>
        </div>
      </div>
    </div>
  )
}
```



### 2、useNavigate

作用:返回一个函数用来实现编程式导航。

基本使用：

> ​    const navigate = useNavigate()
>
>    方式一：指定路径
>
>    navigate('detail', {
>             replace: false,
>             state: {
>                 id: m.id,
>                 title: m.title,
>                 content: m.content
>             }
>         })
>
>   方式二：指定前进后退步数
>
>   navigate(-1)

```jsx
import React, { useState } from 'react'
import { Link, Outlet, useNavigate } from 'react-router-dom'
export default function Message() {
    const [messages] = useState([
        { id: '001', title: '消息1', content: '锄禾日当午' },
        { id: '002', title: '消息2', content: '汗滴禾下土' },
        { id: '003', title: '消息3', content: '谁知盘中餐' },
        { id: '004', title: '消息4', content: '粒粒皆辛苦' }
    ])
    const navigate = useNavigate()
    function showDetails(m) {
        //方式一：指定具体路径
        // navigate('/about')
        navigate('detail', {
            replace: false,
            state: {
                id: m.id,
                title: m.title,
                content: m.content
            }
        })
    }
    return (
        <div>
            <ul>
                {
                    messages.map((m) => {
                        return (
                            <li key={m.id}>
                                <Link
                                    to="detail"
                                    state={{
                                        id: m.id,
                                        title: m.title,
                                        content: m.content
                                    }}
                                >{m.title}</Link>
                                &nbsp;&nbsp;
                                <button onClick={() => showDetails(m)}>查看详情</button>
                            </li>
                        )
                    })
                }
            </ul>
            <Outlet />
        </div >
    )
}
```

![image-20240124212606793](D:\typora_photo\image-20240124212606793.png)

**一般组件实现编程式路由导航**

```jsx
import React from 'react'
import { useNavigate } from 'react-router-dom'
export default function Header() {
    const navigate = useNavigate()

    function back() {
        //方式二：指定前进后退步数
        navigate(-1)
    }
    function forward() {
        navigate(1)
    }
    return (
        <div className="col-xs-offset-2 col-xs-8">
            <div className="page-header">
                <h2>React Router Demo</h2>
                <button onClick={back}> ←后退</button>
                <button onClick={forward}>前进→</button>
            </div>

        </div>
    )
}
```

### 3、useParams

作用:回当前匹配路由的params 参数，类似于5.x中的match. params。

```jsx
import React from 'react'
import { useParams } from 'react-router-dom'
export default function Details() {
    const { id, title, content } = useParams()
    return (
        <ul>
            <li>{id}</li>
            <li>{title}</li>
            <li>{content}</li>
        </ul>
    )
}

```

![image-20240124152617099](D:\typora_photo\image-20240124152617099.png)

与此功能相似的hook为useMatch。

### 4、useSearchParams

1.作用:用于读取和修改当前位置的URL 中的查询字符串。
2.返回一个包含两个值的数组，内容分别为:当前的seaech参数、更新search的函数。

```jsx
import React from 'react'
import { useSearchParams,useLocation } from 'react-router-dom';
export default function Details() {
    const [search,setSearch] = useSearchParams()
    const id=search.get('id');
    const title=search.get('title');
    const content = search.get('content');
    const x = useLocation()
    console.log(x);
    return (
        <ul>
            <li>
                <button onClick={()=>setSearch('id=005&title=消息5&content=悯农')}>点我更新一下search参数</button>
            </li>
            <li>消息编号：{ id}</li>
            <li>消息标题：{title}</li>
            <li>消息内容：{content}</li>
        </ul>
    )
}
```

![image-20240124214350040](D:\typora_photo\image-20240124214350040.png)

与此功能相似的hook为useLocation

### 5、useLocation

1.作用:获取当前location信息，对标5.x中的路由组件的location属性。

```jsx
import React from 'react'
import {useLocation } from 'react-router-dom';
export default function Details() {
    const x = useLocation()
    console.log(x);
}
```

![image-20240124163603258](D:\typora_photo\image-20240124163603258.png)

### 6、useMatch

1.作用:返回当前匹配信息，对标5.x中的路由组件的match属性。

```jsx
import { useParams,useMatch } from 'react-router-dom'
export default function Details() {
    const { id, title, content } = useParams()
    const x = useMatch('/home/message/detail/:id/:title/:content')
    console.log(x);
}
```

![image-20240124152407732](D:\typora_photo\image-20240124152407732.png)

### 7、useInRouterContext()

作用:如果组件在<Router>的上下文中呈现，则useInRouterContext钩子返回true，否则返回 false。

![image-20240124203315266](D:\typora_photo\image-20240124203315266.png)

### 8、useNavigationType

1.作用:**返回当前的导航类型**(用户是如何来到当前页面的)。
2.返回值:POP PUSH REPLACE。 
3.备注:POP 是指在浏览器中直接打开了这个路由组件(刷新页面)。

```jsx
import React from 'react'
import { useNavigationType } from 'react-router-dom'
export default function News() {
    console.log(useNavigationType()); //刷新页面---POP  进入页面PUSH
    return (
        <div>
            <ul>
                <li>news001</li>
                <li>news002</li>
                <li>news003</li>
            </ul>
        </div>
    )
}
```

### 9、useOutlet

1.作用:用来呈现当前组件中要渲染的嵌套路由。
2.示例代码:

```jsx
const result = use0utlet() 
console.log(result)
//如果嵌套路由没有桂载,则result为null
//如果嵌套路由已经挂载,则展示嵌套的路由对象
```

![image-20240124211427318](D:\typora_photo\image-20240124211427318.png)



### 10、useResolvedPath

作用：给定一个URL值，解析其中的：path、search、hash值

```jsx
import React from 'react'
import {useResolvedPath } from 'react-router-dom'
export default function News() {
    console.log('useResolvedPath',useResolvedPath('/user?id=001&name=tom#qwe'));
    return (
        <div>
            <ul>
                <li>news001</li>
                <li>news002</li>
                <li>news003</li>
            </ul>
        </div>
    )
}
```

![image-20240124204851480](D:\typora_photo\image-20240124204851480.png)



## 路由传参（见 Detail 页面）

1. params参数

   - 路由跳转

   ```jsx
   <Link to={`detail/${item.id}/${item.title}/${item.content}`}>{item.content}</Link>
   ```

   - 路由配置

   ```jsx
......
   {
     path: 'message',
     element: <Message />,
     children: [
       {
         path: 'detail/:id/:title/:content',
         element: <Detail />
       }
     ]
   }
   ```
   
   - 接收参数。使用useParams()

   ```jsx
const { id, title, content } = useParams()
   ```

2. search参数

   - 路由跳转

   ```jsx
   <Link to={`detail?id=${item.id}&title=${item.title}&content=${item.content}`}>{item.content}</Link>
   ```

   - 路由配置

   ```jsx
   ......
   {
    path: 'message',
    element: <Message />,
    children: [
      {
        path: 'detail',
        element: <Detail />
      }
    ]
   }
   ```
   
   - 接收参数。使用useSearchParams()

   ```jsx
   const [search] = useSearchParams()
   const id = search.get('id')
   const title = search.get('title')
   const content = search.get('content')
   ```
   
3. state参数

   - 路由跳转

   ```jsx
   <Link to="detail" state={{
    id: item.id,
    title: item.title,
    content: item.content
   }}>
    {item.content}
   </Link>
   ```

   - 路由配置

   ```jsx
   ......
   {
    path: 'message',
    element: <Message />,
    children: [
      {
        path: 'detail',
        element: <Detail />
      }
    ]
   }
   ```
   
   

   - 接收参数。使用useLocation()

   ```jsx
   const { state: { id, title, content } } = useLocation()
   ```
   
   

## 编程式路由导航

通过useNavigate()来实现，如下。navigate()中还可直接传入数字实现前进后退

```
const navigate = useNavigate()
function jumpDetail(item) {
 navigate('detail', {
   replace: false,
   state: {
     id: item.id,
     title: item.title,
     content: item.content
   }
 })
}

......

<li key={item.id}>
 <button onClick={() => jumpDetail(item)}>跳转到详情{item.id}</button>
</li>
```