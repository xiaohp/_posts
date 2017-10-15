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
运行初始化命令，会在该目录下，新建一个`package.json`文件。
添加 `-y` 意味着文件使用默认配置，不添加会在终端问多个问题。

```shell
$ npm init -y
```

<!-- more -->

添加依赖

```shell
$ npm install gulp --save
```

会在项目中添加依赖并放在`node_modules`文件夹中，上传到代码仓库时需要将此文件添加到 `ignore`
使用者运行前安装依赖即可

```shell
$ npm install
```

常用操作可以放在`package.json`文件中：

```javascript
{
  // ...
  "scripts": {
    "dev": "node app.js",
    // 'build': ...,
    // 'lint': ...,
  }
}
```

在终端中通过以下命令运行，相当于 `node app.js` 的快捷方式。

```shell
npm run dev

```
