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
