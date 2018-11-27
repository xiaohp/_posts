---
title: Hexo 工具箱
date: 2017-01-05 23:05:29
categories: 笔记本
toc: true
tags:
  - Hexo
  - Blog
---


[官方文档](https://hexo.io/zh-cn/docs/)

### 添加新文章

``` bash
$ hexo new "My New Post"
```

test
更多信息: [Writing](https://hexo.io/docs/writing.html)

### 开启服务器

``` bash
$ hexo server
```
默认端口4000，如果打不开可能端口冲突（比如在我的电脑上这个端口被福昕阅读器占用），可手动指定其他端口
``` bash
$ hexo server -p 5000

```

<!-- more -->

更多信息: [Server](https://hexo.io/docs/server.html)

### 生成静态文件

``` bash
$ hexo generate
```

更多信息: [Generating](https://hexo.io/docs/generating.html)

### 部署网站，更新到远端

``` bash
$ hexo deploy
```

更多信息: [Deployment](https://hexo.io/docs/deployment.html)

javascript 代码显示效果
``` javascript
var log = function() {
    console.log.apply(console, arguments)
}
```
### 清除缓存文件
``` bash
$ hexo clean
```
