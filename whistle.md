---
title: 使用 whistle 抓包调试
date: 2018-06-27 16:13:29
categories: 笔记本
toc: true
tags:
  - 抓包
  - 调试
  - whistle
---

网上抓包调试工具设置大都是基于 Fiddler 的, macOS 下的设置大多是基于 charles. 后来发现了跨平台的 whistle, 在 windows 和 macOS 下均可方便的切换使用. 本文目的在于用5分钟快速配置抓包环境, 覆盖日常前台开发的场景.更多的功能可以查看官方文档.


## 安装

1.安装最新版 [Node.js](https://nodejs.org/en/)


2.安装 [whistle](http://wproxy.org/whistle/)

这里可以使用 npm 或者 tnpm 安装

```bash
npm install -g whistle

# 可能需要 sudo
sudo npm install -g whistle
```

3.Chrome 浏览器安装代理插件 [Proxy SwitchyOmega](https://chrome.google.com/webstore/detail/proxy-switchyomega/padekgcemlokbadohgkifijomclgjgif)

<!-- more -->

## 配置

1.启动
whistle 支持三种命令 `whistle`、`w2`、`wproxy`, 效果是相同的.

```bash
# 默认启动
w2 start
# 指定端口启动
w2 start -p 8080
```

2.Chrome 浏览器 Proxy SwitchyOmega 配置

新建情景模式, 选择代理服务器
![选择代理服务器](/images/article/1075711.png)

填写 whistle 启动启动时的端口
![](/images/article/48036690.png)


3.查看网络请求

在 http://local.whistlejs.com/#network 监听, 打开其他网页后查看请求

![查看请求效果](/images/article/74710244.png)

## 使用

### 配置常用规则

```bash
# 转发请求
127.0.0.1 so.com

# 请求头添加 client
*.so.com reqHeaders://(client=username)

# 本地文件映射
so.com/test.json file:///Users/haipingxiao/test.json


```

### HTTPS

https 的抓包需要安装证书后使用.
点击顶部 Help-HTTPS 可以查看安装说明, 在安卓端安装证书遇到的坑:
Q:连上代理后无法访问地址 `rootca.pro`
A:使用 ip 地址连接, 配置 `rootca.pro` 的代理

Q:系统自带浏览器无法下载
A:使用 chrome

Q:下载证书后无法安装
A:在系统自带的文件管理器中,找到证书文件手动安装

### 导入 `fiddler` 的抓包请求
有时候测试同学会发来一个后缀是 `saz` 的抓包文件, 该文件是通过 fiddler 导出请求. whistle 也支持该格式的导入导出, 使用顶部的 `Import` 和 `Export` 即可.

## 其他资源

[官方文档](http://wproxy.org/whistle/)
