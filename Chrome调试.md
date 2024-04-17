> 注意以下配置中有些命令不起效果，可能是因为需要在英文面板中使用，中文面板可以直接输入中文寻找对应的功能

# 基础介绍

## 打开Dev Tool

- 菜单>更多工具>开发者工具
- `F12`
- `Ctrl + Shift + L`

## 命令菜单

`Ctrl + Shift + P`

常用命令

- `light/dark theme`切换主题

- `screenshot`截屏

  > - 节点：选中节点截图
  >
  > - 完整尺寸：整个页面，包括滚动条下面的
  >
  > - 区域：框选截图
  >
  > - 屏幕截图：

- `dock`改变调试窗口位置

  > - `undock`分离成独立窗口
  > - `dock to button`
  > - `dock to left/right`

- `enable code folding`打开代码折叠

## 常用的面板

- Elements
- Console
- Source
- Network
- Application

# 元素(Element)

## CSS调试

### 检查元素

选中页面元素，右击“检查”，即可快速再html结构中定位此元素。

查看移动设备显示`Ctrl + Shift + M`

### 查询DOM树

`Ctrl + F`调出搜索框

查询方式：

- 文本查询

- CSS选择器

  例如：`section#section_two`

  表示id为section_tow的section标签元素

- Xpath

  例如：`//section/p`

  `//`表示全局查找，全局中查找section下的p节点

### Console

`inspect(element)`

其中element使用js中dom语句获取元素

例如：`inspect(document.getElementById(‘root’))`

## 编辑样式

### Styles面板

#### 添加样式

点击选中元素

![image-20220913124952227](Chrome调试.assets/image-20220913124952227.png)

样式右上角角标：

- 文件名：行数
- user agent stylesheet浏览器内置央视

样式左上角标识：

- Inherited from xxx继承样式
- Pseudo 伪类定义

#### 样式常驻

![image-20220913133046677](Chrome调试.assets/image-20220913133046677.png)

固定激活后，元素代码左边会出现一个橙色的小点标识

#### 编辑class样式影响范围

.cls中取消勾选，即可取消样式class影响范围

#### 复制样式

打开开发者工具，选中元素，右键

![image-20220913133619354](Chrome调试.assets/image-20220913133619354.png)

即可复制目标元素的样式

在需要粘贴的地方，直接`Ctrl + V`即可粘贴样式。

### 其他面板讲解

#### Computed

列出了所有的样式

![image-20220913134205087](Chrome调试.assets/image-20220913134205087.png)

#### Layout

列出了所有使用Grid布局和FlexBox布局的容器

网格布局中可以调整显示的内容label

每个容器旁边的彩色方框表示辅助线颜色（可以修改

> 使用了flex布局或者grid布局的元素在Element面板代码有标签表示，选中标签时会出现对应的辅助线。

> 在Styles面板中写了flex或grid布局处
>
> ![image-20220913135512994](Chrome调试.assets/image-20220913135512994.png)

#### Event Listeners

列出了页面中所有的绑定事件

Remove按钮可以去除掉对应的事件

#### *DOM Breakpoints

JS调试中使用：

​	在目标元素上右键，绑定中断条件（绑定后代码左边会出现蓝色圆点标识，表示打了断点），当发生了绑定的中断条件后，触发条件进入源代码Sources调试界面，自动定位到发生改变处代码。

![image-20220913143830842](Chrome调试.assets/image-20220913143830842.png)

#### Properties

展示所有节点的属性，使用**原型链**方式展示，由上到下继承

#### *Accessibility

帮助构建无障碍页面

# 控制台(Console)

`Ctrl + Shift + J`

- 直接执行语句

- `$_`返回上一条语句的执行结果

- `$0`当前选择的DOM节点(`$1,$2……`上一个、上上一个选择的)

- `console`输出

  - `log`打印变量

  - `error`错误

  - `warn`警告

  - `table`表格，数据格式为对象数组，点击字段名称可以排序

    ![image-20220913141539485](Chrome调试.assets/image-20220913141539485.png)

  - `clear`清空控制台

  - `group`(‘分组名称’)分组显示，结尾处需要是`groupEnd`(‘分组名称’)

  - `time`，也需要timeEnd结尾，中间插入执行代码，返回中间嵌入代码的执行时长

  - `assert`断言，如果断言为 false，则在信息到控制台输出错误信息，第一个参数为布尔表达式，第二个为信息。

  - `trace`显示当前执行的代码在堆栈中的调用路径。

- Log级别筛选

  ![image-20220913141748742](Chrome调试.assets/image-20220913141748742.png)

- 眼睛图标可以观测变量

  ![image-20220913141913582](Chrome调试.assets/image-20220913141913582.png)

# JavaScript调试

1. 在代码中插入`debugger`语句作为断点进行调试

2. 在Chrome开发者工具的源代码Sources面板中调试时，也可以直接在行号处点击打断点

![image-20220913143738797](Chrome调试.assets/image-20220913143738797.png)

3. 使用Element面板中的[DOM Breakpoints](####*DOM Breakpoints)

4. 在Sources面板中的*Event Listener Breakpoints*处添加监听事件触发断点调试

   ![image-20220913144618223](Chrome调试.assets/image-20220913144618223.png)

   > 当使用框架时，框架本身是不需要调试修改的：
   >
   > ​	需要在Call Stack（调用堆栈）中将框架文件忽略
   >
   > ![image-20220913144915810](Chrome调试.assets/image-20220913144915810.png)

# 网络(Network)

![image-20220913145325736](Chrome调试.assets/image-20220913145325736.png)

- Preserve Log 保留日志：页面跳转、刷新后，保留历史记录
- Throttling节流器：模拟用户网络状态，限制请求速度
- User Agent 用户代理：模拟用户不同请求头部，注意不是切换不同浏览器内核

![image-20220913193101723](Chrome调试.assets/image-20220913193101723.png)

# 应用(Application)

- localStorage：本地永久储存，直到人为删除
- sessionStorage：会话存储，会话结束、页面关闭时清除
- cookie：可以设置过期时间

## 存储常用API

- setItem
- getItem
- removeItem
- clear