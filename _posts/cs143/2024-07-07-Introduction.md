---
title: lec1 Introduction & the Cool Programming Language
# author: alioth
date: 2024-07-06 22:34:23 +0800
categories: [csdiy, cs143]
tags: [c++]
description: none
---

### Introduction & the Cool Programming Language

#### 引入

- fortran 编译器的框架沿用至今
  - 词法分析(Lexical Analysis)
  - 语法分析(Parsing)
  - 语义分析(Semantic Analysis)
  - 优化(Optimization)
  - 代码生成(Code Geneeration)
  
#### 编译器的结构

- Lexical analysis divides program text into "words" or "tokens"
  - Onece words are understood, the next step is to understand sentence structure

- Parsing = Diagramming sentences
  - the diagramming is a tree 
  - Once sentence structure is understood, we can try to understand "meaning"
    - Hard!!

- Semantic Analysis: Compilers perform limited semantic analysis to catch inconsistencies(compiler don't kown what the program is supposed to do)
  - this is a ambiguice English sentences
    - "jack said jerry left his assignment at home"
    - "jack said jack left his assignment at home"
  - Programming languages define strict rules to avoid such ambiguties
  - Compiler perform many semantic check besides variable bindings
    - example: jack left her assignment at home
  - A `type mismatch` between her and jack; we kown they are different people
- Optimization
  - Automatically modify programs so that they
    - Run faster
    - Use less memory
    - In general, to conserve some resource
- Code Generation
  - Typically produces assembly code
  - Generally a translation into another language
    - Analogous to human translation

- and there is reference guideline:
![Desktop View](/assets/img/cs143/p2.png){: .normal}

#### the economic of programming language

- 成本 = 语言使用者 *　培训时间

- 传统语言的更新频率和新语言出现的速度？
  - 传统语言用户群体更大，每多改变一次带来的成本就越大，改变的东西越多成本越大
  - 新语言出现的速度越快成本就越大
  - 所以二者达到了一个微妙的平衡，新语言的用户少，所以就算频繁更新cost也不多，而老语言则是更新较少，但用户数量很多，二者达到一个平衡的状态