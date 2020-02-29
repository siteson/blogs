---
title: "第一章：认识MVC框架模式" 
date: 2020-02-17T16:01:23+08:00 
lastmod: 2020-02-17T16:01:23+08:00 
draft: false  
tags: ["MVC框架模式", "framework mode"] 
categories: ["MVC框架模式"]  
author: "Bob Si (整理)" 

comment: true
toc: false        # 文章目录
reward: false	 # 打赏
mathjax: true    # 打开 mathjax
---

# 前言

如何设计一个程序的结构，这是一门专门的学问，叫做"框架模式"（architectural pattern），属于编程的方法论。

MVC模式就是框架模式的一种，它对我的启发特别大。我觉得它不仅适用于开发软件，也适用于其他广泛的设计和组织工作。

MVC模式并没有非常详细的定义，下面是我对它的简单梳理，便于整理思路。

阮一峰  
2007.11.08

### Part 1

**MVC模式（Model–view–controller）把软件系统分为三个基本部分：模型(Model)、视图(View)和控制器(Controller)。** 

这个模式认为，程序不论简单或复杂，从结构上看，都可以分成三层。

> 1）最上面的一层，是直接面向最终用户的"视图层"（View）。它是提供给用户的操作界面，是程序的外壳。 
> 
> 2）最底下的一层，是核心的"数据层"（Model），也就是程序需要操作的数据或信息。
>
> 3）中间的一层，就是"控制层"（Controller），它负责根据用户从"视图层"输入的指令，选取"数据层"中的数据，然后对其进行相应的操作，产生最终结果。

这三层是紧密联系在一起的，但又是互相独立的，每一层内部的变化不影响其他层。每一层都对外提供接口（Interface），供上面一层调用。这样一来，软件就可以实现模块化，修改外观或者变更数据都不用修改其他层，大大方便了维护和升级。

### Part 2

![what-is-mvc-mode_3.jpg](/images/what-is-mvc-mode/whatismvcmode_3.jpg)

我用Windows的计算器小程序为例，解释一下MVC模式，虽然它不一定使用这个模式编写。

在这个计算器程序中，外部的那些按钮和最上面的显示条，就是"视图层"，那些需要运算的数字就是"数据层"，执行加减乘除的那些内部运算步骤就是"控制层"。每一层执行不同的功能，整个程序的结构非常清楚。

如果我们扩大一点想象，就会发现，很多程序本质上都是这种模式：对外提供一组触发器（本例中是按钮），然后执行一些内部操作，最后返回结果。因此，MVC模式的应用是非常广泛的。

### Part 3

![what-is-mvc-mode_4.jpg](/images/what-is-mvc-mode/whatismvcmode_4.jpg)

在我看来，不仅编写程序可以用MVC模式，家用电器也可以用。

以家用微波炉为例，可以将它也理解成三层结构。最简单的情况下，微波炉的操作用两个转盘实现，一个控制温度，另一个控制时间。这两个转盘就是"视图层"（view），而其内部的微波产生装置则是"数据层"（Model），这里的"数据"需要理解成"核心功能"。至于将用户通过转盘输入的信息，转换成对微波产生器的操作，则用"控制层"来实现。

如果每一层都是独立的，那么微波炉外部更换一个新潮的外壳，或者内部更换更大功率的微波产生器，完全可以在不更改其他层的情况下实现。这就是MVC模式的优势。

### Part 4

**再进一步，如果将MVC模式解释成"外观"、"机制"和"功能/数据"这三层结构，那么很多人类组织也可以通过MVC模式架构。**

比如一家商场，完全可以分成三部分。一部分是仓库，负责提供商品，这是"功能层"（或者"数据层"）；另一部分是零售铺面，负责销售商品，这是它的"外观层"；两者之间就是"机制层"，包括柜台和仓库之间一切互动的机制。

这样区分以后，这个商场的结构就变得非常清楚，可以针对不同的层进行优化，提高效率。

# 结语

**公司、政党、政府、医院、学校等等，这些组织不管是盈利性还是非盈利性的，都可以从MVC模式的角度进行架构，由一个个执行特定功能、可重复使用的模块组成。**

想要了解更多有关MVC的发展与使用，请看[下一章节](/post/history-of-mvc-mode/)。

# Reference  
* [MVC.wiki](https://zh.wikipedia.org/wiki/MVC)  
* [mvc-index](http://heim.ifi.uio.no/~trygver/themes/mvc/mvc-index.html)
* [Model-View-Controller.Cocoa-Core-Competencies.apple-developer](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html#//apple_ref/doc/uid/TP40008195-CH32-SW1)  
* [谈谈MVC模式 - 阮一峰](http://www.ruanyifeng.com/blog/2007/11/mvc.html)

# Index  
[MVC框架模式系列](/categories/mvc%E6%A1%86%E6%9E%B6%E6%A8%A1%E5%BC%8F/)：  
* [第一章：认识MVC框架模式](/post/what-is-mvc-mode/)  
* [第二章：MVC框架模式发展史](/post/history-of-mvc-mode/)  
* [第三章：MVC与其他框架模式的比较](/post/compare-mvc-with-anothers/)   
* [第四章：MVC框架模式案例分析](/post/example-of-mvc-mode/)  