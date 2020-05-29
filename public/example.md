# Current State of Cloud Ladder

---

## 我们是谁

---

|![](https://avatars0.githubusercontent.com/u/25377854?s=80&v=4)  <!-- .element height="50%" width="50%" -->|![](https://avatars1.githubusercontent.com/u/16451516?s=460&v=4) <!-- .element height="50%" width="50%" -->|
|:-:|:-:|
|YHR|FKY|

---

[![](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggVERcbiAgQVtDaHJpc3RtYXNdIC0tPnxHZXQgbW9uZXl8IEIoR28gc2hvcHBpbmcpXG4gIEIgLS0-IEN7TGV0IG1lIHRoaW5rfVxuICBDIC0tPnxPbmV8IERbTGFwdG9wXVxuICBDIC0tPnxUd298IEVbaVBob25lXVxuICBDIC0tPnxUaHJlZXwgRltmYTpmYS1jYXIgQ2FyXVxuXHRcdCIsIm1lcm1haWQiOnsidGhlbWUiOiJkZWZhdWx0In19)](https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZ3JhcGggVERcbiAgQVtDaHJpc3RtYXNdIC0tPnxHZXQgbW9uZXl8IEIoR28gc2hvcHBpbmcpXG4gIEIgLS0-IEN7TGV0IG1lIHRoaW5rfVxuICBDIC0tPnxPbmV8IERbTGFwdG9wXVxuICBDIC0tPnxUd298IEVbaVBob25lXVxuICBDIC0tPnxUaHJlZXwgRltmYTpmYS1jYXIgQ2FyXVxuXHRcdCIsIm1lcm1haWQiOnsidGhlbWUiOiJkZWZhdWx0In19)


---

## 提纲

- 我们目前的成果
- 什么是 Cloud Ladder
- Cloud Ladder 语言设计
- Cloud Ladder 语言实现

> 内容以分享经验心得为主

---

## 我们做了什么

--

### 一个新语言的诞生:
## [Cloud ladder](https://github.com/BIT-SYS/cloud-ladder)

```python
print("Hi, Cloud Ladder!")
```

--

它包括：

- [x] 一份~~不完整的~~规范
- [x] 一个~~不太好用的~~解释器
- [x] 一堆~~零散的~~文档

--

## 里程碑

- 三月初：项目开始，首先进行语言设计。
- 三月十五日：第一份 commit，开始进入代码实现。
- 四月十八日：语义分析分支出现，语法设计的实现完成。
- 四月二十日：IR 分支出现，AST 设计实现已经基本完成。
- 五月七日：IR 基本完成，开始进行解释器部分实现。
- 五月二十一日：加入 AI 的调用。
- 五月二十三日：结束 alpha 版本工作。

--

## Cloud Ladder 目前支持什么功能

- 类型
  - 基本类型
  - 列表
  - 多媒体类型
- 基本功能
  - 变量定义
  - 控制语句
  - 函数定义
  - 函数调用
  - 静态分析
  - 内置基本函数
- 嵌入 Java 编写的代码
- AI 支持的多媒体类型转换

---

## 什么是 Cloud Ladder

--

## 特点

- 面向云计算
- 内置 AI 支持 
- 面向教学
- GPL-3.0 许可证

--

## 架构

- 解释型语言
- 静态类型语言
- 强类型语言
- 基于 ANTLR4
- 基于 Java
- 基于 Gradle 进行构建

---

## 快速上手

--

## 代码仓库都包含什么？

- 目录结构
- 持续集成（CI）

--

- 运行代码
- 使用 Gradle 进行单元测试
- 生成调试信息

---

## Cloud Ladder 语言设计

--

## 为什么使用静态强类型的类型设计

--

## For 循环

--

## 类型系统

- 简单
- 正交
- 可扩展
  - 组合
  - 继承

--

## `NULL` 类型 

--

## 继承与接口的考量

--

## `variable.func()` 语法糖

--

众所周知，调用对象的方法其实只是把对象本身作为第一个参数调用函数。因此定义A的方法时也没必要写在class A的代码块中，直接定义第一个参数为A类型的函数即可。允许通过点操作符像函数第一个参数传参的方式被称为统一函数调用语法（UFCS），这种方式似的连续调用函数的代码看起来更清楚c(b(a()))→a().b().c()，而且也有助于封装。

--

不过Cloud Ladder并没有采用完全体的UFCS，我们规定只有第一个参数的名字为self时才能作为方法被调用。这样有助于帮助使用者规定自己定义的到底是方法还是函数。

--

## 默认返回

函数中没有return，返回最后一句表达式的返回值
那for/if呢？？

--

## 去除多余的 `()`

因为Cloud Ladder从最初起就规定了使用大括号表示代码块，所以if/for/while等语句的条件部分必定紧跟着`{`，在其中再加一层小括号实属多余，所以我们删去了多余的括号。

---

## Cloud Ladder 语言实现

--

## ANTLR

--

语法最初的设计是计老师完成的，他要求变量声明时类型要放在变量名前面、用大括号表示代码块。我们在其上做了些补充，比如if-elif-else、以换行符结尾等。最后的语法类似于java和kotlin的合体，因此我们以java的EBNF描述为底，删除了很多不必要的语法（如类的定义），结合了一部分kotlin语法。匿名函数的写法由F补充，来自 Rust（Rust 借鉴的 Haskell 和 SML）。

--

## AST 设计与实现

--

- 使用 Visiter
- 尽量提供代码复用的支持
- 为了传递更多的信息，AST 节点指向 ParserContext 节点

```mermaid
todo: 表示类关系的设计
```

--

## 静态分析

--

编译器的前端有两个检查：符号检查、类型检查

符号检查阶段建立符号表，可以检查未定义的变量和函数，不在for/while中的break和continue
符号表支持嵌套，代码块内的变量可以遮盖之外的变量。支持同名而参数类型不同的函数，通过name mangling实现

因为语法要求写出变量类型与函数的参数类型、返回值类型。所以类型检查阶段只是从语法树底端向上传递类型，在特殊节点检查类型是否符合要求即可(比如[a..b]需要ab都为Number类型)

--

## IR 设计与实现

--

IR 最早来自于龙书上的示例，但是龙书的例子比较简单。我们在原有的基础上为 AST 节点
增加了可复用的代码，然后定义了 IR。

在这一步，AST 和 IR 是非对称的映射。

--

为了给后续的执行提供支持，IR 的设计还需要考虑到：

- 如何使用标签解决跳转问题
- 如何传递标签
- 如何获得下一个执行语句
- 如何记录额外信息

--

## 解释器实现

--

解释器的难点主要在于设计运行时的环境。比如：

- 数据结构如何存储
- 函数和变量的调用栈如何设计
- 如何满足 break 这种需要弹出多个栈元素的 IR
- 如何内嵌 Java 代码

---

## 暂时的遗憾（目前还不能支持的功能）

- 函数式编程支持
  - 闭包
  - 函数是一等公民
- 语言支持
  - VSCode Language Plugin

---

## 致谢
