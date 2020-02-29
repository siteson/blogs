---
title: "第三章：MVC与其他框架模式的比较" 
date: 2020-02-26T16:01:23+08:00 
lastmod: 2020-02-26T16:01:23+08:00 
draft: false  
tags: ["MVC框架模式", "framework mode"] 
categories: ["MVC框架模式"]  
author: "Bob Si (整理)" 

comment: true
toc: true        # 文章目录
reward: false	 # 打赏
mathjax: true    # 打开 mathjax
---

# 前言

复杂的软件必须有清晰合理的架构，否则无法开发和维护。

MVC（Model-View-Controller）是最常见的软件架构之一，业界有着广泛应用。它本身很容易理解，但是要讲清楚它与衍生的 MVP 和 MVVM 架构的区别就不容易了。

昨天晚上，我读了[《Scaling Isomorphic Javascript Code》](http://blog.nodejitsu.com/scaling-isomorphic-javascript-code/)，突然意识到，它们的区别非常简单。我用几段话，就可以说清。

阮一峰  
2015年2月1日

## 一、MVC

MVC模式的意思是，软件可以分成三个部分。

![mvc1.png](/images/compare-mvc-with-anothers/20200226001.png)

> 1. 视图（View）：用户界面  
> 2. 控制器（Controller）：业务逻辑  
> 3. 模型（Model）：数据保存

各部分之间的通信方式如下:

![mvc2.png](/images/compare-mvc-with-anothers/20200226002.png)

> 1. View 传送指令到 Controller  
> 2. Controller 完成业务逻辑后，要求 Model 改变状态  
> 3. Model 将新的数据发送到 View，用户得到反馈

所有通信都是单向的。

## 二、互动模式

接受用户指令时，MVC 可以分成两种方式。一种是通过 View 接受指令，传递给 Controller。

![interact.png](/images/compare-mvc-with-anothers/20200226003.png)

另一种是直接通过controller接受指令。

## 三、实例：Backbone

实际项目往往采用更灵活的方式，以 [Backbone.js](https://github.com/jashkenas/backbone/) 为例。

![backbone.png](/images/compare-mvc-with-anothers/20200226004.png)

1. 用户可以向 View 发送指令（DOM 事件），再由 View 直接要求 Model 改变状态。

2. 用户也可以直接向 Controller 发送指令（改变 URL 触发 hashChange 事件），再由 Controller 发送给 View。

3. Controller 非常薄，只起到路由的作用，而 View 非常厚，业务逻辑都部署在 View。所以，Backbone 索性取消了 Controller，只保留一个 Router（路由器） 。

## 四、MVP

MVP 模式将 Controller 改名为 Presenter，同时改变了通信方向。

![mvp.png](/images/compare-mvc-with-anothers/20200226005.png)

1. 各部分之间的通信，都是双向的。

2. View 与 Model 不发生联系，都通过 Presenter 传递。

3. View 非常薄，不部署任何业务逻辑，称为"被动视图"（Passive View），即没有任何主动性，而 Presenter非常厚，所有逻辑都部署在那里。

## 五、MVVM

MVVM 模式将 Presenter 改名为 ViewModel，基本上与 MVP 模式完全一致。

![mvvm.png](/images/compare-mvc-with-anothers/20200226006.png)

唯一的区别是，它采用双向绑定（data-binding）：View的变动，自动反映在 ViewModel，反之亦然。[Angular](https://angularjs.org/) 和 [Ember](https://emberjs.com/) 都采用这种模式。

# 结语

看完这些，相信你已经基本掌握了MVC模式的设计思路。在[下一章节](/post/example-of-mvc-mode/)中我将为大家剖析一个使用MVC模式架构的应用，再一起巩固一下学习！


# Reference  
* [MVC.wiki](https://zh.wikipedia.org/wiki/MVC)  
* [mvc-index](http://heim.ifi.uio.no/~trygver/themes/mvc/mvc-index.html)
* [Model-View-Controller.Cocoa-Core-Competencies.apple-developer](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html#//apple_ref/doc/uid/TP40008195-CH32-SW1)  
* [MVC，MVP 和 MVVM 的图示 - 阮一峰](http://www.ruanyifeng.com/blog/2015/02/mvcmvp_mvvm.html)

# Index  
[MVC框架模式系列](/categories/mvc%E6%A1%86%E6%9E%B6%E6%A8%A1%E5%BC%8F/)：  
* [第一章：认识MVC框架模式](/post/what-is-mvc-mode/)  
* [第二章：MVC框架模式发展史](/post/history-of-mvc-mode/)  
* [第三章：MVC与其他框架模式的比较](/post/compare-mvc-with-anothers/)  
* [第四章：MVC框架模式案例分析](/post/example-of-mvc-mode/)  