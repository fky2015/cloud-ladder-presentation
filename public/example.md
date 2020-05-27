# Current State of Cloud Ladder

---

## Who's Speaking

- YHR
- FKY

<!-- 可以弄个头像 -->

---

## What's this Presentation About.

[TOC]

---

## What Have We Done

--

### Annoucing a new language:
## Cloud ladder!

```python
print("Hi, Cloud Ladder!")
```

- [x] specification
- [x] interpreter
- [x] document

--

## MileStone


time + action


TODO

---

## What Is Cloud Ladder

--

## feature

- cloud native
- Builtin AI support
- GPL-3.0 License

--

## architecture

- interpret language
- static type
- strong type
- based ANTLR4
- based on java

---

## Quick Start

--

code repo

- workspace structure
-  CI
- release

--

- run demo
- test with gradle
- debug info

---

## Programming Language Design

--

## Why use strong and static type

--

## for loop

--

## type system

--

## null type

--

## Inherit vs Interface

--

## `variable.func()` sugar syntax

--

众所周知，调用对象的方法其实只是把对象本身作为第一个参数调用函数。因此定义A的方法时也没必要写在class A的代码块中，直接定义第一个参数为A类型的函数即可。允许通过点操作符像函数第一个参数传参的方式被称为统一函数调用语法（UFCS），这种方式似的连续调用函数的代码看起来更清楚c(b(a()))→a().b().c()，而且也有助于封装。

--

不过Cloud Ladder并没有采用完全体的UFCS，我们规定只有第一个参数的名字为self时才能作为方法被调用。这样有助于帮助使用者规定自己定义的到底是方法还是函数。

--

## default return

函数中没有return，返回最后一句表达式的返回值
那for/if呢？？

--

## remove  useless ()
因为Cloud Ladder从最初起就规定了使用大括号表示代码块，所以if/for/while等语句的条件部分必定紧跟着`{`，在其中再加一层小括号实属多余，所以我们删去了多余的括号。

---

## Programming Language Implementation

--

## ANTLR

--

## AST

--

- 使用 Visiter

```mermaid
A->B
```

--

## Static Analysis

--

## IR

--

## Interpreter

---

## What We Haven't Support Yet

---

## Roadmap
