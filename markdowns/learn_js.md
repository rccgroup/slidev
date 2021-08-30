---
download: true
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# colorSchema: 'dark'
# some information about the slides, markdown enabled
info: |
  ## JavaScript培训资料

---

# JavaScript培训资料

---

## 概述

[思维导图](https://gitmind.cn/app/doc/cf42bbc83413c3519c5ee177dfcda140)

JavaScript是一种属于网络的脚本语言,已经被广泛用于Web应用开发,常用来为网页添加各式各样的动态功能,为用户提供更流畅美观的浏览效果。通常JavaScript脚本是通过嵌入在HTML中来实现自身的功能的。

· 是一种解释性脚本语言（代码不进行预编译）。
· 主要用来向HTML（标准通用标记语言下的一个应用）页面添加交互行为。
· 可以直接嵌入HTML页面，但写成单独的js文件有利于结构和行为的分离。
· 跨平台特性，在绝大多数浏览器的支持下，可以在多种平台下运行（如Windows、Linux、Mac、Android、iOS等）。

JavaScript脚本语言同其他语言一样，有它自身的基本数据类型，表达式和算术运算符及程序的基本程序框架。

---

## 数据类型

[文档](https://zh.javascript.info/types)

1、基本类型

Undefined、Null、布尔值（Boolean）、字符串（String）、数值（Number）、Symbol (ES6中新增)、BigInt（ES10中新增，现代浏览器都已支持）

2、引用类型

其他所有的数据类型都被称为“原始类型”，因为它们的值只包含一个单独的内容（字符串、数字或者其他）。

而相反，Object 则用于储存数据集合和更复杂的实体。

Function、Array类型都是继承自Object类型。

....

---

## 二、变量

大多数情况下，JavaScript 应用需要处理信息。这有两个例子：

- 一个网上商店 —— 这里的信息可能包含正在售卖的商品和购物车。
- 一个聊天应用 —— 这里的信息可能包括用户和消息等等。

变量就是用来储存这些信息的。

### 变量声明

变量 是数据的“命名存储”。我们可以使用变量来保存商品、访客和其他信息。

在 JavaScript 中创建一个变量，我们需要先声明，可以通过三种关键字进行不同类型的声明。
示例：

```js
var message // 变量（日常中可以尽量不使用了）
let message // 局部变量
const res // 常量
```

---

### 变量赋值

`JavaScript` 中的变量赋值方式十分简洁，不同类型的值也可以赋值给同一个对象（变量）。

```js
let message
message = 123
message = 1.2
message = 'Hello'
```

但是用const 声明的对象是不能重复赋值的，const声明的变量叫常量，它们不能被修改。

```js
const message = 1
message = 2 // 会报错
```

赋值类型：

- 值传递
- 引用传递

---

### 变量匹配

#### 1.类型判断

判断变量/对象类型

#### 2.值匹配

等于、大于、小于、包含、正则匹配...

---

## 三、函数

函数是程序的主要“构建模块”。函数使该段代码可以被调用很多次，而不需要写重复的代码。

例如，当访问者登录、注销或者在其他地方时，我们需要显示一条好看的信息，我们就可以定义一个函数专门处理这个功能需求。

---

函数声明

通过 function关键字 声明、创建函数。

```js
function test () {
  console.log('这是一个函数')
}
```

函数传参

```js
function test2 (message) {
  console.log('这个一个带参函数，参数是：', message)
}
```

函数调用与返回

```js
function test3 (message) {
  const word = 'World'
  return message + word // 函数返回
}

// 函数调用
test3('Hello')
```

---

## 四、原型与原型链

概念/理解：每一个JavaScript对象(null除外)在创建的时候就会与之关联另一个对象，这个对象就是我们所说的原型，每一个对象都会从原型"继承"属性。

[文档](https://github.com/mqyqingfeng/Blog/issues/2)

如：```const a = 1;``` 中，a这个对象就会继承Number这个原型（数据类型）中的属性

要点：

构造函数

prototype 属性（指向调用构造函数而创建出当前的实例的原型）

---

## 五、作用域与闭包

概念：作用域是指程序源代码中定义变量的区域。

作用域规定了如何查找变量，也就是确定当前执行代码对变量的访问权限。

因为 JavaScript 采用的是词法作用域，函数的作用域在函数定义的时候就决定了。

词法作用域中变量查找的顺序，是从函数内部开始，然后到函数定义的外层（作用域链），每个函数都会有自己的作用域和对应的变量。

[作用域](https://github.com/mqyqingfeng/Blog/issues/3)

[执行上下文](https://github.com/mqyqingfeng/Blog/issues/4)

[this指针](https://github.com/mqyqingfeng/Blog/issues/5)

[闭包与IIFE](https://github.com/mqyqingfeng/Blog/issues/9)

[bind/apply/call函数](https://github.com/mqyqingfeng/Blog/issues/11)

---

示例：

```js
let value = 1;

function foo() {
  console.log(value);
}

function bar() {
  let value = 2;
  foo();
}

bar();
```

---

## 六、事件循环与机制

[同步任务与异步任务](https://www.yuque.com/aomantiankong-bk96v/gdoh4b/mtv7gv)

[事件执行栈/调用栈](https://segmentfault.com/a/1190000018183651)

---

## 七、浮点数精度

IEEE 754标准，64位双精度浮点型

计算不准确问题（0.1+0.2!=0.3）

---

## 八、异常与处理

错误类型（常见：InternalError内部错误、Reference引用错误、SyntaxError语法错误 等等）

try/catch（错误/异常捕获）

---

## 九、ES6语法

---

### 迭代器

概念：依次处理该对象（数据集合）的所有成员

[Iterator](https://es6.ruanyifeng.com/#docs/iterator)

---

### Generator与async/await

[Generator 函数](https://es6.ruanyifeng.com/#docs/generator)是 ES6 提供的一种异步编程解决方案
是一种新的函数声明方式（function*）

可以自定义 函数执行与暂停（等待其他方法执行后继续进行等情况）

[async/await](https://es6.ruanyifeng.com/#docs/async)是generator的语法糖

---

### Promise

[Promise](https://es6.ruanyifeng.com/#docs/promise) 也是异步编程的一种解决方案

Promise定义了一种新的异步操作定义方式，这种新的方式涉及js底层的事件执行机制

<img src="https://static.cnodejs.org/FgKu20kvFqHrkgpjbQxXkV1DmrG1" alt="图来源https://cnodejs.org/topic/560dbc826a1ed28204a1e7de" style="height:70%;margin: auto;"/>


---

### Proxy与Reflect

[proxy](https://es6.ruanyifeng.com/#docs/proxy): 拦截与代理对 对象 的操作

[reflect](https://es6.ruanyifeng.com/#docs/reflect): 类似Java的反射，获取/修改对象本身的属性和方法

---

### 类与继承

语法上更像面对对象编程的语法

[文档](https://es6.ruanyifeng.com/#docs/class)

```js
class Foo {
  constructor () {}
  test () {
    console.log('foo.test')
  }
}

const foo = new Foo()
foo.test()
```

---

### 模块

[模块的导入与导出（import与export）](https://es6.ruanyifeng.com/#docs/module)

静态化（编译时确认依赖关系）

严格模式

---

## 九、资料

文档

- <https://github.com/mqyqingfeng/Blog>
- <https://es6.ruanyifeng.com/#README>
