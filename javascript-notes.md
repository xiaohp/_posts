---
title: Javascript 踩坑笔记
date: 2017-03-16 14:10:29
categories: 笔记本
toc: true
tags:
  - Javascript
---

自定义 `log` 函数，可以方便的进行调试

```javascript
var log = function() {
    console.log.apply(console, arguments)
}

// var log = console.log.bind(console)
```

利用 `typeof` 来检查一个没有声明的变量，而不报错。

```javascript
// 错误的写法
if (v) {
  // ...
}
// ReferenceError: v is not defined

// 正确的写法
if (typeof v === "undefined") {
  // ...
}
```

<!-- more -->

利用 `window` 对象的属性来检查全局变量是否声明

```javascript
if ('a' in window) {
  // 变量 a 声明过
} else {
  // 变量 a 未声明
}
```

利用 `setTimeout` 实现异步

```javascript
var a = function () {
    console.log('begin')
    setTimeout(function () {
        console.log('function 1')
    }, 0)
    setTimeout(function () {
        console.log('function 2')
    }, 0)
    console.log('end')
}

a()

// begin
// end
// function 1
// function 2
```

利用 `Object` 的 `key` 不重复特性给数组去重

```javascript
var deduplication = function(array) {
    var o ={}
    for (let a of array) {
        o[a] = 1
    }
    return Object.keys(o)
}
var a = [1, 2, 2, 5, 2, 1]

deduplication(a)
// [1, 2, 5]
```

利用 `ES6` 的 `set` 进行数组去重

```javascript
// 方法一
var unique = function(array) {
  return Array.from(new Set(array))
}
// 方法二
var unique = function(array) {
  return [...new Set(array)]
}
```

利用 `JSON` 深度复制对象
对象和数组为引用类型，不能直接赋值

```javascript
var copy_object = function(obj) {
    return JSON.parse(JSON.stringify(obj))
}
```

设置 `iframe` 内容为指定 `HTML` 字符串

```javascript
var iframe = document.querySelector('#iframe')
// 方法一
iframe.contentWindow.document.write(data.html)
// 此方法为叠加的方式，若需要刷新，则需要在之前运行
// iframe.src = "about:blank"

// 方法二
iframe.src = "data:text/html;charset=utf-8," + escape(data.html)
```

`window.open` 打开的窗口被浏览器后屏蔽的解决方案

在 `AJAX` 之前调用 `window.open` 并保存该窗口
在回调函数中设置该窗口的 `location` 属性
```javascript
var newWindow = window.open()
newWindow.location = url
```

## 踩坑记录

1. Array.prototype.includes() 在360浏览器中不兼容，查询后需要47以上版本的chrome才支持。`String` 和 `Array`的`includes`方法，是 ES6 加入的内容。
2. 通过代码添加的自定义 data 不会在开发者工具中显示
3. jQuery 获取元素自定义 data, 如果是数字会自动转成 Number
