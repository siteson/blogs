---
title: "第二章：MVC框架模式发展史" 
date: 2020-02-25T16:01:23+08:00 
lastmod: 2020-02-25T16:01:23+08:00 
draft: false  
tags: ["MVC框架模式", "framework mode"] 
categories: ["MVC框架模式"]  
author: "Bob Si (整理)" 

comment: true
toc: true        # 文章目录
reward: false	 # 打赏
mathjax: true    # 打开 mathjax
---

# 前言：  
上一章节我们基本认识了MVC框架模式，本章我们将从历史的角度深入了解MVC，重点介绍它的应用分支以及发展现状。  

# 波澜壮阔的MVC发展史

> **MVC模式** 最早是由Trygve Reenskaug在1978年提出的一种软件架构，其目的是实现一种动态的程序设计，使后续对程序的修改和扩展简化，并且使程序某一部分的重复利用成为可能，并使程序结构更加直观。  

## 一、Model1 模式的出现，让混沌世界出现一丝曙光

Model1 模式[^1]十分简单，它使用 JSP 页面和 JavaBean 相结合的方式，由 JSP 页面来接收客户端请求，用 JavaBean[^2] 或其他服务完成业务逻辑、数据库操作和返回页面。

[^1]:**Model1模式** 出现前，整个Web应用的情况：几乎全部由JSP页面组成，JSP页面接受处理客户端请求，对请求处理后直接做响应。这样做的弊端是在界面层充斥着大量的业务逻辑的代码和数据访问层代码，Web程序的可扩展性和维护性非常差。（本文以Java举例，不代表该模式只适合Java）  
[^2]:**Javabean** 是指能完成特定功能的 Java 类。它使得我们能在 JSP 中直接调用，大大提升了程序的可维护性。

![model1.png](/images/history-of-mvc-mode/1_model1.png)

### 1.1 Model1 模式的优缺点  
（1）优点：架构简单，比较适合小型项目开发  
（2）缺点：JSP 职责不单一，职责过重，不便于维护

## 二、Model2（MVC）开发模式，让刀耕火种的原始时代迈入了石器时代，社会开始分工，生产更加有秩序

Model1 虽然在一定程度上实现了解耦，但 JSP 依旧即要负责页面控制，又要负责逻辑处理，职责不单一。此时 Model2 应运而生，使得各个部分各司其职。 Model2 基于 MVC 模式：

（1）Controller：应用程序中用户交互部分（Servlet）  
（2）Model：应用程序数据逻辑部分（JavaBeans）  
（3）View：数据显示部分（JSP）  

![model2.png](/images/history-of-mvc-mode/2_model2.png)

### 2.1 Model2 模式的优缺点  
（1）优点：职责清晰，较适合于大型项目架构  
（2）缺点：分层较多，不适合小型项目开发

### 2.2 Model1 和 Model2 区别  
Model2 在 Model1 的基础上分离了控制，将 JSP 中的逻辑操作部分分离出来，这样做不仅减轻了 JSP 的职责，而且更有利于分工开发，耦合性降低。对于复杂的 Web 应用开发，更适合使用 Model2，而对于小型应用，使用Model1 比较简单。

## 三、Struts1 登上历史舞台，但又匆匆走过

### 3.1 Struts1 诞生背景  
Struts1[^3] 出现的目的是为了帮助我们减少在运用MVC设计模型来开发Web应用的时间，使用Struts1可以提高系统的维护和开发效率，我们只需要配置和编码实现Action和ActionForm就可以了。

[^3]:**Struts1框架** 是apache公司的开源子项目，是基于mvc逻辑分层的web层框架实现。是出现最早的web层框架，应用最广。Struts1框架重点关注的是控制层，对于视图层只是提供了大量的标签；对于model层的影响微乎其微。

### 3.2 Struts1 组成部分  
![struts1.jpg](/images/history-of-mvc-mode/3_2_struts1.jpg)  

下面，对比一下Servlet和Struts1的执行过程，我们更能看清楚两者的区别。

### 3.3 Servlet 执行过程  
需要再每个页面都设置一个Servlet类来处理请求和响应，再获取用户提交的数据和再把数据与持久化类对应起来。再做判断，决定跳转，再让JSP显示。

![servlet.png](/images/history-of-mvc-mode/3_3_servlet.png)  

### 3.4 Struts1 执行过程  
使用Struts1时，通过运行时（runtime）初始化ActionServlet，再把所有持久化类的各个属性设为null。当有请求来时，通过name属性找到form-beans中form-bean的name属性，得到ActionForm的包名类名。然后实例化form，把用户数据提交给它，调用form的validate 方法验证。ActionErrors返回null表示验证通过，否则失败返回。验证通过会根据请求的Action类型实例化Action，执行Action的execute方法。根据传进来的ActionForm持久化对象可以取到传进来的数据，这个数据可以先和数据库中的数据交互，再决定跳转。  
也就是说Struts1封装了request.getParameter()，再把数据传给JavaBean持久化类。另外，Struts1弥补了JPS标签的不足，为开发提供了便利。

![3_4_struts1.png](/images/history-of-mvc-mode/3_4_struts1.png)   

## 四、Struts2 框架，雄心勃勃，但又毁誉参半

### 4.1 Struts2 诞生背景  
Struts2和Struts1的差别巨大，Struts2以WebWork为核心，采用拦截器的机制来处理用户的请求，这样的设计也使得业务逻辑控制器能够与Servlet API完全脱离开。

### 4.2 Struts1与Struts2的区别  
下面主要从Action类，线程模式，Servlet依赖，捕获输入，以及表达式语言等五个方面来进行比较。  

- （1）Action类  
Struts1要求Action类继承一个抽象基类；Struts2要求Action类可以实现一个Action接口，也可以实现其他接口。

- （2）线程模式  
Struts1是单例设计模式并且必须是线程安全的，因为仅有一个Action的实例来处理所有请求。而Struts2为每一个请求产生一个实例，因此没有线程安全问题。

- （3）Servlet依赖  
Struts1 Action依赖于Servlet API，因为当一个ACtion被调用时HttpservletRequest和HttpServletResponse被传递给execute方法。Struts2 Action不依赖于容器，允许Action脱离容器单独被测试。

- （4）捕获输入  
Struts1 使用ActionForm对象捕获输入，所有的Actionform必须继承一个基类。而Struts2直接使用Action属性作为输入属性。

- （5）表达式语言  
Struts1 整合了JSTL El表达式。而Struts2不仅可以使用JSTL，也支持ognl表达式语言。

### 4.3 Struts2 的安全问题异常严峻  
Struts2在前几年可谓是非常流行，不管你去哪个公司面试，都要求会SSH，这时的SS指的是Spring和Struts2，曾经风靡一时的Struts2最终被SpringMVC所取代。Struts2 的安全漏洞，让不少大小公司吃尽了苦头，慢慢磨掉了用户的信心。

## 五、SpringMVC 如日中天

### 5.1 SpringMVC 原理  
![5_1_springmvc.jpg](/images/history-of-mvc-mode/5_1_springmvc.jpg)   

Spring[^4], SpringMVC[^5]

[^4]:**Spring** 是一个开源框架，是为了解决企业应用程序开发复杂性而创建的。Spring使用的是基本的JavaBean来完成以前只可能由EJB完成的事情。  
[^5]:**SpringMVC** 是在Spring框架中内置的MVC子框架。

### 5.2 SpringMVC和Struts2的区别  
- （1）入口不同  
SpringMVC入口是servlet，Struts2入口是filter。

- （2）生命周期不同  
SpringMVC Controller是单例的，所以效率更高，但是不能使用成员变量获取参数。
Struts2 Action是多例的，可以使用成员变量获取参数，导致效率比较低。

SpringMVC中文官网： http://www.springmvc.cn/

# 结语

起至今日的MVC发展史就介绍到这里。随着对MVC的使用，我们发现它也存在诸多不适用的地方，因此市面上也诞生了许多别的模式，如：MVP、MVVM等。所以我们应该从实际项目出发，使用适合的模式，甚至不严格遵循某一模式。  
关于框架模式如何挑选，想要了解MVC和别的主流框架模式的区别，请看[下一章节](/post/compare-mvc-with-anothers/)。

# Reference  
* [MVC.wiki](https://zh.wikipedia.org/wiki/MVC)  
* [mvc-index](http://heim.ifi.uio.no/~trygver/themes/mvc/mvc-index.html)
* [Model-View-Controller.Cocoa-Core-Competencies.apple-developer](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html#//apple_ref/doc/uid/TP40008195-CH32-SW1)  
* [浅谈 MVC、MVP 和 MVVM 架构模式 - 面向信仰编程](https://draveness.me/mvx)
* [波澜壮阔的MVC发展史 - MyBatis](http://www.mybatis.cn/archives/634.html)

# Index  
[MVC框架模式系列](/categories/mvc%E6%A1%86%E6%9E%B6%E6%A8%A1%E5%BC%8F/)：  
* [第一章：认识MVC框架模式](/post/what-is-mvc-mode/)  
* [第二章：MVC框架模式发展史](/post/history-of-mvc-mode/)  
* [第三章：MVC与其他框架模式的比较](/post/compare-mvc-with-anothers/)   
* [第四章：MVC框架模式案例分析](/post/example-of-mvc-mode/)    