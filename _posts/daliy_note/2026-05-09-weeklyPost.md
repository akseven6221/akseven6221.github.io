---
title: weekly_post
# author: alioth
date: 2026-05-09 00:00:00 +0800
categories: [daliy, post]
tags: [notes]
description: none
---

这周开始算是正式进入状态学习算子编译器了，但组里让我学习的几个算子lowering的过程感觉还是有点摸不着头脑。
首先是设计到了会用到gpu的线程布局的算子，有几条路线走，lowering过程就很复杂。
再然后就是分布式的算子，设计到了hopper架构里的Thread Block Cluster这种东西，也是让我感到非常困惑。
还有就是一个关于流水线的算子，这个也让我觉得很困惑，不是很懂流水线是怎么具体影响到算子速度的。
总之结论就是现在的这些算子是需要大量的实践才能理解他们为什么要存在，需要深入系统的学习英伟达的计算卡的体系结构和cuda编程和实践这些算子才能更好的理解他们。