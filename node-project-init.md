---
title: node 项目初始化
date: 2017-05-16 14:10:29
categories: 笔记本
toc: true
tags:
  - Javascript
  - node
---

新建一个目录
```shell
$ mkdir app-demo
$ cd app-demo
```

在该目录下，新建一个`package.json`文件
```shell
$ npm init -y
```

添加依赖
```shell
$ npm install gulp --save
```

会在项目中添加依赖并放在`node_modules`文件夹中，上传到代码仓库时需要将此文件添加到 `ignore`
使用者运行前安装依赖即可
```shell
$ npm install
```
