---
title: 原生 Javascript 与 jQuery API 对照
date: 2017-04-20 14:10:29
categories: 笔记本
toc: true
tags:
  - Javascript
  - jQuery
---

## 选择器

通用选择
```javascript
// jQuery
$('selector')

// Native
document.querySelector('selector')

document.querySelectorAll('selector')
// return NodeList
```

后代选择
```javascript
// jQuery
$el.find('li')

// Native
el.querySelectorAll('li')
```

<!-- more -->

前后元素
```javascript
// jQuery
$el.prev()

// Native
el.previousElementSibling

// next
$el.next()

// Native
el.nextElementSibling
```

父元素
```javascript
// jQuery
$el.parent()

// Native
el.parentNode
```

closest 最接近的祖先元素
```javascript
// jQuery
$el.closest(selector)

// Native
el.closest(selector)
// 原生方法不兼容 IE, chrome 浏览器仅 41 版本以上支持
```

## 获取值和属性操作

获取值
```javascript
// jQuery
$('#my-input').val()

// Native
document.querySelector('#my-input').value
```

获取属性
```javascript
// jQuery
$el.attr('foo')

// Native
el.getAttribute('foo')
```

设置属性
```javascript
// jQuery
$el.attr('foo', 'bar')

// Native
el.setAttribute('foo', 'bar')
```

获取和设置 `data` 属性
```javascript
// jQuery
$el.data('foo')
$el.data('foo', value)

// Native
el.dataset['foo']
el.dataset.foo
el.dataset['foo'] = value
```

## class 操作

添加 class
```javascript
// jQuery
$el.addClass(className)

// Native
el.classList.add(className)
```

移除 class
```javascript
// jQuery
$el.removeClass(className)

// Native
el.classList.remove(className)
```

切换 class
```javascript
// jQuery
$el.toggleClass(className)

// Native
el.classList.toggle(className)
```

判断拥有 class
```javascript
// jQuery
$el.hasClass(className)

// Native
el.classList.contains(className)
```

## 操作 DOM

移除元素
```javascript
// jQuery
$el.remove()

// Native
el.remove()
```

获取 text
```javascript
// jQuery
$el.text()

// Native
el.textContent
```

设置 text
```javascript
// jQuery
$el.text(string)

// Native
el.textContent = string
```

获取 HTML
```javascript
// jQuery
$el.html()

// Native
el.innerHTML
```

设置 HTML
```javascript
// jQuery
$el.html(htmlString)

// Native
el.innerHTML = htmlString
```

append 添加元素到末尾
```javascript
// jQuery
$el.append("<div id='container'>hello</div>")

// Native (HTML string)
el.insertAdjacentHTML('beforeend', '<div id="container">Hello World</div>')

// Native (Element)
el.appendChild(newEl)
```

prepend 添加元素到开头
```javascript
// jQuery
$el.prepend("<div id='container'>hello</div>")

// Native (HTML string)
el.insertAdjacentHTML('afterbegin', '<div id="container">Hello World</div>')

// Native (Element)
el.insertBefore(newEl, el.firstChild)
```

insertBefore 添加到指定元素前
```javascript
// jQuery
$newEl.insertBefore(queryString);

// Native (HTML string)
el.insertAdjacentHTML('beforebegin ', '<div id="container">Hello World</div>')

// Native (Element)
const el = document.querySelector(selector)
el.parentNode.insertBefore(newEl, el)
```

insertAfter 添加到指定元素后
```javascript
// jQuery
$newEl.insertAfter(queryString)

// Native (HTML string)
el.insertAdjacentHTML('afterend', '<div id="container">Hello World</div>')

// Native (Element)
const el = document.querySelector(selector)
el.parentNode.insertBefore(newEl, el.nextSibling)
```

移除子元素
```javascript
// jQuery
$el.empty()

// Native
el.innerHTML = ''
```

## 事件

绑定事件
```javascript
// jQuery
$el.on(eventName, eventHandler)

// Native
el.addEventListener(eventName, eventHandler)
```

解绑事件
```javascript
// jQuery
$el.off(eventName, eventHandler)

// Native
el.removeEventListener(eventName, eventHandler)
```

触发事件
```javascript
// jQuery
$el.trigger(eventName)

// Native
var event = new Event(eventName)
el.dispatchEvent(event)
```

## 工具

isArray 判断数组
```javascript
// jQuery
$.isArray(range)

// Native
Array.isArray(range)
```

inArray 判断数组包含
```javascript
// jQuery
$.inArray(item, array)

// Native
array.indexOf(item) > -1

// ES6
array.includes(item)
```

extend 扩展对象
```javascript
// jQuery
$.extend({}, defaultOpts, opts)

// Native
Object.assign({}, defaultOpts, opts)
```

trim 去除字符串首尾空白
```javascript
// jQuery
$.trim(string)

// Native
string.trim()
```

map 根据数组内容生成新数组
```javascript
// jQuery
$.map(array, (value, index) => {
})

// Native
array.map((value, index) => {
})
```

each 遍历对象和数组
```javascript
// jQuery
$.each(array, (index, value) => {
})

// Native
array.forEach((value, index) => {
})
```

等待 DOM 加载完执行操作
```javascript
// jQuery
$(document).ready(function() {
})

// Native
window.onload = function() {
}

document.addEventListener("DOMContentLoaded", function(event) {
    console.log("DOM fully loaded and parsed")
})
```

## API 分析
在 [jQuery](https://api.jquery.com/jQuery/) 官网上，核心函数 jQuery() 有 9 种用法
```javascript
jQuery(selector [, context])
jQuery(element)
jQuery(elementArray)
jQuery(object)
jQuery(jQuery object)
jQuery()
jQuery(html [, ownerDocument])
jQuery(html, attributes)
jQuery(callback)
```
一个函数如此多的用法，通过参数类型进行判断，显然设计得不好。前 3 个 API 是可以使用的，主要是第一个。
并不是提供的方法都要去用，取其精华，去其糟粕即可。
