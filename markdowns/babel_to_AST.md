---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
title: babel编译之解析阶段
---

# babel编译之解析阶段

---

# babel编译

之前分享了关于模块打包、引入的文章，这一次进一步延伸分享下babel编译相关

babel编译处理有三个阶段
- 解析（baylon）：将javascript代码进行分析、转换生成AST语法树
- 转换（babel-traverse）：在这个阶段对AST语法树进行浏览、分析和修改，比如可以在这一步做tree shaking，转换生成新的AST语法树
- 生成（babel-generator）：将上一阶段转换生成的AST语法树 再重新编译回javascript代码

<img src="/public/label.png">


---

# babel解析

+ 解析（baylon）这一步有两个环节：
- 词法分析阶段：input => **tokenizer** => tokens，先对输入代码进行分词，根据最小有效语法单元，对字符串进行切割。
- 语法分析阶段：tokens => **parser** => AST，然后进行语法分析，会涉及到读取、暂存、回溯、暂存点销毁等操作。

---

# 什么是AST语法树


- 抽象语法树 (Abstract Syntax Tree)，简称 AST，它是源代码语法结构的一种抽象表示。

- 它以树状的形式表现编程语言的语法结构，树上的每个节点都表示源代码中的一种结构。

<img src="/public/ast.png">


<!--

-->

---

# 作用


- 📝 编辑器的错误提示、代码格式化、代码高亮、代码自动补全；
- 🛠 elint、pretiier 对代码错误或风格的检查；
- 📤 webpack 通过 babel 转译 javascript 语法、代码打包等；
- ...

---

# 如何生成AST语法树

## 解析器
能够将JavaScript源码转化为抽象语法树（AST）的工具叫做JS Parser解析器。

相同的JavaScript代码，通过各种parser解析的AST结果都是一样的，这是因为他们都参照了同样的[AST解析规范](https://github.com/estree/estree)

## 解析过程
- 词法分析（Lexical Analysis）：将整个代码字符串分割成最小语法单元数组
- 语法分析（Syntax Analysis）：在分词基础上建立分析语法单元之间的关系

---

# 词法分析

- input => **tokenizer** => tokens，先对输入代码进行分词，根据最小有效语法单元，对字符串进行切割。

<br>
<br>

**tokenizer怎么工作的？**

- 通过内部的readToken_numberSign与readWord方法，一个字符一个字符的读取并转换为标识符（如const）
- 将这些标识符根据类型属性（如点、左括号、右括号等等）转换为一个个的token，并放入到 tokens（扁平的语法片段数组）中
- token格式示例： { type: { ... }, value: "1", start: 0, end: 1, loc: { ... } },

<!-- 
比如const，会按 c o n s t直到空格为止，

35个关键字

1 * 2会分析成怎样？ 分别会是三个token

词法分析被抽象为了一个“有限状态自动机”，在某个状态下，满足一些条件后，会进行状态转移，转移到新的状态，从代码层面看，是一系列的 switch case 语句。经过词法分析后，代码被准确的切割，每个被切分的词叫做 token。

每一个 type 有一组属性
 type: {
    label: 'name',
    keyword: undefined,
    beforeExpr: false,
    startsExpr: true,
    rightAssociative: false,
    isLoop: false,
    isAssign: false,
    prefix: false,
    postfix: false,
    binop: null,
    updateContext: null
  },
-->

---

# 语法分析

- tokens => **parser** => AST，然后进行语法分析，会涉及到读取、暂存、回溯、暂存点销毁等操作。
- 语法分析也就是根据词法分析的结果（tokens），将其转换成AST

<br>
<br>

**parser怎么工作的？**

核心：根据每个token对象的属性，将每个token转换为节点插入AST语法树（有些token是不会生成节点，而是依附某个节点上的）

- 插入的逻辑会根据token属性的不同而不同，比如const会判断为是一个声明变量语句，会走 statement 模块执行分析；* 是一个表达式，会走expression模块执行分析
- 需要处理规则的嵌套（如嵌套中高优先级的运算规则需要先执行，插入节点的时候需要根据一系列规则算法进行处理）

<!-- 
函数也是表达式，function statement
上下文无关文法， LL 算法
 -->

---

# 参考文献

<br>

[ 【你应该了解的】抽象语法树AST (juejin.cn)](https://juejin.cn/post/6844904126099226631)

[高级前端基础-JavaScript抽象语法树AST - SegmentFault 思否](https://segmentfault.com/a/1190000018532745)

[手把手带你入门 AST 抽象语法树 (juejin.cn)](https://juejin.cn/post/6844904035271573511#heading-0)

[第 149 题：babel 怎么把字符串解析成 AST，是怎么进行词法/语法分析的？ · Issue #315 · Advanced-Frontend/](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/315)

[Parser API - Mozilla 产品与私有技术 | MDN](https://developer.mozilla.org/zh-CN/docs/Mozilla/Projects/SpiderMonkey/Parser_API)

[babel/index.js at main · babel/babel (github.com)](https://github.com/babel/babel/blob/main/packages/babel-parser/src/tokenizer/index.js)
