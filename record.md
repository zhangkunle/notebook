# 伙伴匹配系统

## **一、**项目实现过程问题

### **1、vue3的路由实现**

Vue3 中不再使用 `new Router()` 创建 router ，而是调用 `createRouter` 方法：

```js
import { createRouter } from 'vue-router'

const router = createRouter({
  // ...
})
```

路由模式 `mode` 配置改为 `history` ，属性值调整为：

- `"history"` => `createWebHistory()`
- `"hash"` => `createWebHashHistory()`
- `"abstract"` => `createMemoryHistory()`

```js
import { createRouter, createWebHistory } from 'vue-router'
// createWebHashHistory 和 createMemoryHistory (SSR相关) 同理

createRouter({
  history: createWebHistory(),
  routes: []
})
```

### 2、tab栏切换

![image-20231113224011683](D:\typora_photo\image-20231113224011683.png)

### 3、路由vue-router

![image-20231114130718134](D:\typora_photo\image-20231114130718134.png)

### 4、ref取值的时候要加上value

### 5、数组的filter（item表示数组的每一项）

![image-20231114152630634](D:\typora_photo\image-20231114152630634.png)

### 6、利用vant组件库的layout解决tag标签的排列样式

若采用 <van-row gutter="10" >设置列间距时，由于不同标签的文字大小不同，所以会出现tag对齐问题

![image-20231114161321230](D:\typora_photo\image-20231114161321230.png)

若采用 <van-row style="padding:7px">通过自行设置的padding以及子标签设置margin调整间距

```vue
<van-row style="padding:7px">
  <van-col v-for="tag in activeIds">
     <van-tag closeable size="medium" type="primary" plain @close="close(tag)" style="margin:5px">
                {{ tag }}
     </van-tag>
   </van-col>
</van-row>
```

![image-20231114163109094](D:\typora_photo\image-20231114163109094.png)

### 7、搜索标签显示查询结果

首先把所有分类通过flatMap和map（返回一个数组）汇总为一个数组，在数组中通过filter查找

（1）对于中文字精确查询添加

（2）对于英文字母不区分大小写添加查询，刚开始是用x===searchText.value.toUpperCase()||x===searchText.value.toLowerCase()作为判定条件的，是指全大写或者全小写的，不符合情况

后来经过查找用x.toUpperCase()===searchText.value.toUpperCase()，将输入转化为全大写再进行判断

### 8、flatMap和map和flat的用法

### 9、路由传参的两种方式（动态路由）

（1）/user/:id （如果是文章网站的话一般用这个，搜索引擎才能区分不同文章，下面的搜索引擎会认为是同一个文章）

（2）通过params传参

### 10、发送axios请求传递一个数组给后端会出现

![image-20231115151133001](D:\typora_photo\image-20231115151133001.png)

导致后端不认识这个东西，返回400，此时借助一个库qs来解决https://blog.csdn.net/pckzzy123/article/details/132478873

qs解决参数传递中数组格式不合法问题，需要指定 axios 的序列化方式，我们可以用 `paramsSerializer` 参数指定序列化函数

```
npm install qs
import qs from 'qs'
// indices（默认）
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'indices' })
// 'a[0]=b&a[1]=c'
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'brackets' })
// 'a[]=b&a[]=c'
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'repeat' })
// 'a=b&a=c'
```

### 11、resopnse.data?.data其中的问号是指可选链操作符，**？.（可选链）**

**引用为空 (`null` 或者 `undefined`) 的情况下不会引起错误，该表达式短路返回值是 `undefined`**

### 12、axios请求传递的参数类型

- data----->body参数（也就是请求体）

  ![image-20231201164732653](D:\typora_photo\image-20231201164732653.png)

- params----->query参数（都是拼接在请求地址上）

  ![image-20231201164531184](D:\typora_photo\image-20231201164531184.png)

  ![image-20231201164658059](D:\typora_photo\image-20231201164658059.png)

### 13、Vant中的Toast请提示

​     vant4中语法改变了

![image-20231116150031857](D:\typora_photo\image-20231116150031857.png)

### 15、配置代理服务器

![image-20231116171928597](D:\typora_photo\image-20231116171928597.png)

### 16、设置 axios.defaults.withCredentials = true; 以便携带跨域请求时的 cookie 信息

withCredentials 是 XMLHttpRequest 对象的一个属性，用来指定是否携带跨域请求时的 cookie 信息。当设置为 true 时，表示允许携带 cookie，否则不允许。在 axios 中，可以通过 axios.defaults.withCredentials = true; 来全局设置 withCredentials 属性。

### 17、通过onMounted发送数据请求，获取数据，在模板上用数据对象的一个属性值，报错如下：

![img](D:\typora_photo\a6e4a6e27fe2488082daea176e31eb3e.png)

原因：通过onMounted函数挂载后添加的，我们进来的data 在创建后已经完成了初始化，所以第一次渲染时我们这个时候拿到的值是第一次渲染时data中还没被添加数据的空数据，所以上面显示的时候就找不到里面的值  所以我们需要在父标签中添加上一个v-if 进行一个判断 如果有的话在进行渲染 就能拿到数据了
原文链接：https://blog.csdn.net/weixin_73260088/article/details/129622384

解决方法：![img](D:\typora_photo\e60ae732c21d4b52842835f3cbb090cf.png)

### 16、对于利用axios发送请求，post方法，参数类型为body ，且为application/json格式，可以采用第二种方式来写，或者直接将每个参数ref一遍再传值到属性里面，而第一种方式，则需要

![image-20231119001138231](D:\typora_photo\image-20231119001138231.png)

![image-20231119001144439](D:\typora_photo\image-20231119001144439.png)

17、pub/sub消息发布与订阅实现组件间传值方法

18、todo:json作为响应式对象传值与普通对象的区别是什么？

19、修改ref嵌套对象中某个属性值，是不起作用的

修改只有一层的ref对象中某个属性值会起作用





## 二、项目部署上线

### 1、打包前端代码问题

#### （1）修改请求文件myAxios.ts生产环境配置，配置线上后端地址

![image-20231201152515487](D:\typora_photo\image-20231201152515487.png)

#### （2）使用npm run bulid 打包

#### （3）使用npm install -g serve工具做线上前端测试 ，进入dist目录， 命令为serve

![image-20231201152247269](D:\typora_photo\image-20231201152247269.png)

![image-20231129233330919](D:\typora_photo\image-20231129233330919.png)

#### （4）由于打包有些依赖包体积过于庞大，提示你进行配置分割；https://blog.csdn.net/qq_45284938/article/details/129707

![image-20231130000114590](D:\typora_photo\image-20231130000114590.png)

#### （5）修改websocket中的端口地址localhost为后端线上地址配置

![image-20231201152626265](D:\typora_photo\image-20231201152626265.png)

### 2、打包后端代码

#### （1）购买服务器，进入宝塔面板，安装mysql以及redis、tomcat、ngix，PHP、PHPMyadmin

#### （2）安装完毕后，开发服务器和面板的3306端口，点击数据库一栏，新建数据库，输入数据库名与密码

![image-20231201153518493](D:\typora_photo\image-20231201153518493.png)

#### （3）点击phpmyadmin通过面板访问，输入账号名root以及密码![image-20231201153610393](D:\typora_photo\image-20231201153610393.png)

![image-20231201153646780](D:\typora_photo\image-20231201153646780.png)

#### （4）接着打开navcat，输入服务器地址以及在面板中创建的数据库密码与用户名，点击链接成功即可。

![image-20231201153837687](D:\typora_photo\image-20231201153837687.png)

#### （5）在IDEA中创建新的数据库连接，如果能够连接上就可以使用其访问了。

![image-20231201153936325](D:\typora_photo\image-20231201153936325.png)

#### （6）开发服务器和面板的6379端口，点击软件商店，找到redis点击性能调整

![image-20231201154148317](D:\typora_photo\image-20231201154148317.png)

#### （7）点击数据库redis添加redis远程服务器

![image-20231201154230899](D:\typora_photo\image-20231201154230899.png)

#### （8）保存连接后打开IDEA，添加新的redis链接即可。

#### （9）添加application-prod.yml文件，修改数据库，redis以及domain配置

```yml
server:
  port: 8080
  servlet:
    context-path: /api
    session:
      cookie:
        domain: 43.139.60.235  #服务器地址
        http-only: false
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://43.139.60.235:3306/super?serverTimezone=Asia/Shanghai #数据库地址
    username: super #云服务器的数据库名称
    password: dj4xtnS7NsNNMwbZ #云服务器的数据库密码
  redis:
    host: 43.139.60.235  #服务器地址
    port: 6379
    database: 0
    password: my12345hct  #云服务上redis的密码
  jackson:
    time-zone: GMT+8
    date-format: java.text.SimpleDateFormat
  mail:
    host: host
    username: username
    password: password
  session:
    store-type: redis
    timeout : 86400
  servlet:
    multipart:
      max-file-size: 10MB
      max-request-size: 10MB
#spring boot部署服务器端微服务，server.address配置0.0.0.0
#需要在application.properties/yml配置server.address=0.0.0.0
#server.address=0.0.0.0
#否则当微服务的jar部署在机器上跑起来后，外面机器通过http连接访问不到。
  server:
    address: 0.0.0.0  #必要步骤，配置本地IPV4的8080端口
mybatis-plus:
  configuration:
    map-underscore-to-camel-case: on
  global-config:
    db-config:
      logic-delete-value: 1
      logic-not-delete-value: 0
      logic-delete-field: isDelete
      id-type: auto
```

#### （10）修改redisConfig.java文件，添加一栏密码

```java
package net.zjitc.config;
import org.redisson.Redisson;
import org.redisson.api.RedissonClient;
import org.redisson.config.Config;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
/**
 * RedisConfig
 *
 * @author OchiaMalu
 * @date 2023/07/28
 */
@Configuration
public class RedisConfig {
    @Value("${spring.redis.host}")
    private String host;

    @Value("${spring.redis.port}")
    private String port;
    @Value("${spring.redis.password}")
    private String password;
    /**
     * redisson客户
     *
     * @return {@link RedissonClient}
     */
    @Bean
    public RedissonClient redissonClient() {
        Config config = new Config();
        String address = String.format("redis://%s:%s",host,port);
      config.useSingleServer().setAddress(address).setDatabase(0).setPassword(password);
        return Redisson.create(config);
    }
}
```

#### （12）跨域请求配置（后端）方法

##### 【1】修改后端服务：添加跨域配置文件WebMvcConfig

```java
package net.zjitc.config;
import net.zjitc.common.JacksonObjectMapper;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.converter.HttpMessageConverter;
import org.springframework.http.converter.json.MappingJackson2HttpMessageConverter;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;
import java.text.SimpleDateFormat;
import java.util.List;
/**
 * web mvc配置
 *
 * @author OchiaMalu
 * @date 2023/07/28
 */
@Configuration
public class WebMvcConfig implements WebMvcConfigurer {
    /**
     * 扩展消息转换器
     *
     * @param converters 转换器
     */
    @Override
    public void extendMessageConverters(List<HttpMessageConverter<?>> converters) {
        MappingJackson2HttpMessageConverter converter = new MappingJackson2HttpMessageConverter();
        JacksonObjectMapper objectMapper = new JacksonObjectMapper();
        //重写日期格式
        SimpleDateFormat smt = new SimpleDateFormat("yyyy-MM-dd");
        objectMapper.setDateFormat(smt);
        converter.setObjectMapper(objectMapper);
        converters.add(0, converter);
    }

    /**
     * 添加歌珥映射
     *
     * @param registry 注册表
     */
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                //设置允许跨域请求的域名
                //当**Credentials为true时，**Origin不能为星号，需为具体的ip地址【如果接口不带cookie,ip无需设成具体ip】
                .allowedOrigins("http://match.ymxcode.cn", "http://127.0.0.1:5173")
                //是否允许证书 不再默认开启
                .allowCredentials(true)
                //设置允许的方法
                .allowedMethods("*")
                //跨域允许时间
                .maxAge(3600);
    }
}
//http://match.ymxcode.cn 服务器前端地址
```

##### 【2】修改后端服务：在所有controller文件中添加@CrossOrigin注解

![image-20231201155739011](D:\typora_photo\image-20231201155739011.png)

##### 【3】网关支持（让服务器告诉浏览器允许跨域）：修改ngix配置

在ngix配置文件中添加以下代码

```yml
 Location ^~ /api/{
    proxy_pass http://127.0.0.1:8080/api/;
    add_header 'Access-Control-Allow-Origin'$http_origin; 
    add_header 'Access-Control-Allow-Credentials''true';
    add_header Access-Control-Allow-Methods 'GET, POST, OPTIONS'; 
    add_header Access-Control-Allow-Headers '*'; 
 if ($request_method ='OPTIONS') {
    add_header 'Access-Control-Allow-Credentials' 'true'; 
    add_header 'Access-Control-Allow-Origin' $http_origin;
    add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
    add_header 'Access-Control-Allow-Headers' 'DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range'; 
    add_header 'Access-Control-Max-Age'1728000;
    add_header 'Content-Type’ 'text/plain; charset=utf-8';
    add_header 'Content-Length' 0; 
    return 204;
    }
  }
```

#### （13）通过maven工具打包为jar文件，首先关闭项目的单元测试（maven的闪电圆点），然后点击package打包

![image-20231201153057464](D:\typora_photo\image-20231201153057464.png)

#### （14）进入target目录，open in terminal，输入以下语句进行线上测试

![image-20231201155936811](D:\typora_photo\image-20231201155936811.png)

#### （15）测试无误后，进入腾讯云，在购买的域名中进行解析，解析两个域名应用于前后端

![image-20231201160054058](D:\typora_photo\image-20231201160054058.png)

#### （16）进入宝塔，点击新建PHP网站，添加站点，输入域名，创建站点，进入此站点根目录，上传dist文件夹文件到根目录。输入域名进行测试，**注意这里是使用http访问**

![image-20231201160319552](D:\typora_photo\image-20231201160319552.png)

![image-20231201160400155](D:\typora_photo\image-20231201160400155.png)

#### （17）修改站点配置文件，添加以下语句，保证其他路由下的文件可以访问到**（如/user/login[解决刚开始访问域名出现/user/login的404或者500问题]）**

https://blog.csdn.net/qq_39330397/article/details/131460227

![image-20231201161603401](D:\typora_photo\image-20231201161603401.png)

#### （18）将后端jar文件上传至新建文件夹/www/wwwroot/match-backend，进入网站，点击java项目，进行如下设置：

![image-20231201160648388](D:\typora_photo\image-20231201160648388.png)

#### （19）如果宝塔启动不成功可以使用原生启动方式，在腾讯云远程登录中输入项目执行命令，启动项目

```java
/usr/bin/java -jar -Xmx1024M -Xms256M  /www/wwwroot/match-backend/super-backend-2.0.1.RELEASE.jar --spring.profiles.active=prod
```

#### （20）输入后端地址：8080/api/user/search进行测试成功后，通过前端域名进行访问

#### （21）设置后端项目后台启动，输入以下语句

```java
//启动后台项目
nohup /usr/bin/java -jar -Xmx1024M -Xms256M  /www/wwwroot/match-backend/super-backend-2.0.1.RELEASE.jar --spring.profiles.active=prod &

//关闭后台项目
ps -aux | grep jar包名称   #如 ps -aux | grep newssystem
kill 进程ID号
```

## 三、聊天功能websocket实现

1、准备一个存放当前用户信息，聊天对象信息与队伍聊天信息的对象stats

2、当用户点击进入私聊tochat时传入用户名与用户ID/队伍名与队伍ID，以及各自的类型userType:1与teamType：2.,主要用来识别是属于队伍聊天还是个人私聊，以及3为大厅聊天，与前面定义的chatEnum相对应

3、在onMounted是，通过路由获取传入的信息传到stats对象上，然后通过chatEnum来分组if-else实现不同类型的聊天功能，发送不同的axios请求

4、私聊：传入toId   队伍：传入teamId   大厅：无需参数

5、创建createContent：用来将json数据 转为html聊天框信息，定义参数remoteUser（远程用户）, nowUser（当前用户）, text（聊天内容文本）, isAdmin（是否为管理员）, createTime（创建时间）分别通过模板字符串方法创建远程用户与当前用户的聊天气泡框，将html添加到stats中的content

6、通过三种不同的axios请求返回聊天数据，通过isMy字段判断消息是否为我的消息，来渲染以前的信息到页面上，若是，则表示由自己发送的信息，若否则为别人发送信息，对于队伍以及大厅聊天来说，只有fromuser没有touser，而私聊是一对一的则有touser。根据Ismy来创造先前已有的聊天记录信息，返回的数据如下所示：

![image-20231202173302293](D:\typora_photo\image-20231202173302293.png)

7、创建init(）方法连接websocket并接受服务器发送过来的数据，实时渲染页面信息。首先是判断浏览器是否支持websocket，若支持则创建websocket实例，则首先通过socket.close()清除之前的socket链接，再将socket置空，接着创建实例socket = new WebSocket(socketUrl);socketUrl为后端通信的路径，在 socket.onopen（建立连接时触发） 中调用心跳机制

```javascript
//使用setInterval定时发送心跳包。监听是否建立连接
const startHeartbeat = () => {
    heartbeatTimer = setInterval(() => {
        if (socket.readyState === WebSocket.OPEN) {
            socket.send("PING");
        }
    }, heartbeatInterval);
}
```

#####  webSocket.readyState

readyState属性返回实例对象的当前状态，共有四种。

> - CONNECTING：值为0，表示正在连接。
> - OPEN：值为1，表示连接成功，可以通信了。
> - CLOSING：值为2，表示连接正在关闭。
> - CLOSED：值为3，表示连接已经关闭，或者打开连接失败

8、通过onmessage接收服务器发送过来的消息，当发送一个消息时服务器接收消息并传给前端onmessage中的data,当前端接收数据时，如果含有users，就过滤当前用户信息，如果没有含有users说明是其他用户发送了信息。

9、当前用户发送一个新信息时，实现判断输入内容不能为空以及聊天用户不为自身等因素，然后判断浏览器是否支持websocket，如果支持，发送message字段给服务器（由服务器转发到别的用户，把客户端发送来的信息，广播给其它客户端），如下：

![image-20231202220112487](D:\typora_photo\image-20231202220112487.png)



10、接着通过createContent将信息插入到对话框中，通过nextTick()方法获取聊天框div最后一个子元素并在其身上加上scrollIntoView()方法.

注意：scrollIntoView()方法将调用它的元素滚动到浏览器窗口的可见区域。

- 根据其他元素的布局，元素可能无法完全滚动到顶部或底部。
- 页面（容器）可滚动时才有用！为容器添加overflow:auto属性

```javascript
 await nextTick(() => {
                const lastElement = chatRoom.value.lastElementChild
                if (lastElement) {
                    lastElement.scrollIntoView()
                }
            })
```

11、接着当有其他用户发送信息时，则利用各个聊天类型的特点来判断属于哪个类型的聊天方式，可以通过flag属性判断是否为某种类型，接着将此数据通过createContent将信息插入到对话框中，接着调用nextTick滚动元素，最后将flag=null

12、当服务器端关闭时，触发 socket.onclose ，首先会情况心跳机制，设置5s后重连；当发生错误时触发  socket.onerror

![image-20231202222650929](D:\typora_photo\image-20231202222650929.png)

13、vue中动态添加html元素并绑定点击事件onclick，需要在window上绑定该事件才能使用。

原因：vue代码，需要分为编译前，和编译后，用动态添加html标签的方法，实际上就是编译后添加进这个html语句，再生成这个控件，这时候再控件里写的onclick就是去找编译后叫这个名称的方法，而直接写function的话，就生成的是编译前的方法，生成html之后再去找这个方法，必然是找不到的，找到的只能是后面写在window.function的全局方法。

14、后端部署出现问题

![image-20240412132012395](D:/typora_photo/image-20240412132012395.png)

解决方法：

Spring Boot Redis 集成 Error creating bean with name 'enableRedisKeyspaceNotificationsInitializer

1、原因：redis集群环境没有开启Keyspace notifications

2、解决办法　 在HttpSessionConfig中添加一下代码：

```
@Configuration
public class HttpSessionConfig {
    @Bean
    public static ConfigureRedisAction configureRedisAction() {
        return ConfigureRedisAction.NO_OP;
    }
}
```

