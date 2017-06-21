---
title: Javascript 常用函数封装
date: 2017-01-16 14:10:29
categories: 杂物间
toc: true
tags:
  - Javascript
---



自定义 log 函数

```javascript
var log = function() {
    console.log.apply(console, arguments)
}
```

选择器封装，类似 jQuery 中的 $

```javascript
var e = function(selector) {
    return document.querySelector(selector)
}
```

添加 HTML 到指定元素后面

```javascript
var appendHtml = function(element, html) {
	element.insertAdjacentHTML('beforeend', html)
}
```

绑定事件

```javascript
var bindEvent = function(element, eventName, callback) {
    element.addEventListener(eventName, callback)
}
```
给多个元素绑定事件

```javascript
var bindAll = function(selector, eventName, callback) {
    var elements = document.querySelectorAll(selector)
    for(var i = 0; i < elements.length; i++) {
        var e = elements[i]
        bindEvent(e, eventName, callback)
    }
}
```

切换 class

```javascript
var toggleClass = function(element, className) {
    if (element.classList.contains(className)) {
        element.classList.remove(className)
    } else {
        element.classList.add(className)
    }
}
```

删除拥有某个 class 的所有元素

```javascript
var removeClassAll = function(className) {
    var selector = '.' + className
    var elements = document.querySelectorAll(selector)
    for (var i = 0; i < elements.length; i++) {
        var e = elements[i]
        e.classList.remove(className)
    }
}
```

批量删除元素

```javascript
var removeAll = function(selector) {
    var tags = document.querySelectorAll(selector)
    for (var i = 0; i < tags.length; i++) {
        var tag = tags[i]
        tag.remove()
    }
}
```

查找 element 的所有子元素

```javascript
var find = function(element, selector) {
    return element.querySelector(selector)
}
```

利用 typeof 来检查一个没有声明的变量，而不报错。

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
利用 setTimeout 实现异步

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

利用 Object 的 key 不重复特性给数组去重

```javascript
var deduplication = function (list) {
    var o ={}
    for (let l of list) {
        o[l] = 1
    }
    return Object.keys(o)
}
var a = [1, 2, 2, 5, 2, 1]

deduplication(a)
// [1, 2, 5]
```

利用 ES6 的 set 进行数组去重

```javascript
function unique (arr) {
  return Array.from(new Set(arr))
}
```

## 踩坑记录

1. Array.prototype.includes() 在360浏览器中不兼容，查询后需要47以上版本的chrome才支持
2. 通过代码添加的自定义 data 不会在开发者工具中显示
3. jQuery 获取自定义 data, 如果是数字会自动转成 Number
