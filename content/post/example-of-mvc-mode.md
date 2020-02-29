---
title: "第四章：MVC框架模式案例分析" 
date: 2020-02-28T16:01:23+08:00 
lastmod: 2020-02-28T16:01:23+08:00 
draft: false  
tags: ["MVC框架模式", "framework mode", "software engine"] 
categories: ["MVC框架模式"]  
# author: "司想" 

comment: true
toc: false       # 文章目录
reward: false	 # 打赏
mathjax: true    # 打开 mathjax
---

# 前言

如果你想使用 MVC 模式开发应用，我们没必要从零开始，使用现成的骨架是一个不错的选择。无论是web、Android、iOS 还是别的应用场景，都有基于MVC、MVP、MVVM的骨架，你可以利用互联网轻易地找到。

网站引擎 [Hugo](https://gohugo.io/commands/hugo/) 就是一个基于MVC模式的应用，它使用Go语言编写，非常简单且功能强大。能够将你的文章生成为静态网站，你可以把它部署到共享服务器甚至 github 上。

对于分析MVC框架模式来说，这是一个很好的例子。

## Part 1

### 我们先看一下 Hugo 的设计逻辑：

> 1. Hugo 应用本身 (Control)  
>
> 2. 主题模板 (View)
>
> 3. 文章和配置文件 (Model)

Hugo 官方已经为我们提供了执行应用（控制层），主题商店（视图层）。  

因此我们只需要关注模型层，也就是文章本身就好了。这样大大提高了博客网站的开发效率。

当然，你也可以自己制作模板以及在github上为应用提供代码，它具有很高的自由度。

## Part 2

我们来尝试一下。

### 安装 Hugo

在终端上执行：

Mac & Linux  
```bash
brew install hugo
```

Windows
```shell
iwr -useb get.scoop.sh | iex
scoop install hugo
```

### 初始化网站

在你想要存放的目录下执行：

```
hugo new site blogs
```

### 添加一个主题

去官方提供的主题商店里选一个，[点击这里](https://themes.gohugo.io/)。大部分都是免费的，如果对方有提供 Donate 选项，记得给他捐钱。

挑好后，在你选中的主题那里往下翻，执行 Installation 里的安装命令。

如果要用到 git 克隆，小白可以参考 [这篇文章](https://www.jianshu.com/p/3ef797fcb17d) 快速学习，这里不过多赘述。

### 本地测试

通过本地测试来调试你的网站：

```
hugo server
```

然后浏览器打开 [http://localhost:1313](http://localhost:1313)，你将看到你的主题模板，例如：

![Example-theme-Terrassa](/images/example-of-mvc-mode/20200301012242.png)

说明你的本地hugo站可以工作了。

### 修改默认的配置

在 themes 文件夹中找到你的主题，拷贝 exampleSite 文件夹中的 config.toml 文件到你本地站的根目录。一般会有一个 ful-config.toml，里面有详细的配置说明。

根据配置说明修改 config,toml，这便是你的配置文件。

建议仔细阅读主题网站中的内容，它会提供详细的使用帮助。

### 编辑博文

- 把 exampleSite 中 content 文件夹里的内容复制到网站根目录下的 content 中。  
这个content文件夹便是用来存放你文章的地方，里面的 xxxx.md 文件就是你的文章，随便一个文本编辑器就可以打开。  

- 删除 exampleSite。删除之后所剩下的便只有你的内容，当然你可以自行备份一下，方便参考。

- 图片放到本地站根目录下的 static 文件夹中。那个是你的静态元素的存放位置。

文章支持使用 markdown 语法。写文章时，需要在最上放插入一段配置，可以这样编写：

```
---
date: 2020-02-15    # 编辑日期
title: "你的标题"
tags: ["关键词", "标签", "关键词"] 
categories: ["类别"]  
author: "作者姓名"
draft: false      # 是否为草稿
comment: true     # 是否打开评论
toc: false        # 文章目录
reward: false	  # 打赏
mathjax: true     # 是否打开 mathjax
---
```

生成网站后 content 和 static 目录将作为实际根目录。  
例如下面这张图的存放位置是 `/static/images/example-of-mvc-mode/example.jpg`

![图例2](/images/example-of-mvc-mode/example.jpg)

你在文章中就需要这么写：

```markdown
![图例2](/images/example-of-mvc-mode/example.jpg)
```

### 部署网站

在本地网站根目录下执行命令：  
```
hugo
```

很快便会生成一个 public 文件夹。这个文件夹里面就是 hugo 生成的静态网站。将它上传到你的仓库、服务器或者直接用 Apache 转发，一个高效的网站就搭建完成了。

# 结语

通过这个案例我们可以看到，MVC框架模式使网站开发变得非常高效。  
一个良好的模式所拥有的潜力是巨大的，无论做什么工作，我们似乎都应该重新审视模式的重要性。

# Reference  
* [Slim 4 Documentation](http://www.slimframework.com/docs/v4/)
* [Hugo Documentation](https://gohugo.io/documentation/)

# Index  
[MVC框架模式系列](/categories/mvc%E6%A1%86%E6%9E%B6%E6%A8%A1%E5%BC%8F/)：  
* [第一章：认识MVC框架模式](/post/what-is-mvc-mode/)  
* [第二章：MVC框架模式发展史](/post/history-of-mvc-mode/)  
* [第三章：MVC与其他框架模式的比较](/post/compare-mvc-with-anothers/)   
* [第四章：MVC框架模式案例分析](/post/example-of-mvc-mode/)  