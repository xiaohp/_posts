---
title: Javascript 实现 jQuery API
date: 2017-02-20 14:10:29
categories: 杂物间
toc: true
tags:
  - Javascript
---

选择器封装，类似 jQuery 中的 $

```javascript
var e = function(selector) {
    return document.querySelector(selector)
}
```
查找 element 的所有子元素

```javascript
var find = function(element, selector) {
    return element.querySelector(selector)
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
    element.innerText = text
}
var setHtml = function(element, html) {
    element.innerHtml = html
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
