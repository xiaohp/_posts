---
title: Javascript 工具函数封装
date: 2017-02-20 14:10:29
categories: 笔记本
toc: true
tags:
  - Javascript
  - jQuery
---

自定义 `log` 函数

```javascript
var log = function() {
    console.log.apply(console, arguments)
}

// var log = console.log.bind(console)
```


选择器封装，类似 jQuery 中的 $

```javascript
var e = function(selector) {
    return document.querySelector(selector)
}
var es = function(selector) {
    return document.querySelectorAll(selector)
}

```

<!-- more -->

查找 element 的所有子元素

```javascript
var find = function(element, selector) {
    return element.querySelector(selector)
}
// 在原生对象上部署此方法
// Element.prototype.find = Element.prototype.querySelector
```

添加 HTML 到指定元素后面

```javascript
var appendHtml = function(element, html) {
	element.insertAdjacentHTML('beforeend', html)
}
```
添加 HTML 到指定元素开头

```javascript
var prependHtml = function(element, html) {
	element.insertAdjacentHTML('afterbegin', html)
}
```

绑定事件

```javascript
var bindEvent = function(element, eventName, callback) {
    element.addEventListener(eventName, callback)
}
// 在原生对象上部署此方法
// Element.prototype.on = Element.prototype.addEventListener
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

添加 class

```javascript
var addClass = function(element, className) {
    element.classList.add(className)
}
```
删除 class

```javascript
var removeClass = function(element, className) {
    element.classList.remove(className)
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

切换元素显示和隐藏
```javascript
var show = function(element) {
    element.classList.add('hide')
}
var hide = function(element) {
    element.classList.remove('hide')
}
```

设置元素内容
```javascript
var setText = function(element, text) {
    element.textContent = text
}
var setHtml = function(element, html) {
    element.innerHTML = html
}
var setValue = function(element, value) {
    element.value = value
}
```

自定义属性操作
```javascript
// 获取自定义属性
var getData = function(element, property) {
    return element.dataset.property
}
var setData = function(element, property, value) {
    element.dataset.property = value
}
```
AJAX
```javascript
var ajax = function(method, path, data, reseponseCallback) {
    var r = new XMLHttpRequest()
    r.open(method, path, true)
    r.setRequestHeader('Content-Type', 'application/json')
    r.onreadystatechange = function() {
        if(r.readyState === 4) {
            reseponseCallback(r)
        }
    }
    r.send(data)
}
```
