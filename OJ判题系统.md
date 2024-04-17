##                                          OJ判题系统（umi+arco design）

### 一、做项目的流程

1、项目介绍、项目调研、需求分析

2、核心业务流程

3、项目要做的功能（功能模块）

4、技术选型（技术预研）

5、项目初始化(umi脚手架https://umijs.org/docs/guides/getting-started)

6、项目开发

7、测试

8、优化

9、代码提交，代码审核

10、产品验收

11、上线

写文档、持续调研、持续记录总结

### 二、Ant design v5

- 不再支持 `babel-plugin-import`，CSS-in-JS 本身具有按需加载的能力，不再需要插件支持。(无需手动设置按需加载样式了)

  > CSS-in-JS：是 WEB 项⽬中将 CSS 代码捆绑在 **JavaScript** 代码中的解决⽅案.这种⽅案旨在解决 CSS 的局限性, **例如缺乏动态功能, 作⽤域和可移植性.**
  >
  > 1、CSS-IN-JS ⽅案的优点：
  > 让 CSS 代码拥有独⽴的作⽤域, 阻⽌ CSS 代码泄露到组件外部, 防⽌样式冲突.
  > 让组件更具可移植性, 实现开箱即⽤, 轻松创建松耦合的应⽤程序
  > 让组件更具可重⽤性, 只需编写⼀次即可, 可以在任何地⽅运⾏. 不仅可以在同⼀应⽤程序中重⽤组件, ⽽且可以在使⽤相同框架构建的其他应⽤程序中重⽤组件.
  > 让样式具有动态功能, 可以将复杂的逻辑应⽤于样式规则, 如果要创建需要动态功能的复杂UI, 它是理想的解决⽅案.
  > 2、CSS-IN-JS ⽅案的缺点：
  > 为项⽬增加了额外的复杂性.
  > ⾃动⽣成的选择器⼤⼤降低了代码的可读性
  > 3、Emotion 是⼀个旨在使⽤ JavaScript 编写 CSS 样式的库
  >
  > npm install @emotion/core @emotion/styled

```jsx
import React from 'react';
/** @jsx jsx */
import {jsx} from '@emotion/core'
function App() {
  return <div css={{width: 200, height: 200,background: red}}></div>
}
```

### 三、arco design按需加载样式



### 四、项目中遇到的问题：

（1） 渐变色写法是background-image而不是backgroundColor

```css
  background-image: linear-gradient(to right, #5cd6e6, #a79df5);
```

（2）全局路由layout（上--中--下模式），实现全局路由页面的导航和登录注册页的不同页面跳转：

实现在全局布局文件中通过添加<OutLet/>实现子路由跳转，可以跳转到登录注册页面；

在通用布局文件中，通过在Content中添加<Outlet/>实现中部的导航切换展示效果；

路由配置：

```jsx
export default [
  {
    path: "/",
    component: "@/layouts/index",
    routes: [
      {
        path: "/",
        component: "@/layouts/BasicLayout/index",
        routes: [
          {
            path: "/home",
            name: "浏览题目",
            component: "@/pages/hu",
          },
          {
            path: "/about",
            name: "查看",
            component: "@/pages/docs",
          },
          {
            path: "/admin",
            name: "管理员可见",
            component: "@/pages/admin"
          },
          {
            path: "/noAuth",
            name: "无权限",
            component: "@/pages/noAuth",
          },
        ],
      },
      {
        path: "/login",
        component: "@/pages/Login/index",
      },
      {
        path: "/docs",
        component: "@/pages/docs",
      },
    ],
  },
];
```

```jsx
//layouts index.jsx
import "@arco-design/web-react/dist/css/arco.css";
import { Outlet } from "umi";
const index = () => {
  return (
    <div>
      <Outlet />
    </div>
  );
};
export default index;
```

```jsx
//BasicLayout.jsx
import { Layout } from "@arco-design/web-react";
import "../index.css";
import "@arco-design/web-react/dist/css/arco.css";
import GobalHeader from "../../components/GobalHeader/index";
import { Outlet } from "umi";
const { Header, Footer, Content } = Layout;
const index = () => {
  return (
    <div className="layout-basic-demo">
      <Layout style={{ height: "400px" }}>
        <Header className="header">
          <GobalHeader />
        </Header>
        <Content className="content">
          <Outlet />
        </Content>
        <Footer className="footer">
          <div>彗变OJ by zhangkl</div>
          <div>粤ICP备2024167901号-1</div>
        </Footer>
      </Layout>
    </div>
  );
};
export default index;
```

（3） 实现通用的路由菜单

目标：根据路由配置信息，自动生成菜单内容，实现更通用、更自动的菜单配置。（to do 写死菜单名）

- 提取通用路由文件
- 菜单组件读取路由，动态渲染菜单菜单项
- 绑定跳转事件
- 同步路由的更新到菜单项高亮

同步高亮原理:首先点击菜单项=>触发点击事件(onClickMenuItem)，跳转更新路由=>更新路由后，**同步去更新菜单栏的高亮状态**。

注意：首先将每一个菜单项的key设置为path路径，利用点击事件触发useNavigate实现菜单项跳转到对应的路由，利用useLocation()获得当前路由信息，并将路由信息的路径作为菜单的高亮项，更新路由后，同步去更新菜单栏的高亮状态。

```jsx
  const navigate = useNavigate();
  const arr = [
    { title: "Home", name: "/home" },
    { title: "About", name: "/about" },
    { title: "admin", name: "/admin" },
    {title: "noAuth", name: "/noAuth",},
  ];
  const [titleArr]: any = React.useState(arr);
  function doMenuClick(key: String) {
    navigate(`${key}`);
  }
  return (
    <div>
      <div className="menu-demo">
        <Menu
          mode="horizontal"
          selectedKeys={[useLocation().pathname]}
          onClickMenuItem={doMenuClick}
        >
          {titleArr.map((item: any) => {
            return <MenuItem key={item.name}>{item.title}</MenuItem>;
          })}
        </Menu>
      </div>
    </div>
  );
```

（4）全局状态管理-----react-redux

  **什么是全局状态管理?    所有页面全局共享的变量，而不是局限在某一个页面中。**
 适合作为全局状态的数据:已登录用户信息(每个页面几乎都要用)
 **具体实现步骤：**

创建redux/store.js文件，引入redux中的createStore函数，创建一个store

```jsx
//store.js
//暴露一个store对象，整个应用只有一个store
import { legacy_createStore as createStore } from "redux";
import reducer from './reducers/user'
const store = createStore(reducer);
export default store;
```

在全局layouts文件中引入，通过Provider传递store给组件

```jsx
import "@arco-design/web-react/dist/css/arco.css";
import { Outlet } from "umi";
import { Provider } from 'react-redux';
import store from '../redux/store'
const index = () => {
  return (
    <div>
      <Provider store={store}> <Outlet /></Provider>
    </div>
  );
};
export default index;
```

创建action.js，引入Action对象（type+data）

```jsx
export const updateUser = (data: any) => ({ type: 'UPDATEUSER', data })
```

创建reducer.js,对数据进行加工（初始化），对接收的data即用户的账号，直接返回即可

```jsx
//reducer，本质是一个函数
//reducer函数接收两个参数:之前的状态，动作对象
const initState = "未登录"; //初始化状态
export default function countReducer(preState = initState, action: any) {
  //从action对象中获取type和data
  const { type, data } = action;
  switch (type) {
    case 'UPDATEUSER':
      return data;
    //初始化
    default:
      return preState;
  }
}
```

靠react-redux的connect函数创建并暴露Gobaluser的容器组件,设置映射状态和操作映射状态的方法,在 React.useEffect钩子中更新用户名称，通过props.user获取用户名展示在页面上。

```jsx
import { connect } from "react-redux";
import { updateUser } from "@/redux/actions/user";
function User(props: any) {
  React.useEffect(() => {
    setTimeout(() => {
      props.updateUser("sunnyday");
    }, 2000);
  }, []);
  return (
    <div>
        <Button className="trigger-hover" style={{ backgroundColor: "#fff" }}>
          {props.user || "未登录"}
        </Button>
    </div>
  );
}
export default connect(
  (state: any) => ({
    user: state,
  }),
  (dispatch) => ({
    updateUser: (username: any) => dispatch(updateUser(username)),
  })
)(User);
```

（5）全局权限管理

目标:能够直接以一套通用的机制，去定义哪个页面需要那些权限。而不用每个页面独立去判断权限，提高效率。

思路:
1.在路由配置文件，定义某个路由的访问权限
2.在全局页面组件app.vue中，绑定一个全局路由监听。每次访问页面时，根据用户要访问页面的路由
信息，先判断用户是否有对应的访问权限。
3.如果有，跳转到原页面;如果没有，拦截或跳转到401鉴权或登录页



#### 根据权限隐藏菜单

1）route.ts增加一个标志位

```js
       {
            path: "/hide",
            name: "隐藏",
            component: "@/pages/docs",
            meta: {
              hideInMenu: true,
            },
          },
```

2）根据路由自定义的meta的hideInMenu属性控制菜单的显隐

```jsx
<Menu
      mode="horizontal"
      selectedKeys={[useLocation().pathname]}
      onClickMenuItem={doMenuClick}
      className="menu-container">
     {titleArr.map((item: any,index:any) => {
      return item.meta?.hideInMenu ? (
      '' //这里不要用<></>
      ) : (
      <MenuItem className="menu_item_demo" key={item.path}>
      {item.name}
      </MenuItem>
    );
  })}
</Menu>
```

#### 全局权限管理

需求：具有权限的菜单才对用户可见

原理：类似上面的控制路由显示隐藏，只要用户没有这个权限就过滤掉

1）定义权限

```js
/*权限定义 */
const ACCESSENUM = {
  NOT_LOGIN: "notLogin",
  USER: "user",
  ADMIN: "admin",
};
export default ACCESSENUM;
```

2）定义一个通用的权限校验方法

因为菜单组件中要判断权限，权限拦截中也要判断权限，所以抽离成一个公共方法

创建checkAccess.js,专门用于检验权限的函数

```js
/**
 * 检查权限 判断当前用户需要某个权限
 * @param loginUser  当前登录用户
 * @param needAccess  需要有的权限
 * @return boolean 有无权限
 */
import ACCESS_ENUM from "./accessEnum";
const checkAccess = (
  loginUser: any,
  needAccess: String = ACCESS_ENUM.NOT_LOGIN
) => {
    
  //获取当前登录用户具有的权限
  const loginUserAccess = loginUser?.userRole ?? ACCESS_ENUM.NOT_LOGIN;
  if (needAccess === ACCESS_ENUM.NOT_LOGIN) {
    return true;
  }
    
  //需要用户登录就可以访问
  if (needAccess === ACCESS_ENUM.USER) {
    //如果无登录就不能访问
    if (loginUserAccess === ACCESS_ENUM.NOT_LOGIN) {
      return false;
    }
  }
    
  //如果需要管理员权限
  if (needAccess === ACCESS_ENUM.ADMIN) {
    //不为管理员就无权限
    if (loginUserAccess !== ACCESS_ENUM.ADMIN) {
      return false;
    }
    return true;
  }
};
export default checkAccess;
```

3）非容器组件使用redux数据----扩展

**使用 useStore 钩子**:

- `useStore` 钩子允许你直接访问 Redux store 对象，这样你可以调用 `getState` 来获取整个 store 的当前状态。

```jsx
import { useStore } from 'react-redux';
const NonConnectedComponent = () => {
  const store = useStore();
  const state = store.getState();
};
```

4）修改GobalHeader动态菜单组件，根据权限来过滤菜单

注意：当用户状态开始变化时，此时需要重新设置头部导航栏中使用的loginuser值，从而引发页面的重新渲染，展示新增的菜单项，不然会出现当用户名刷新时，菜单栏没有根据权限作出改变。

```tsx
//GobalHeader /index.tsx
//检验权限实现菜单显隐
  const visibleRoute = titleArr.filter((item: any) => {
    if (item.meta?.hideInMenu) { //隐藏项
      return false;
    }
    if (!checkAccess(loginUser, item.meta?.access)) {
      return false;
    }
    return true;
  });
```

初始化登录用户，并将设置方法传给子组件

```tsx
let [loginUser, setLoginUser]: any = React.useState({ username: '未登录', role: ACCESS_ENUM.NOT_LOGIN })    

<GobalUser setUserLogin={setLoginUser} />
```

5）全局项目入口

在layout /index.tsx中预留一个可以编写全局初始化逻辑的代码

```tsx
const doInit = () => {
    console.log('欢迎你呀');
  }

  useEffect(() => {
    doInit()
  })
```

### 前后端联调

1）安装Axios

下载依赖

```js
npm install axios
```

2）编写调用后端代码

传统————单独编写每个请求代码，至少写一个请求路径

自动生成即可————使用openapi

安装依赖：

```js
npm install openapi-typescript-codegen --save-dev
```

终端生成代码：

```js
npx openapi --input http://localhost:8101/api/v2/api-docs --output ./generated --client axios
```

请求示例写法：

```jsx
     const fetchData = async () => {
      const res_current_user = await UserControllerService.getLoginUserUsingGet();
      if (res_current_user.code === 0) {
        const perobj = { username: res_current_user.data?.userName, role: res_current_user.data?.userRole };
        props.updateUser(perobj);
        props.setUserLogin(perobj);
      }else{
        const perobj = { username: '未登录', role:ACCESS_ENUM.NOT_LOGIN };
        props.updateUser(perobj);
      }
    };
```

如果要自定义请求参数，方法一使用代码生成器提供的全局参数修改对象：

```jsx
import type { ApiRequestOptions } from "./ApiRequestOptions";
type Resolver<T> = (options: ApiRequestOptions) => Promise<T>;
type Headers = Record<string, string>;
export type OpenAPIConfig = {
  BASE: string;
  VERSION: string;
  WITH_CREDENTIALS: boolean;
  CREDENTIALS: "include" | "omit" | "same-origin";
  TOKEN?: string | Resolver<string> | undefined;
  USERNAME?: string | Resolver<string> | undefined;
  PASSWORD?: string | Resolver<string> | undefined;
  HEADERS?: Headers | Resolver<Headers> | undefined;
  ENCODE_PATH?: ((path: string) => string) | undefined;
};

export const OpenAPI: OpenAPIConfig = {
  BASE: "http://localhost:8101",
  VERSION: "1.0",
  WITH_CREDENTIALS: true,
  CREDENTIALS: "include",
  TOKEN: undefined,
  USERNAME: undefined,
  PASSWORD: undefined,
  HEADERS: undefined,
  ENCODE_PATH: undefined,
};
```

方法二：直接定义axios请求库的全局参数，比如全局请求拦截器

```tsx
import axios from 'axios';
// 创建新的axios实例
const service = axios.create({
    baseURL: process.env.BASE_API, //这里使用了webpack中的全局变量
    timeout: 3 * 1000
})
//请求拦截器
service.interceptors.request.use(config => {
    //发请求前做的一些处理，数据转化，配置请求头，设置token，设置loading等,根据需求去添加
    config.data = JSON.stringify(config.data); //数据转化,也可以qs转换
    config.headers = {
            'Content-Type': 'application/x-www-form-urlencoded' //配置请求头
        }
    return config
}, error => {
    Promise.reject(error)
})
//响应拦截
service.interceptors.response.use(response => {
    //接收到响应数据并成功后的一些共有处理,关闭loading等
    return response
}, error => {
    //  接收到异常响应的处理开始
    if (error && error.response) {
        //1.公共错误处理
        //2,。根据响应码具体处理
        switch (error.response.status) {
            case 400:
                error.message = "错误请求"
                break;
            case 401:
                error.message = '未授权，请重新登录'
                break;
            default:
                error.message = `链接错误${error.response.status}`
        }
    } else {
        //超时处理
        if (JSON.stringify(error).includes('timeout')) {
            console.log('服务器响应超时，请刷新当前页')
        }
        error.message('连接服务器失败')
    }
    console.log(error.response)
    return Promise.resolve(error.response)
})
//导出文件
export default service
```

### 用户登录功能

#### 自动登录

1）在进入首页时编写获取远程登录用户信息的代码

```tsx
  React.useEffect(() => {
    const fetchData = async () => {
      const res_current_user = await UserControllerService.getLoginUserUsingGet();
      if (res_current_user.code === 0) {
        const perobj = { username: res_current_user.data?.userName, role: res_current_user.data?.userRole };
        props.updateUser(perobj);
        props.setUserLogin(perobj);
      }else{
        const perobj = { username: '未登录', role:ACCESS_ENUM.NOT_LOGIN };
        props.updateUser(perobj);
      }
    };
  setTimeout(() => {
     fetchData()
  }, 0);
  }, []);
```

### 全局权限管理优化

（根据对应权限展示相应的页面+在用户跳转路由时判断用户的登录状态）

在一个全局的位置----路由拦截中判断用户是否登录了

1）新建access/index.ts文件，把原有的路由拦截以及校验逻辑放在这个文件中

2）编写权限管理和自动登录逻辑

- 如果未登录过，自动登录（todo)

- 判断用户所在的路由和该路由所需要的权限与登录态的关系

- 如果要跳转的页面必须登录，若用户**没有登录就跳转到登录页面**

- 如果用户**登录**了，但是**权限不足**，那么跳转到无权限页面

```js
import { history } from "umi";
import store from "../redux/store";
import ACCESS_ENUM from "./accessEnum";
import router from "../../config/routes";
import checkAccess from "./checkAccess";
import { UserControllerService } from "generated";
function getRoutesArr() {
  const routeArr = router[0].routes;
  let arr = [routeArr];
  for (let i = 0; i < routeArr.length; i++) {
    if (routeArr[i].routes) {
      const routes = [routeArr[i].routes, ...arr].flatMap((item: any) => {
        return item;
      })
      return routes;
    }
  }
}
history.listen(async (location) => {
  // 在这里实现你的路由守卫逻辑 仅管理员可见，判断用户是否有管理员权限
  const routes = getRoutesArr();
  const loginUser = store.getState();
  //自动登录
  // if (
  //   loginUser.role === ACCESS_ENUM.NOT_LOGIN ||
  //   loginUser.username === "未登录"
  // ) {
  //   await UserControllerService.getLoginUserUsingGet()
  // }
  const needRoute = routes?.find((item) => {
    return item.path === location.location.pathname;
  });
  if (needRoute?.path === '/login' || needRoute?.path === '/register') {
    return
  }
  const needAccess =
    (needRoute.meta?.access as String) ?? ACCESS_ENUM.NOT_LOGIN;
  //要跳转的页面必须登录
  if (needAccess !== ACCESS_ENUM.NOT_LOGIN) {
    //如果没有登录，跳转到登录页面
    if (
      loginUser.role === ACCESS_ENUM.NOT_LOGIN ||
      loginUser.username === "未登录"
    ) {
      history.push(`/login?redirect=${needRoute.path}`);
    }
  }
  //如果已经登陆了，但是权限不足，那么跳转到无权限页面
  if (!checkAccess(loginUser, needAccess)) {
    history.push("/noAuth");
  }
  // 如果校验通过，直接返回
  return true;
});
```

### Markdown编辑器

### 代码编辑器

### 题目提交页面

请求时需要用户输入的值

```json
{
  "answer": "",
  "content": "",
  "judgeCase": [
    {
      "input": "",
      "output": ""
    }
  ],
  "judgeConfig": {
    "memoryLimit": 0,
    "stackLimit": 0,
    "timeLimit": 0
  },
  "tags": [],
  "title": ""
}
```

### 五、前端问题

1、安装ant pro脚手架出现'pro‘ 不是内部或外部命令，也不是可运行的程序 或批处理文件。

https://blog.csdn.net/weixin_48877626/article/details/135308016

2、函数式组件中子组件向父组件传递值和方法

 **使用回调函数**：父组件给子组件传递一个**函数，**子组件点击按钮时，调用这个函数，实现传值。

```jsx
//Parent.jsx
import React, { useState } from 'react'
import Child from '../components/Child'
export default function Parent() {
    const [count, setCount] = useState(0);
  return (
    <div>
        <div>计数值：{count}</div>
      <Child setCountChild={setCount}/>
    </div>
  )
}
//Child.jsx
import React from 'react'
export default function Child({ setCountChild }: any) {
    return <button onClick={() => setCountChild((count: any) => count + 1)}>点击+1</button>;
}
```

![image-20240213215716790](C:\Users\YE\AppData\Roaming\Typora\typora-user-images\image-20240213215716790.png)



#### 引入echarts图表库

安装相关库：

```powershell
npx npm install --save echarts
npx npm install --save echarts-for-react
```

使用：

```tsx	
import ReactEcharts from "echarts-for-react";
 //柱状图配置
  const barOption = {
    backgroundColor: "transparent",
    tooltip: {
      trigger: "axis",
      axisPointer: {
        type: "shadow",
      },
    },
    legend: {
      data: ["门禁进入", "门禁外出"],
      align: "left",
      top: 18,
      right: 20,
      textStyle: {
        color: "#c1c5cd",
      }
    },
    grid: {
      top: "24%",
      left: "3%",
      right: "3%",
      bottom: "3%",
      containLabel: true,
    },
    xAxis: [
      {
        type: "category",
        data: [
          "1号楼",
          "2号楼",
          "3号楼"
        ],
        axisLine: {
          show: true,
          lineStyle: {
            color: "#45647f",
            width: 1,
            type: "solid",
          },
        },
      {
        name: "门禁外出",
        type: "bar",
        data: [50, 70, 60, 61, 75, 87, 60, 62],
        barWidth: 8,
        itemStyle: {
          color: "#f84f55",
        },
      },
    ],
  };
<ReactEcharts
        option={barOption}
        style={{ width: "300px", height: "150px" }}
 />
```



### 六、后端问题

安装maven依赖出现的问题：

```powershell
Failed to execute goal org.apache.maven.plugins:maven-compiler-plugin:3.10.1:compile (default-compile) on project kunoj-backend: Fatal error compiling: 无
效的目标发行版: 14 -> [Help 1]
```

确保项目的jdk配置为1.8，修改项目中关于14版本的switch问题，写为老版本switch。

导入项目到IDEA，点击mvn install 加载配置，出现各种java文件报错，此时需要配置maven 权限
https://blog.csdn.net/studyday1/article/details/126892063?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522168438768816800215096326%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=168438768816800215096326&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-1-126892063-null-null.blog_rank_default&utm_term=%E9%85%8D%E7%BD%AE&spm=1018.2226.3001.4450





### 七、知识小点：

1、降低Node版本教程：安装NVM实现node版本切换

![image-20240126205415479](D:\typora_photo\image-20240126205415479.png)

https://blog.csdn.net/weixin_43961117/article/details/124961214

2、代理

正向代理：替客户端向服务器发送请求

反向代理：体服务器接收请求

怎么搞代理：

Nignx代理、Node.js服务器

3、ant Design pro项目瘦身

（1）移除国际化

```powershell
第一步：pro i18n-remove --locale=zh-CN --write
第二步：删除locales目录
第三步：删除Test目录
```

4、空值合并操作符 (`??`):
空值合并操作符是一个逻辑操作符，当左侧的操作数为 `null` 或 `undefined` 时，返回其右侧的操作数。它通常用于提供一个默认值。

在你的例子中，`loginUser?.userRole ?? ACCESS_ENUM.NOT_LOGIN` 表示如果 `loginUser?.userRole` 的结果是 `null` 或 `undefined`，则整个表达式的结果将是 `ACCESS_ENUM.NOT_LOGIN`。

5、form.item表单的getValueFromEvent方法，这个属性可以设置如何把输入的内容转换为表单项实际获取的值。例如：对输入的金额需要最多保留两位小数或者去除空格等等。

```js
  <Form.Item
         label="金额"
         name="amount"
         getValueFromEvent={(event: any) => {
         return event.target.value.replace(/^(\-)*(\d+)\.(\d\d).*$/, '$1$2.$3');
         }
>
```







在使用umi脚手架的React项目中实现路由守卫，可以通过以下步骤实现：

1. 首先，确保已经安装了`@umijs/plugin-router`插件。在umi项目的`package.json`文件中，应该可以看到这个插件：

json

复制

```json
"dependencies": {
  "@umijs/plugin-router": "^2.x"
}
```

1. 在`src`目录下创建一个名为`router.js`的文件，用于配置路由守卫。在这个文件中，你可以使用`umijs/plugin-router`提供的API来实现路由守卫。

javascript

复制

```javascript
// src/router.js
import { history } from '@umijs/plugin-router';

// 全局前置路由守卫
history.listen((location, action) => {
  // 在这里实现你的路由守卫逻辑
  // ...
  // 如果校验通过，直接返回
  return true;
});

// 全局后置路由守卫
history.listen((location, action) => {
  // 在这里实现你的路由守卫逻辑
  // ...
  // 如果校验通过，直接返回
  return true;
});
```

1. 在你的组件中，使用`withRouter`高阶组件来包裹需要跳转的组件。这样，你可以通过`this.props.history`来获取到路由跳转对象，从而实现跳转。

javascript

复制

```javascript
// src/pages/index/index.js
import React from 'react';
import { withRouter } from 'react-router-dom';

@withRouter
class Index extends React.Component {
  render() {
    const { history } = this.props;
    // ...
    // 在这里使用history来实现跳转
    history.push('/other');
    // ...
  }
}
```

通过以上步骤，你可以在umi脚手架的React项目中实现路由守卫。需要注意的是，umi脚手架默认使用`react-router-dom`进行路由配置，因此这里提供的示例代码仅供参考，具体实现方式可能需要根据你的项目配置进行调整。








在 Umi 4 中，可以通过以下几种方式实现路由权限管理：

### 1. 使用 `@umijs/plugin-access`

`@umijs/plugin-access` 是一个官方提供的插件，用于在 Umi 中实现路由权限管理。以下是基本的步骤：

1. 安装插件：

   bash

   复制

   ```bash
   npm install @umijs/plugin-access --save
   ```

   或

   bash

   复制

   ```bash
   yarn add @umijs/plugin-access
   ```

2. 配置插件：

   在 `config/config.js` 或 `config/config.ts` 中配置插件：

   javascript

   复制

   ```javascript
   import { defineConfig } from 'umi';
   
   export default defineConfig({
     plugins: [
       '@umijs/plugin-access',
       // ... 其他插件
     ],
     access: {
       // 权限规则配置
       rules: [
         { path: '/', name: '首页', access: 'canRead' },
         { path: '/about', name: '关于', access: 'canAbout' },
         // ... 更多规则
       ],
     },
   });
   ```

3. 在组件中使用：

   在需要控制权限的页面组件中，使用 `useAccess` 钩子来定义权限：

   javascript

   复制

   ```javascript
   import { useAccess } from 'umi';
   
   export default function Page() {
     const access = useAccess();
     if (!access.canRead) {
       return <div>你没有访问这个页面的权限</div>;
     }
     return <div>页面内容</div>;
   }
   ```

### 2. 自定义路由守卫

除了使用插件，还可以通过自定义路由守卫来实现权限管理：

1. 创建路由守卫：

   javascript

   复制

   ```javascript
   import { Navigate, useLocation } from 'umi';
   
   export function useAuthGuard() {
     const location = useLocation();
     const user = getUser(); // 假设有一个函数可以获取当前用户信息
   
     if (!user || !user.hasAccess(location.pathname)) {
       return <Navigate to="/login" state={{ from: location }} replace />;
     }
   }
   ```

2. 在路由配置中使用守卫：

   javascript

   复制

   ```javascript
   import { useAuthGuard } from './guards';
   
   export default [
     {
       path: '/',
       component: Layout,
       children: [
         { path: 'home', component: Home },
         { path: 'about', component: About },
         // ... 其他路由
       ],
     },
     {
       path: '*',
       component: Layout,
       wrappers: [useAuthGuard],
       children: [
         { path: 'admin', component: Admin },
         // ... 需要权限的路由
       ],
     },
   ];
   ```

### 3. 使用 `useEffect` 钩子

在页面组件加载时，通过 `useEffect` 钩子检查权限，如果无权限则重定向到登录页面：

javascript

复制

```javascript
import { useEffect } from 'react';
import { Navigate, useLocation, history } from 'umi';

export default function SecurePage() {
  const location = useLocation();

  useEffect(() => {
    const user = getUser();
    if (!user || !user.hasAccess(location.pathname)) {
      history.push('/login', { from: location });
    }
  }, []);

  return <div>Secure Page Content</div>;
}
```

以上是几种在 Umi 4 中实现路由权限管理的方法。你可以根据项目的具体需求选择合适的方式。





优化的todo:

（1）按需引入组件库  







## UmiJS

1、umiJS是什么？

Umi，中文发音为「乌米」，Umi 是蚂蚁集团的底层前端框架，**是可扩展的企业级前端应用框架**。Umi 以路由为基础，同时支持配置式路由和约定式路由，保证路由的功能完备，并以此进行功能扩展。然后配以生命周期完善的插件体系，覆盖从源码到构建产物的每个生命周期，支持各种功能扩展和业务需求。

**相比于React的官方脚手架create-react-app来说，create-react-app在使用数据状态管理或者数据交互，一些hook库或者配置路由时，我们需要安装一些第三方库或者插件进行配置，但是使用umi在项目初始化时就已经完成这些配置，帮我们内置了路由、构建、部署、测试等。**

![image-20240126212712854](D:\typora_photo\image-20240126212712854.png)



