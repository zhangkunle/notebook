#                      ECMAScript 6简介

小马哥：https://juejin.im/post/6844903470823145486

阮一峰：https://es6.ruanyifeng.com/#README

​        ECMAScript 6.0（以下简称 ES6）是 JavaScript 语言的下一代标准，已经在 2015 年 6 月正式发布了。它的目标，是使得 JavaScript 语言可以用来编写复杂的大型应用程序，成为企业级开发语言。

## 一、let 和 const 命令

### 1.let基本用法

#### （1）块级作用域

在es6中可以使用let声明变量，用法类似于var，let声明的变量，只在`let`命令所在的代码块内有效。

```javascript
{
let a = 10;
var b = 20;
}
console.log(a);      //a is not defined
console.log(b);      //20
```



#### （2）不存在变量提升

`       var`命令会发生`变量提升`现象，即变量可以在声明之前使用，值为`undefined`。这种现象多多少少是有些奇怪的，按照一般的逻辑，变量应该在声明语句之后才可以使用。

为了纠正这种现象，let命令改变了语法行为，它所声明的变量一定在声明后使用，否则报错。

```javascript
//var的情况
console.log(c);//输出undefined
 var c = 30;
//let的情况
console.log(c);// 报错ReferenceError
let c = 30;
```



#### （3）不允许重复声明

```javascript
let c = 10;
let c = 30;
console.log(c);    //报错
function func(arg) {
let arg;            // 报错
 }
```



#### （4）暂时性死区

了解的一个名词，说的就是`let`和`const`命令声明变量的特征。

在代码块内，使用`let`命令声明变量之前，该变量都是不可用的。这在语法上，称为`暂时性死区`(temporal dead zone，简称 TDZ)

##### 注意：

```javascript
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 10  此时由于变量提升，所以for前面就是var i变量提升，此时i就是循环后i++是10
```

```javascript
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 6  此时没有变量提升，买一个循环的i就是一个块级区域
```

### 2.为什么需要块级作用域？

##### 原因一：内层变量可能会覆盖外层变量

```javascript
function foo(a){
    console.log(a);
    if(1===2){
        var a = 'hello 小马哥';
    }
}
var a = 10;
foo(a);
```

##### 原因二：用来计数的循环遍历泄露为全局变量

```javascript
var arr = []
for(var i = 0; i < 10; i++){
    arr[i] = function(){
        return i;
    }
}
console.log(arr[5]());
```

变量`i`只用来控制循环，但是循环结束后，它并没有消失，用于变量提升，泄露成了全局变量。

**解决循环计数问题**

```javascript
//解决方式一：使用闭包
var arr = []
for(var i = 0; i < 10; i++){
    arr[i] = (function(n){
        
        return function(){
            return n;
        }
    })(i)
}
//解决方式二：使用let声明i
var arr = []
for(let i = 0; i < 10; i++){
    arr[i] = function () {
        return i;
    }
}
```

### 3.const基本用法-声明只读的常量

这意味着，`const`一旦声明变量，就必须立即初始化，不能留到以后赋值。对于`const`来说，只声明不赋值，就会报错。

```javascript
const a = 10;
a = 20;    //报错
const b;   //报错
```

#### 与`let`命令相同点

- 块级作用域
- 暂时性死区
- 不可重复声明

#### `let`和`const`使用建议

> 在默认情况下用const,而只有你在知道变量值需要被修改的情况下使用let

### 4.模板字符串

传统的 JavaScript 语言，输出模板通常是这样写的

```javascript
const oBox = document.querySelector('.box');
// 模板字符串
let id = 1,name = '小马哥';
let htmlTel = "<ul><li><p>id:" + id + "</p><p>name:" + name + "</p></li></ul>";
oBox.innerHTML = htmlTel;
```

上面的这种写法相当繁琐不方便,ES6引入了模板字符串解决这个问题

```javascript
let htmlTel = `<ul>
    <li>
    <p>id:${id}</p>
    <p>name:${name}</p>
    </li>
</ul>`;

```

### 5.强大的函数

##### (1)ES5写法

```javascript
function pick(obj) {
    let result = Object.create(null);
    for (let i = 1; i < arguments.length; i++) {
        result[arguments[i]] = obj[arguments[i]];
        //其中arguments为输入的数据，是伪数组
}
    return result;
}
let book = {
    title: 'es6',
    author: '小马哥',
    year: 2019
}
let bookData = pick(book, 'author', 'year');
console.log(bookData);
```

##### (2)剩余参数：由三个点...和一个紧跟着的具名参数指定...keys

```javascript
 function pick(obj, ...keys) {
     // ...keys解决了arguments 的问题
     let result = Object.create(null);
     for (let i = 1; i < keys.length; i++) {
         
         result[keys[i]] = obj[keys[i]];
      }
      return result;
}
let book = {
    title: 'es6',
    author: '小马哥',
    year: 2019
}
let bookData = pick(book, 'author', 'year');
console.log(bookData);//
function checkArgs(...args) {
    console.log(args); //['a', 'b', 'c']
    console.log(arguments);
    //Arguments(3) ['a', 'b', 'c', callee: (...), Symbol(Symbol.iterator): ƒ]
    //0: "a  1: "b"  2: "c"}
checkArgs('a', 'b', 'c ');
```

##### (3)   剩余运算符：把多个独立的合并到一个数组中。

#####        扩展运算法：将一个数组分割，并将各个项作为分离的参数传给函数。

```javascript
const maxnum=Math.max(20,30);
console.log(maxnum);  //30
//处理数组中的最大值 使用apply
const arr=[10,20,50,30,67,100]
console.log(Math.max.apply(null,arr)); //100
//es6 扩展运算法更方便
console.log(Math.max(...arr));//100
```

##### （4）es6箭头函数

使用=>来定义  function（）{}等于（）=>{ }，没有this指向

###### 例1

```javascript
let add = function (a, b) {
    return a + b;
}
console.log(add(10, 20)); //30
//等价于
let add1 = (a, b) => {
    return a + b;
}
console.log(add1(10, 20));//30
```

###### 例2

```javascript
let add2 = val => val;
console.log(add2(10)); //

let add3 = val => (val + 5);
console.log(add3(10));

let add4 = (val1, val2) => val1 + val2;
console.log(add4(10, 30)); //40
```

例3

```javascript
let fn = () => 'hello world' + 123;
console.log(fn());  //hello world123

let obj = id => {
            return {
                id: id,
                name: '小马哥'
            }
        }
console.log(obj(20));  //{id: 20, name: '小马哥'}
```

例4

```javascript
let fn1 = (function () {
    return function () {
    console.log('hello es6');
}
})();
fn1(); //hello es6
//等价于
let fn2 = (() => {
    return () => {
    console.log('hi es6');
}
})();
fn2(); //hi es6
```

###### 区分：立即执行函数

```javascript
//(function(){})() 或者 (function(){}())
(function (a) {
    console.log(a);
})(1); //第二个小括号相当于调用参数

(function (a, b) {
    console.log(a + b);
}(1, 3));
 //有多个立即执行函数用分号分开
//3.立即执行函数作用是独立创建了一个作用域，里面所有变量都是局部变量，不会有命名冲突的情况
```

###### 注意事项：

（1）箭头函数没有this指向，箭头函数内部this值只能通过查找作用域链来确定，一旦使用箭头函数，当前就不存在作用域链。

```javascript
let pageHandle = {
    id: 123,
    init: function () { //此时如果把function ()改为()=>时，this指向的就是window会报错
     document.addEventListener("click", (event) => {
         console.log(this);  //Object对象，即为整个pagehandle对象
         this.dosomething(event.type);
     }, false)
},
    //此时使用箭头函数，整个function的作用域链取消，此时this指向的就是pagehandle
   dosomething: function (type) {
        console.log(`事件类型:${type},当前id:${this.id}`);
   }
}
 pageHandle.init();//事件类型:click,当前id:123
```

（2）使用箭头函数，函数内部没有arguments，因为没有作用域链

```javascript
let getVal = (a, b) => {
    console.log(this);//Window {window: Window, self: Window, document: document …}
    console.log(arguments);//报错
    return a + b;
}
console.log(getVal(1, 3));
```

（3）箭头函数不能使用new关键字来实例化对象，function函数也是一个对象，但是箭头函数不是一个对象，它其实是一个语法糖。

```javascript
let Person = () => {}
console.log(Person);//() => {}
```

### 6.解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为**解构**。

解构赋值是对赋值运算符的一种扩展，它针对数组和对象来进行操作。

优点：代码书写上简洁易读。

#### （1）解构对象

```javascript
 let node = {
     type: 'iden',
     name: 'foo'
}
//es5写法
let type=node.type;
let name=node.name;
//es6写法
//完全解构----对象
let { type, name } = node;
console.log(type, name);
let obg = {
    a: {
         name: '张飒'
    },
    b: [],
    c: 'hello'
}
//如果变量名与属性名不一致，必须写成下面这样。
let obj = { first: 'hello', last: 'world' };
let { first: f, last: t } = obj;
f // 'hello'
t // 'world'
//不完全解构 可忽略
let { a } = obg;
 console.log(a);    //{name: '张飒'}
//剩余运算符
let { a, ...res } = obg;
console.log(res);//{b: Array(0), c: 'hello'}
//默认值
let {a,b=30}={a:20};
let [foo = true] = []; // foo的值是true
let [x = 1] = [undefined];   //x 的值是 1

function f() {
    console.log('aaa');
}
//因为x能取到值，所以函数f根本不会执行
let [x = f()] = [1];
console.log(x);  //1
```

#### （2）解构数组

```javascript
let arr1 = [1, 2, 3];
let [a, b, c] = arr1;
//完全解构
console.log(a, b, c);  // 1 2 3
//不完全解构
 let [a, b] = arr1;
 console.log(a, b);  // 1 2 
//可嵌套
let [g,[h],j]=[1,[2],3];
```

```javascript
let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []

```

### 7.对象的扩展

#### (1)对象属性写法（es6)

```javascript
 const name1='哈哈',age=10;
//ES5写法
 const person1={
     name1:name1,
     age:age,
     sayName:function(){
         console.log('jj');
     }
}
//es6写法
const person2={
    name1,
    age,
    sayName(){
        console.log('jj');
  }
}
person2.sayName();//jj
```

```javascript
//简洁写法
function fnn(x, y) {
      return { x, y };
}
console.log(fnn(10, 20));  //{x: 10, y: 20}
```

```javascript
//应用
let cart = {
    wheel: 4,
    set(newVal) {
        if (newVal < this.wheel) {
             throw new Error('轮子数太少了')
        }
        this.wheel = newVal;
        console.log();
 },
    get() {
        return this.wheel;
    }
}
 //cart.set(3)//Uncaught Error: 轮子数太少了
cart.set(7);
console.log(cart.get());  //7
```

```javascript
//对象属性组合一
const obj1 = {};
obj1.isShow = true;
const name2 = 'a';
obj1[name2 + 'bc'] = 123;
obj1['f' + 'bc'] = function () {
    console.log(this);
}
console.log(obj1);//{isShow: true, abc: 123, fbc: ƒ}
```

```javascript
//对象属性组合二
 const name3 = 'a';
const obj2 = {
    isShow: true,
    [name3 + 'bc']: 123,
    [name3 + 'f']() {
        console.log(this);
     }
}
 console.log(obj2);//{isShow: true, abc: 123, af: ƒ}
```

#### (2)对象的方法

ES5 比较两个值是否相等，只有两个运算符：相等运算符（`==`）和严格相等运算符（`===`）。它们都有缺点，前者会自动转换数据类型，后者的`NaN`不等于自身，以及`+0`等于`-0`。

①ES6 提出“Same-value equality”（同值相等）算法，用来解决这个问题。*`Object.is*`就是部署这个算法的新方法。

is() 等价于 ===   比较两个值是否严格相等，解决了三个等号的特殊性

```javascript
console.log(NaN === NaN);//false
console.log(Object.is(NaN, NaN));//true
console.log(+0 === -0);//true
```

②Object.assign()`方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象。

assign()  用于对象的合并  Object.assign(target,obj1,obj2...),`

```javascript
 //返回合并之后的新对象
let newobj = Object.assign({}, { a: 1 }, { b: 2 });
console.log(newobj);//{a: 1, b: 2}
let newobj = Object.assign({ j: 8 }, { a: 1 }, { b: 2 });
console.log(newobj);//{j: 8, a: 1, b: 2}
```

由于`undefined`和`null`无法转成对象，所以如果它们作为参数，就会报错。

```javascript
Object.assign(undefined) // 报错
Object.assign(null) // 报错
```

如果非对象参数出现在源对象的位置（即非首参数），那么处理规则有所不同。首先，这些参数都会转成对象，如果无法转成对象，就会跳过。这意味着，*如果`undefined`和`null`不在首参数，就不会报错。*

```javascript
let obj = {a: 1};
Object.assign(obj, undefined) === obj // true
Object.assign(obj, null) === obj // true
```

其他类型的值（即数值、字符串和布尔值）不在首参数，也不会报错。但是，除了字符串会以数组形式，拷贝入目标对象，其他值都不会产生效果。

```javascript
const v1 = 'abc';
const v2 = true;
const v3 = 10;

const obj = Object.assign({}, v1, v2, v3);
console.log(obj); // { "0": "a", "1": "b", "2": "c" }
```

上面代码中，`v1`、`v2`、`v3`分别是字符串、布尔值和数值，结果只有字符串合入目标对象（以字符数组的形式），数值和布尔值都会被忽略。这是因为只有字符串的包装对象，会产生可枚举属性。

### 注意点

**（1）浅拷贝**

`Object.assign()`方法实行的是浅拷贝，而不是深拷贝。也就是说，如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用。

```javascript
const obj1 = {a: {b: 1}};
const obj2 = Object.assign({}, obj1);

obj1.a.b = 2;
obj2.a.b // 2
```

上面代码中，源对象`obj1`的`a`属性的值是一个对象，`Object.assign()`拷贝得到的是这个对象的引用。这个对象的任何变化，都会反映到目标对象上面。

**（2）同名属性的替换**

对于这种嵌套的对象，一旦遇到同名属性，`Object.assign()`的处理方法是替换，而不是添加。

```javascript
const target = { a: { b: 'c', d: 'e' } }
const source = { a: { b: 'hello' } }
Object.assign(target, source)
// { a: { b: 'hello' } }
```

上面代码中，`target`对象的`a`属性被`source`对象的`a`属性整个替换掉了，而不会得到`{ a: { b: 'hello', d: 'e' } }`的结果。这通常不是开发者想要的，需要特别小心。

一些函数库提供`Object.assign()`的定制版本（比如 Lodash 的`_.defaultsDeep()`方法），可以得到深拷贝的合并。

**（3）数组的处理**

`Object.assign()`可以用来处理数组，但是会把数组视为对象。

```javascript
Object.assign([1, 2, 3], [4, 5])
// [4, 5, 3]
```

上面代码中，`Object.assign()`把数组视为属性名为 0、1、2 的对象，因此源数组的 0 号属性`4`覆盖了目标数组的 0 号属性`1`。

**（4）取值函数的处理**

`Object.assign()`只能进行值的复制，如果要复制的值是一个取值函数，那么将求值后再复制。

```javascript
const source = {
  get foo() { return 1 }
};
const target = {};

Object.assign(target, source)
// { foo: 1 }
```

上面代码中，`source`对象的`foo`属性是一个取值函数，`Object.assign()`不会复制这个取值函数，只会拿到值以后，将这个值复制过去。

### 8.Symbol

ES6 引入了一种新的原始数据类型`Symbol`，表示独一无二的值。它属于 JavaScript 语言的原生数据类型之一，其他数据类型是：`undefined`、`null`、布尔值（Boolean）、字符串（String）、数值（Number）、大整数（BigInt）、对象（Object）。

最大用途：定义对象的私有变量

```javascript
const fk = Symbol('name');
const f1 = Symbol('name');
console.log(fk === f1);//false
const s1 = Symbol('s1');
console.log(s1);//Symbol(s1)
let obj3 = {};
obj3[s1] = '小马';
//如果用symbol定义对象 
console.log(obj3);//{Symbol(s1): '小马'}
let obj4 = {
    [s1]: '小马哥'
};
 console.log(obj4[s1]);//小马哥

 for (let key in obj4) {
      console.log(key);
}//无输出，因为由symbol定义的变量是无法遍历
console.log(Object.keys(obj4));//[]
//获取Symbol声明的属性名（作为对象的key)
let s = Object.getOwnPropertySymbols(obj4);
console.log(s);//[Symbol(s1)]
console.log(s[0]);//Symbol(s1)
let m = Reflect.ownKeys(obj4);
console.log(m);//[Symbol(s1)]
```

常量使用 Symbol 值最大的好处，就是其他任何值都不可能有相同的值了

​        Symbol 值作为属性名，遍历对象的时候，该属性不会出现在`for...in`、`for...of`循环中，也不会被`Object.keys()`、`Object.getOwnPropertyNames()`、`JSON.stringify()`返回。

​         但是，它也不是私有属性，有一个`Object.getOwnPropertySymbols()`方法，可以获取指定对象的所有 Symbol 属性名。该方法返回一个数组，成员是当前对象的所有用作属性名的 Symbol 值。

### 9.Set数据集合

ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

`Set`本身是一个构造函数，用来生成 Set 数据结构。

```javascript
let set = new Set();
console.log(set);//Set(0) {size: 0}
//添加元素
set.add(2);
set.add('2');
set.add(['hello', 2, 3]);
//删除元素
set.delete(2);
console.log(set);//set(2) {'2', Array(3)}
//集合校验:某个值是否在集合中
console.log(set.has('2'));//true
console.log(set.size);//2
//foreach方法不提倡，因为set的键值是相同的
set.forEach((val, key) => {
    console.log(val);// 2 (3) ['hello', 2, 3]
    console.log(key);//2 (3) ['hello', 2, 3]
})
//set集合的prototype可以查看对应的方法
```

![image-20230814212202145](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230814212202145.png)

```javascript
  //set中对象的引用无法被释放
let set3 = new Set(), obj5 = {};
set3.add(obj5);
  //释放当前的资源
obj5 = null;
console.log(set3);//Set(1) {{…}}
  //set中对象的引用无法被释放


//WeakSet的方法比Set少
//1.不能传入非对象类型的参数
//2.不可迭代
//3.没有forEach()
//4.没有size属性
let set4 = new WeakSet(), obj6 = {};
set4.add(obj6);
  //释放当前的资源
obj5 = null;
 console.log(set4);//WeakSet {{…}}
```

### 9.Map类型

​        ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。

map类型是键值对的有序列表，键和值是任意类型。

```javascript
let map = new Map();
map.set('name', '张飒');
map.set('age', 20);
console.log(map);//Map(2) {'name' => '张飒', 'age' => 20}
console.log(map.get('name'));//张飒
console.log(map.has('name'));//true
map.delete('name');
map.clear();
console.log(map);//Map(0) {size: 0}
map.set(['a', [1, 2, 3]], 'hello');
console.log(map);//Map(1) {Array(2) => 'hello'}
```

作为构造函数，Map 也可以接受一个数组作为参数。该数组的成员是一个个表示键值对的数组。

```javascript
const set = new Set([
    ['foo', 1],
    ['bar', 2]
]);
const m1 = new Map(set);
console.log(m1);       //Map(2) {'foo' => 1, 'bar' => 2}
m1.get('foo')          // 1
 
const m2 = new Map([['baz', 3]]);
console.log(m2);        //Map(1) {'baz' => 3}
const m3 = new Map(m2);
m3.get('baz')           // 3
```

![image-20230815100622716](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230815100622716.png)

### 10.数组的扩展

#### （1）Array.from()

`Array.from()`方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）。

```javascript
//es5写法
function add() {
     let arr = [].slice.call(arguments);//es5 将arguments伪数组转为数组
     console.log(arr);
}
add(1, 2, 3);//(3) [1, 2, 3]
// es6写法
function add() {
    let arr = Array.from(arguments);
    console.log(arr);
}
add(1, 2, 3);//Array(3)
//扩展运算符写法
function add() {
    console.log([...arguments]);//(3) [1, 2, 3]
}
add(1, 2, 3);

```

`Array.from()`还可以接受一个函数作为第二个参数，作用类似于数组的`map()`方法，用来对每个元素进行处理，将处理后的值放入返回的数组

```html
<ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
```

```javascript
//from()用来接受第二个参数，用来对每个元素进行处理
var lis = document.querySelectorAll('li');
var liContent = Array.from(lis, ele => ele.textContent);
console.log(liContent);//(4) ['1', '2', '3', '4']
```

#### （2）Array.of()

`Array.of()`方法用于将一组值（任意数据类型），转换为数组。

```javascript
Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]
Array.of(3).length // 1
console.log(Array.of(3, 11, [1, 2, 3], { id: 4 }));//(4) [3, 11, Array(3), {…}]
```

这个方法的主要目的，是弥补数组构造函数`Array()`的不足。因为参数个数的不同，会导致`Array()`的行为有差异。

`Array.of()`方法可以用下面的代码模拟实现。

```javascript
function ArrayOf(){
  return [].slice.call(arguments);
}
```

#### （3）实例方法：copyWithin()

数组实例的`copyWithin()`方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。

```javascript
Array.prototype.copyWithin(target, start = 0, end = this.length)
```

它接受三个参数。

- target（必需）：从该位置开始替换数据。如果为负值，表示倒数。
- start（可选）：从该位置开始读取数据，默认为 0。如果为负值，表示从末尾开始计算。
- end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示从末尾开始计算。

这三个参数都应该是数值，如果不是，会自动转为数值。

```javascript
//从三往后的所有数值替换从0位置开始往后的三个数值
[1, 2, 3, 4, 5].copyWithin(0, 3)
// [4, 5, 3, 4, 5]
```

上面代码表示将从 3 号位直到数组结束的成员（4 和 5），复制到从 0 号位开始的位置，结果覆盖了原来的 1 和 2。

#### （4）实例方法：find()，findIndex()，findLast()，findLastIndex() 

数组实例的`find()`方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为`true`的成员，然后返回该成员。如果没有符合条件的成员，则返回`undefined`。

```javascript
//找出数组中第一个小于 0 的成员。
[1, 4, -5, 10].find((n) => n < 0)
// -5
```

```javascript
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10
```

上面代码中，`find()`方法的回调函数可以接受三个参数，依次为当前的值、当前的位置和原数组。

数组实例的`findIndex()`方法的用法是返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回`-1`。

```javascript
let num1 = [1, 2, -10, 3, 4, 5].findIndex(x => x < 0);
console.log(num1);//2
```

```javascript
[1, 5, 10, 15].findIndex(function(value, index, arr) {
  return value > 9;
}) // 2
```

[ES2022](https://github.com/tc39/proposal-array-find-from-last) 新增了两个方法`findLast()`和`findLastIndex()`，从数组的最后一个成员开始，依次向前检查，其他都保持不变。

#### (5)实例方法：entries()，keys() 和 values() 

​        ES6 提供三个新的方法——`entries()`，`keys()`和`values()`——用于遍历数组。它们都返回一个遍历器对象，可以用`for...of`循环进行遍历。

​        唯一的区别是`keys()`是对键名的遍历、`values()`是对键值的遍历，`entries()`是对键值对的遍历。

```javascript
  for (let index of ['a', 'b'].keys()) {
      console.log(index);//0 1 索引
  }
  for (let ele of ['a', 'b'].values()) {
      console.log(ele);//a b 值
  }
  for (let [index, ele] of ['a', 'b'].entries()) {
      console.log(index, ele);//0 'a'  1 'b'
 }
```

如果不使用`for...of`循环，可以手动调用遍历器对象的`next`方法，进行遍历。

```javascript
let letter = ['a', 'b', 'c'];
let entries = letter.entries();
console.log(entries.next().value); // [0, 'a']
console.log(entries.next().value); // [1, 'b']
console.log(entries.next().value); // [2, 'c']
```

#### (6)fill()方法

`fill`方法使用给定值，填充一个数组。

```javascript
['a', 'b', 'c'].fill(7)
// [7, 7, 7]

new Array(3).fill(7)
// [7, 7, 7]
```

上面代码表明，`fill`方法用于空数组的初始化非常方便。数组中已有的元素，会被全部抹去。

`fill`方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。

```javascript
['a', 'b', 'c'].fill(7, 1, 2)
// ['a', 7, 'c']
```

上面代码表示，`fill`方法从 1 号位开始，向原数组填充 7，到 2 号位之前结束。

#### (7)实例方法：includes() [§](https://es6.ruanyifeng.com/#docs/array#实例方法：includes) 

`Array.prototype.includes`方法返回一个布尔值，表示某个数组是否包含给定的值。

```javascript
console.log([1, 2, 34, 6, 7].includes(34));//true
console.log([1, 2, 3].indexOf(2));//1
console.log([1, 2, 3].indexOf('2'));//-1，表示不包含
```

该方法的第二个参数表示搜索的起始位置，默认为`0`。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为`-4`，但数组长度为`3`），则会重置为从`0`开始。

```javascript
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
```

### 11.Iterator（遍历器）

遍历器（Iterator）就是这样一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。

两个核心：1.迭代器是一个接口，能快捷地访问数据，通过Symbol.iterator来创建迭代器，通过迭代器的next()获取迭代之后的结果。

2.迭代器是用于遍历数据结构的指针（数据库的游标）

```javascript
let arr = ['a', 'b', 'c'];
let iter = arr[Symbol.iterator]();//Array Iterator {}

iter.next() // { value: 'a', done: false }
iter.next() // { value: 'b', done: false }
iter.next() // { value: 'c', done: false } done为false表示遍历继续
iter.next() // { value: undefined, done: true } done为true表示遍历完成
```

上面代码中，变量`arr`是一个数组，原生就具有遍历器接口，部署在`arr`的`Symbol.iterator`属性上面。所以，调用这个属性，就得到遍历器对象。

### 12.Generator 生成器函数

Generator 函数是一个状态机，封装了多个内部状态。

执行 Generator 函数会返回一个遍历器对象，也就是说，Generator 函数除了状态机，还是一个遍历器对象生成函数。返回的遍历器对象，可以依次遍历 Generator 函数内部的每一个状态。

形式上，Generator 函数是一个普通函数，但有区别，有两个特征。一是，`function`关键字与函数名之间有一个星号；二是，函数体内部使用`yield`表达式，定义不同的内部状态。可以通过yield将函数挂起，为改变执行流提供可能，为异步编程提供方案。

```javascript
function* func() {
    console.log('one');
    yield 2;
    console.log('two');
    yield 3;
    console.log('end');
}
let o = func();
console.log(o.next());//返回一个遍历器对象，one {value: 2, done: false}
console.log(o.next());//two  {value: 3, done: false}
console.log(o.next());//end {value: undefined, done: true}
```

总结一下，调用 Generator 函数，返回一个遍历器对象，代表 Generator 函数的内部指针。以后，每次调用遍历器对象的`next`方法，就会返回一个有着`value`和`done`两个属性的对象。`value`属性表示当前的内部状态的值，是`yield`表达式后面那个表达式的值；`done`属性是一个布尔值，表示是否遍历结束。

**<u>遍历器对象的`next`方法的运行逻辑如下：</u>**

（1）遇到`yield`表达式，就暂停执行后面的操作，并将紧跟在`yield`后面的那个表达式的值，作为返回的对象的`value`属性值。

（2）下一次调用`next`方法时，再继续往下执行，直到遇到下一个`yield`表达式。

（3）如果没有再遇到新的`yield`表达式，就一直运行到函数结束，直到`return`语句为止，并将`return`语句后面的表达式的值，作为返回的对象的`value`属性值。

（4）如果该函数没有`return`语句，则返回的对象的`value`属性值为`undefined`。

```javascript
function* add() {
     console.log('start');
     //x表示yield的返回值，是next()方法调用恢复当前yield()执行传入的实参
     let x = yield '2';
     console.log('one:' + x);
     let y = yield '3';
     console.log('two:' + y);
     return x + y;
}
 const fn = add();
console.log(fn.next());//start  {value: '2', done: false}
console.log(fn.next(20));//one:20  {value: '3', done: false}
console.log(fn.next(30));//two:30   {value: 50, done: true}
console.log(fn.return(100));//{value: 100, done: true}
```

```javascript
function * foo(x, y) { ··· }
function *foo(x, y) { ··· }
function* foo(x, y) { ··· }
function*foo(x, y) { ··· }
```

ES6 没有规定，`function`关键字与函数名之间的星号，写在哪个位置。这导致上面的写法都能通过。

总结：Generator 函数是分段执行的，yield语句时暂停执行，而next()语句时恢复执行

使用场景：为不具备Interator接口的对象提供遍历操作

```javascript
function* objectEntries(obj) {
    const propKeys = Object.keys(obj);
    for (const propKey of propKeys) {
        yield [propKey, obj[propKey]]
 }
}
const obj = {
    name: '小马',
    age: 18
}
//console.log(obj[Symbol.iterator]);
obj[Symbol.iterator] = objectEntries;
//console.log(obj);
 for (let [key, value] of objectEntries(obj)) {
      //console.log(`${key}:${value} `);//name:小马 age:18 
     console.log(key + ":" + value);//name:小马 age:18
}
```

### 13.Generator 生成器函数异步应用

#### （1）异步

所谓"异步"，简单说就是一个任务不是连续完成的，可以理解成该任务被人为分成两段，先执行第一段，然后转而执行其他任务，等做好了准备，再回过头执行第二段。

相应地，连续的执行就叫做同步。由于是连续执行，不能插入其他任务，所以操作系统从硬盘读取文件的这段时间，程序只能干等着。

```javascript
function* load() {
    loadUI();
    yield showData();
    hideUI();
}
let itload = load();
console.log(itload.next());
function loadUI() {
    console.log('加载loading...页面');
}
function showData() {
    setTimeout(() => {
        console.log('数据加载完成');
        itload.next();
}, 1000);
}
function hideUI() {
    console.log('隐藏loading..页面');
}
 //结果 ：加载loading...页面   数据加载完成    隐藏loading..页面
```

因为多个异步操作形成了强耦合，只要有一个操作需要修改，它的上层回调函数和下层回调函数，可能都要跟着修改。这种情况就称为"回调函数地狱"（callback hell）。

```javascript
 //解决回调地狱问题
function* main() {
     let res = yield request('https://api.github.com/users/github');
     console.log(res);
}
console.log('数据请求完成，可以继续操作');
const ite = mian();
ite.next();
function request(url) {
    alert(url);
    $.ajax({
         url,
         method: 'get',
         success(res) {
             ite.next(res);
         }
    })
}

```

```javascript
function* gen(x) {
  var y = yield x + 2;
  return y;
}

var g = gen(1);
g.next() // { value: 3, done: false }
g.next() // { value: undefined, done: true }
```

上面代码中，调用 Generator 函数，会返回一个内部指针（即遍历器）`g`。这是 Generator 函数不同于普通函数的另一个地方，即执行它不会返回结果，返回的是指针对象。调用指针`g`的`next`方法，会移动内部指针（即执行异步任务的第一段），指向第一个遇到的`yield`语句，上例是执行到`x + 2`为止。

​       `next`返回值的 value 属性，是 Generator 函数向外输出数据；`next`方法还可以接受参数，向 Generator 函数体内输入数据。

### 14.promise对象

#### （1）promise的含义

所谓`Promise`，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，**各种异步操作都可以用同样的方法进行处理**。

`Promise`对象有以下两个特点。

（1）对象的状态不受外界影响。`Promise`对象代表一个**异步操作**，有三种状态：`pending`（进行中）、`resolved`（已成功）和`rejected`（已失败）。

（2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。

ES6 规定，`Promise`对象是一个构造函数，用来生成`Promise`实例。

下面代码创造了一个`Promise`实例。

```javascript
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
console.log(promise);
```

![image-20230816141702412](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230816141702412.png)

`Promise`构造函数接受一个函数作为参数，该函数的两个参数分别是`resolve`和`reject`。

`     resolve`函数的作用是，将`Promise`对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去。

`  reject`函数的作用是，将`Promise`对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

`Promise`实例生成以后，可以用`then`方法分别指定`resolved`状态和`rejected`状态的回调函数。

```javascript
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```

#### （2）then方法

`then`方法可以接受两个回调函数作为参数。第一个回调函数是**`Promise`对象的状态变为`resolved`时调用**，第二个回调函数是**`Promise`对象的状态变为`rejected`时调用**。这两个函数都是**可选**的，不一定要提供。它们都接受`Promise`对象传出的值作为参数。

**then()返回的是return的结果。**

then()方法返回一个新的promise实例，可以采用链式编程。

```javascript
getJSON("/posts.json").then(function(json) {
  return json.post;
}).then(function(post) {
  // ...
});
```

上面的代码使用`then`方法，依次指定了两个回调函数。第一个回调函数完成以后，会将返回结果作为参数，传入第二个回调函数。

采用链式的`then`，可以指定一组按照次序调用的回调函数。这时，前一个回调函数，有可能返回的还是一个`Promise`对象（即有异步操作），这时后一个回调函数，**就会等待该`Promise`对象的状态发生变化，才会被调用**。

```javascript
getJSON("/post/1.json").then(function(post) {
  return getJSON(post.commentURL);
}).then(function (comments) {
  console.log("resolved: ", comments);
}, function (err){
  console.log("rejected: ", err);
});
```

上面代码中，第一个`then`方法指定的回调函数，返回的是另一个`Promise`对象。这时，第二个`then`方法指定的回调函数，就会等待这个新的`Promise`对象状态发生变化。如果变为`resolved`，就调用第一个回调函数，如果状态变为`rejected`，就调用第二个回调函数。

```
catch(err=>{})`方法等价于`then(null,err=>{})
```

用于指定发生错误时的回调函数。

```javascript
getJSON('/posts.json').then(function(posts) {
  // ...
}).catch(function(error) {
  // 处理 getJSON 和 前一个回调函数运行时发生的错误
  console.log('发生错误！', error);
});
//等价于
getJSON('/posts.json').then(function(posts) {
  // ...
}).then(null,function(error) {
  // 处理 getJSON 和 前一个回调函数运行时发生的错误
  console.log('发生错误！', error);
});
```

***示例：***

```javascript
const promise = new Promise(function (resolve, reject) {
    // ... some code
    let res = {
        code: 201,
        data: {
            name: '香'
        },
        error: '失败'
     };
     setTimeout(() => { //通过设置定时器模拟异步操作，隔1s后操作
         if (res.code == 200) {
             resolve(res.data);
          } else {
              reject(res.error);
      }, 1000)
});
console.log(promise);
 promise.then((val) => {//其中val的值是接收resolved方法的值
     console.log(val);//{name: '香'}
 }, (err) => {
     console.log(err);//失败
});

//对上面的操作进行简单的封装
function timeout(ms) {
     return new Promise((resolve, reject) => {
         setTimeout(() => {
            resolve('hello success');
         }, ms);
      })
}
timeout(2000).then((val) => {
    console.log(val);
})
```

```javascript
//自行封装的getJSON方法
const getJOSN = function (url) {
    return new Promise((resolve, reject) => {
        const xhr = new XMLHttpRequest();
        xhr.open('GET', url);
        xhr.onreadystatechange = handler;
        xhr.responseType = 'json';
        xhr.setRequestHeader('Accept', 'application/json');
        xhr.send();//发送
        function handler() {
            console.log(this);
            if (this.readyState === 4) {
                if (this.status === 200) {
                    resolve(this.response);
                } else {
                    reject(new Error(this.statusText));
                }
           }
         }
  })
}
getJOSN('https://api.github.com/users/github').then((data) => {
    console.log(data);
    //{login: 'github', id: 9919, node_id: 'MDEyOk9yZ2FuaXphdGlvbjk5MTk=', avatar_url:    'https://avatars.githubusercontent.com/u/9919?v=4', gravatar_id: '', …}
}, (error) => {
    console.log(error);
})

//then方法的链式调用
getJSON('https://free-api.heweather.net/s6/weather/now?location=beijing&key=4693ff5ea653469f8bb0c29638035976')
    .then((res)=>{
    return res.HeWeather6;
}).then((HeWeather6)=>{
    console.log(HeWeather6);
})
```

#### then方法的规则

- `then`方法下一次的输入需要上一次的输出
- 如果一个promise执行完后 返回的还是一个promise，会把这个promise 的执行结果，传递给下一次`then`中
- 如果`then`中返回的不是Promise对象而是一个普通值，则会将这个结果作为下次then的成功的结果
- 如果当前`then`中失败了 会走下一个`then`的失败
- 如果返回的是undefined 不管当前是成功还是失败 都会走下一次的成功
- catch是错误没有处理的情况下才会走
- `then`中不写方法则值会穿透，传入下一个`then`中

#### （3）resolve()方法

```javascript
let p = Promise.resolve('foo');
//等价于
let p=new Promise(resolve=>resolve('foo'));
p.then((data) => {
    console.log(data);//foo
})
```

#### (4)Promise.all()方法

`Promise.all()`方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。

应用：一些游戏类的素材比较多，等待图片、flash、静态资源文件都加载完成才进行页面初始化

```javascript
const p = Promise.all([p1, p2, p3]);
```

上面代码中，`Promise.all()`方法接受一个数组作为参数，`p1`、`p2`、`p3`都是 Promise 实例。

`p`的状态由`p1`、`p2`、`p3`决定，分成两种情况。

（1）只有`p1`、`p2`、`p3`的状态都变成`resolved`，`p`的状态才会变成`resolved`，此时`p1`、`p2`、`p3`的返回值组成一个数组，传递给`p`的回调函数。

（2）只要`p1`、`p2`、`p3`之中有一个被`rejected`，`p`的状态就变成`rejected`，此时第一个被`reject`的实例的返回值，会传递给`p`的回调函数。

如果作为参数的 Promise 实例，自己定义了`catch`方法，那么它一旦被`rejected`，并不会触发`Promise.all()`的`catch`方法。

```javascript
const p1 = new Promise((resolve, reject) => {
  resolve('hello');
})
.then(result => result)
.catch(e => e);

const p2 = new Promise((resolve, reject) => {
  throw new Error('报错了');
})
.then(result => result)
.catch(e => e);

Promise.all([p1, p2])
.then(result => console.log(result))
.catch(e => console.log(e));
// ["hello", Error: 报错了]
```

如果`p2`没有自己的`catch`方法，就会调用`Promise.all()`的`catch`方法。

#### （5）race()方法

`Promise.race()`方法同样是将多个 Promise 实例，包装成一个新的 Promise 实例。

应用：某个异步请求设置超时时间，并且在超时后执行相应操作。

有些时候，多个异步任务是为了容错。比如，同时向两个URL读取用户的个人信息，只需要获得先返回的结果即可。这种情况下，用Promise.race()实现。

```javascript
const p = Promise.race([p1, p2, p3]);
```

```javascript
let meInfoPro1 = new Promise( (resolve, reject)=> {    setTimeout(resolve, 500, 'P1'); }); 
let meInfoPro2 = new Promise( (resolve, reject)=> {    setTimeout(resolve, 600, 'P2'); }); Promise.race([meInfoPro1,meInfoPro2]).then((result)
     => {  console.log(result); // P1 });
```

上面代码中，只要`p1`、`p2`、`p3`之中有一个实例率先改变状态，`p`的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给`p`的回调函数。

```javascript
function requestImg(imgSrc) {
    return new Promise((resolve, reject) => {
        const img = new Image();
        img.onload = function () {
            resolve(img);
        }
        img.src = imgSrc;
    })
}
function Timeout() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            reject(new Error('图片请求超时'));
        }, 3000);
    })
}      Promise.race([requestImg('https://img1.baidu.com/it/u=3539595421,754041626&fm=253&fmt=auto&app=138&f=JPEG?w=889&h=500'), Timeout()]).then(res => {
            console.log(res);
//<img src="https://img1.baidu.com/it/u=3539595421,754041626&amp;fmt=auto&amp;app=138&
//amp;f=JPEG?w=889&amp;h=500">
            document.body.appendChild(res);
            //等价于
            // var div = document.querySelector('div');
            // var img = document.createElement('img');
            // div.appendChild(img);
            // img.src = res.src;
        }).catch(err => {
            console.log(err);
        })
//当通过后台Networks设置网络为slow 3G时，返回结果为请求超时
```

**总结：**

**Promise.all接受一个promise对象的数组，待全部完成之后，统一执行success**;

**Promise.race接受一个包含多个promise对象的数组，只要有一个完成，就执行success**

#### （6)Promise.prototype.finally()

`finally()`方法用于指定不管 Promise 对象最后状态如何，都会执行的操作。该方法是 ES2018 引入标准的。

```javascript
promise
.then(result => {···})
.catch(error => {···})
.finally(() => {···});
```

上面代码中，不管`promise`最后的状态，在执行完`then`或`catch`指定的回调函数以后，都会执行`finally`方法指定的回调函数。

### 15.async 函数异步操作

ES2017 标准引入了 async 函数，使得异步操作变得更加方便。async 函数是什么？一句话，它就是 Generator 函数的语法糖。

`async`函数的返回值是 Promise 对象，这比 Generator 函数的返回值是 Iterator 对象方便多了

```javascript
 async function f() {
     //return await 'hello';
     let s=await 'hello world';
     let data=await s.split();
     return data;
}
//async函数中有多个await，那么then函数会等待所有await命令运行完结果 才去执行
  f().then(v => {
      console.log(v);//(11) ['h', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd']
   }).catch(err=>{
      console.log(err);
   })
```

`async`函数返回一个 Promise 对象，可以使用`then`方法添加回调函数。当函数执行的时候，一旦遇到`await`就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。

`async`函数内部抛出错误，会导致返回的 Promise 对象变为`reject`状态。抛出的错误对象会被`catch`方法回调函数接收到。

#### Async/await介绍

1. async/await是写异步代码的新方式，优于回调函数和Promise。

2. async/await是基于Promise实现的，它不能用于普通的回调函数。

3. async/await与Promise一样，是非阻塞的。

4. async/await使得异步代码看起来像同步代码，再也没有回调函数。但是改变不了JS单线程、异步的本质。(**异步代码同步化**)

   #### Async/await的使用规则

   凡是在前面添加了async的函数在执行后都会自动返回一个Promise对象

   await必须在async函数里使用，不能单独使用

   await后面需要跟Promise对象，不然就没有意义，而且await后面的Promise对象不必写then，因为**await的作用之一就是获取后面Promise对象成功状态传递出来的参数**。

   **当函数执行的时候，一旦遇到 await 就会先返回，等到触发的异步操作完成，再接着执行函数体内后面的语句**。

```javascript
async function f() {
  throw new Error('出错了');
}

f().then(
  v => console.log('resolve', v),
  e => console.log('reject', e)
)
//reject Error: 出错了
```

```javascript
 async function f2() {
     await Promise.reject('出错了');
     await Promise.resolve('hello');
}
  f2().then(v => {
      console.log(v);//出错了
  }).catch(err => {
      console.log(err);
  })
//当第一个await是返回reject的error结果，则后面的await就不会执行了
```

```javascript
async function f2() {
    try {
         await Promise.reject('出错了');
         } catch (error) {
             
        }
     return await Promise.resolve('hello');
}
f2().then(v => {
    console.log(v);//hello
}).catch(err => {
    console.log(err);
})
```

获取和风天气的Now数据

![image-20230816211718760](C:\Users\PNTL\AppData\Roaming\Typora\typora-user-images\image-20230816211718760.png)

```javascript
 async function getNowWeather(url) {
     //发送ajax获取实况天气
     let res = await getJOSN(url);
     console.log(res);
      //获取HeWeather6的数据 获取未来3-7天的天气
     let arr = await res.HeWeather6;
     return arr[0].now;
}
getNowWeather('http://free-api....').then(now => {
    console.log(now);
})
```

总结：Generator Promise async  为了解决回调地狱问题，使得异步操作更加方便。

### 16.Class 的基本语法

#### (1)类的由来

JavaScript 语言中，生成实例对象的传统方法是通过构造函数。下面是一个例子。

```javascript
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);
```

上面这种写法跟传统的面向对象语言（比如 C++ 和 Java）差异很大，很容易让新学习这门语言的程序员感到困惑。

ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过`class`关键字，可以定义类。

基本上，ES6 的`class`可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的`class`写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。上面的代码用 ES6 的`class`改写，就是下面这样。

```javascript
class Point {
     constructor(name, age) {
         this.name = name;
         this.age = age;
      }
}
//通过 Object.assign（）方法一次性向类中添加多个方法
Object.assign(Point.prototype, {
    sayName() {
        return this.name;
    },
    sayAge() {
        return this.age;
    }
})
let p1 = new Point('小马哥', 12);
console.log(p1);
```

上面代码定义了一个“类”，可以看到里面有一个**`constructor()`方法，这就是构造方法**，而`this`关键字则代表实例对象。这种新的 Class 写法，本质上与本章开头的 ES5 的构造函数`Point`是一致的.

#### (2)class的继承

Class 可以通过`extends`关键字实现继承，让子类继承父类的属性和方法。extends 的写法比 ES5 的原型链继承，要清晰和方便很多。

```javascript
 class animals {
      constructor(name, age) {
          this.name = name;
          this.age = age;
      }
      sayName() {
           return this.name;
      }
      sayAge() {
           return this.age;
      }
}
class Dog extends animals {
    constructor(name, age, color) {
        super(name, age);
        //等价于animals.call(this,name,age);
        this.color = color;
     }
    sayColor() {
        return `${this.name}是${this.age}岁了，它的颜色是${this.color}`
    }
    sayName() {
        return this.name + super.sayAge() + this.color
    }
}
let p1 = new Dog('小马', 12, 'red');
console.log(p1.sayName());//小马12red
console.log(p1.sayColor());//小马是12岁了，它的颜色是red
```

在子类的构造函数中，只有调用`super()`之后，才可以使用`this`关键字，否则会报错。这是因为子类实例的构建，**必须先完成父类的继承，只有`super()`方法才能让子类实例继承父类**。

```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
}

class ColorPoint extends Point {
  constructor(x, y, color) {
    this.color = color; // ReferenceError
    super(x, y);
    this.color = color; // 正确
  }
}
```

### 17.Module 模块化

#### 概述

历史上，JavaScript 一直没有模块（module）体系，无法将一个大程序拆分成互相依赖的小文件，再用简单的方法拼装起来。其他语言都有这项功能，比如 Ruby 的`require`、Python 的`import`，甚至就连 CSS 都有`@import`，但是 JavaScript 任何这方面的支持都没有，这对开发大型的、复杂的项目形成了巨大障碍。

在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。

ES6 模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。比如，CommonJS 模块就是对象，输入时必须查找对象属性。

#### export命令

模块功能主要由两个命令构成：`export`和`import`。`export`命令用于规定模块的对外接口，`import`命令用于输入其他模块提供的功能。

**一个模块就是一个独立的文件。**该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用`export`关键字输出该变量

```javascript
//module/index.js
export const name = 'zhangsan ';
export const age = 18;
export const color = 'red ';
export const sayName = function() {
    console.log(fristName);
}

//也可以这样
const name = 'zhangsan ';
const age = 18;
const color = 'red ';
const sayName = function() {
    console.log(fristName);
}
export {name,age,color,sayName}
```

```javascript
// 写法一
export var m = 1;

// 写法二
var m = 1;
export {m};

// 写法三
var n = 1;
export {n as m};
```

上面三种写法都是正确的，规定了对外的接口`m`。其他脚本可以通过这个接口，取到值`1`。它们的实质是，在接口名与模块内部变量之间，建立了一一对应的关系。

#### import命令

使用`export`命令定义了模块的对外接口以后，其他 JS 文件就可以通过`import`命令加载这个模块。

```javascript
//main.js
import {name,age,color,sayName,fn} from './modules/index.js';
```

如果想为输入的变量重新取一个名字，`import`命令要使用`as`关键字，将输入的变量重命名

```javascript
import * as obj from './modules/index.js';
console.log(obj);
```

#### export default 命令

使用`export default`命令为模块指定默认输出

```javascript
//export-default.js
export default function(){
    console.log('foo');
}

//或者写成
function foo() {
  console.log('foo');
}

export default foo;
```

在其它模块加载该模块时，`import`命令可以为该匿名函数指定任意名字

```javascript
//import-default.js
import customName from './export-default.js'
customNmae();//foo
```

如果想在一条import语句中，同事输入默认方法和其他接口，可以写成下面这样

```javascript
import customName,{add} from 'export-default.js'
```

对应上面`export`语句如下

```javascript
//export-default.js
export default function(){
    console.log('foo');
}

export function add(){
    console.log('add')
}
```

`export default`也可以用来输出类。

```javascript
// MyClass.js
export default class Person{ ... }

// main.js
import Person from 'MyClass';
let o = new Person();
```

