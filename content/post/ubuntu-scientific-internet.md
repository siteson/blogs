---
# 常用定义
title: "Ubuntu使用 V2ray 科学上网" 
date: 2020-02-02T16:01:23+08:00 
lastmod: 2020-02-16T16:01:23+08:00 
draft: false  
tags: ["ubuntu", "v2ray", "VPN", "2020"] 
categories: ["打开世界的大门"]  
# author: "Bob Si" 

# 你可以选择 关闭(false) 或者 打开(true) 以下选项
comment: true
toc: true       # 文章目录
reward: false	 # 打赏
mathjax: true    # 打开 mathjax
---

# 前言：

V2Ray 是一个与 Shadowsocks 类似的代理软件，可以用来科学上网（翻墙）学习国外先进科学技术。

> 随着时间的推移，许多陈年教程贴已经失效。所以我整理了一份较为全面的2020版供大家参考。  
> 编写平台：Ubuntu 18.04 LTS

首先贴上ss的购买链接，在这里你可以买到一份服务器端的账号：  
http://jsssa.top/W9MKK  
这里面也包含Windows、macOS、Android、iOS的使用指南。

已购买或者已拥有相关服务器，请看下面的指南来完成客户端的配置。

# GUI版：

这是一个**简单有效**的图形用户界面客户端，可以通过这个链接免费下载：  
[https://github.com/jiangxufeng/v2rayL](https://github.com/jiangxufeng/v2rayL)  
但是目前来看并不十分稳定，欢迎去给原作者贡献代码。如果不嫌麻烦，建议使用官方提供的终端版，也就是下面的版本。

# 终端版：

### 一、通过snap安装v2ray

`sudo snap install v2ray-core`

由于终端下不支持使用订阅链接，所以填写配置信息需要先转到windows平台，在windows端的v2rayN安装目录中找到 config.json ，然后  
``` bash
# 以管理员身份打开文件管理器
sudo nautilus
```  
替换 /etc/v2ray/config.json

### 二、操作 v2ray

启动 V2Ray：  
`sudo service v2ray start`

停止 V2Ray：  
`sudo service v2ray stop`

重启 V2Ray：  
`sudo service v2ray restart`

显示 V2Ray 状态：  
`service v2ray status`

如果能看到一个绿色的小圆点（如下图所示），则说明运行正常

![2020-02-17 03-59-17屏幕截图.jpg](/images/ubuntu-scientific-internet/03-59-17.jpg)

### 三、设置代理

#### 浏览器下的代理：

方法a：

打开系统网络设置，把网络代理设为手动。socks 中填入回环ip，端口中填入v2ray配置文件里的监听端口，“忽略主机”填入 127.0.0.1;[::1];localhost

>在不使用代理的时候需要重新设为禁用，否则stop v2ray后会失去网络连接。

![2020-01-26 03-39-12屏幕截图.png](/images/ubuntu-scientific-internet/03-39-12.png)


方法b：

使用 SwitchyOmega 插件进行带PAC模式的连接。

安装 SwitchyOmega 插件：
[https://github.com/FelisCatus/SwitchyOmega/releases](https://github.com/FelisCatus/SwitchyOmega/releases)

>Chrome如果出现安装错误，把文件后缀名改为 7z 或 rar 解压出来，选择“加载已解压的拓展程序”进行安装

#### 终端下的代理：

1. 下载proxy-chain：  
`sudo apt install proxychains`

2. 修改参数:  
`sudo nano /etc/proxychains.conf`   
最后一行改为： socks5 127.0.0.1 10808   
这里的10808就是v2ray的socks5 代理端口，要保持和config里一致。

3. 测试proxy-chain:   
`proxychains wget http://www.google.com`

4. 使用proxy-chain:  
在你的命令前加上 `proxychains` 如：  
``` bash
proxychains wget www.google.com
sudo proxychains wget www.google.com
```

**终端下的使用步奏总结：**  
``` bash
sudo service v2ray start # 开启v2ray
proxychains # 你的命令
sudo service v2ray stop # 关闭v2ray
```

### 四、配置 PAC

PAC(Proxy auto-config)：使国内网站依旧走本地网络
我们通过[GenPAC](https://github.com/JinnLynn/genpac)来生成pac文件

1. 安装  
`pip install genpac`

2. 从gfwlist生成代理信息为SOCKS5 127.0.0.1:10808的PAC文件：  
`genpac --format=pac --pac-proxy="SOCKS5 127.0.0.1:10808" -o /etc/v2ray/autoproxy.pac`

3. 把pac文件的位置填入自动网络代理的“配置URL”中：  
![2020-01-26 03-49-13屏幕截图.jpg](/images/ubuntu-scientific-internet/03-49-13.png)

# 结语：
以上就是 Ubuntu 使用 V2ray 科学上网的全部内容。如有问题，欢迎留言。