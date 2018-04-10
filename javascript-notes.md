---
title: Javascript 踩坑笔记
date: 2017-03-16 14:10:29
categories: 笔记本
toc: true
tags:
  - Javascript
---

## 自定义 `log` 函数，可以方便的进行调试

```javascript
var log = function() {
    console.log.apply(console, arguments)
}

// var log = console.log.bind(console, 'debug --')
```

## 利用 `typeof` 来检查一个没有声明的变量，而不报错。

```javascript
// 错误的写法
if (v) {
  // ...
}
// ReferenceError: v is not defined

// 正确的写法
if (typeof v === 'undefined') {
  // ...
}
```

<!-- more -->

## 利用 `window` 对象的属性来检查全局变量是否声明
备注：`var` 和`function`声明的全局变量，是顶层对象的属性。ES6 中，`let`、`const`、`class`声明的全局变量，不属于顶层对象的属性。从 ES6 开始，全局变量将逐步与顶层对象的属性脱钩。
```javascript
if ('a' in window) {
  // 变量 a 声明过
} else {
  // 变量 a 未声明
}
```

## 利用 `setTimeout` 实现异步

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

## 利用 `Object` 的 `key` 不重复特性给数组去重
备注：`Object.keys` 的结果不保证顺序，如对顺序有要求，需要使用其他方法
```javascript
var deduplication = function(array) {
    var o = {}
    for (let a of array) {
        o[a] = 1
    }
    return Object.keys(o)
}
var a = [1, 2, 2, 5, 2, 1]

deduplication(a)
// [1, 2, 5]
```

## 利用 `ES6` 的 `set` 进行数组去重
备注：若有多个相同的值，会保留第一个
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

## 数组去重，多个相同的值，保留最后一个
备注：这个需求需要手动处理
```javascript
var unique = function(array) {
    var res = []
    array.forEach(e => {
        if (res.includes(e)) {
            removeElement(res, e)
        }
        res.push(e)
    })
    return res
}
// 辅助函数，根据数组元素删除元素
var removeElement = function(array, el) {
    var index = array.indexOf(el)
    if (index > -1) {
        array.splice(index, 1)
    }
    return array
}
// 辅助测试
var ensure = function(a, b, msg) {
    if (JSON.stringify(a) !== JSON.stringify(b)) {
        console.log('test error', `${a} 不等于 ${b}, ${msg}`)
    } else {
        console.log('test success', `${msg}`)
    }
}
// 测试函数
var test = function() {
    var a = [5, 2, 1, 3, 4, 3, 1]
    var b = [5, 2, 4, 3, 1]
    ensure(unique(a), b, 'test unique')
}

test()
// test success test unique
```

## 利用 `JSON` 深度复制对象
对象和数组为引用类型，不能直接赋值

```javascript
var copyObject = function(obj) {
    return JSON.parse(JSON.stringify(obj))
}
```

## 设置 `iframe` 内容为指定 `HTML` 字符串

```javascript
var iframe = document.querySelector('#iframe')

// 此方法为叠加的方式，若需要刷新，则需要在之前设置 src 为空
iframe.src = "about:blank"
iframe.contentWindow.document.write(data.html)
// jQuery 修改 iframe 内部样式
$(iframe).contents().find('body').css('zoom', '0.5')
// 设置完内容需要关闭，否则一直在 loading
iframe.contentWindow.document.close()
```

## `window.open` 打开的窗口被浏览器后屏蔽的解决方案

在 `AJAX` 之前调用 `window.open` 并保存该窗口
在回调函数中设置该窗口的 `location` 属性
如果用户浏览器开启了拦截，则用户点击页面后，1s内打开新窗口有效，1s后会被拦截。所以需要在 ajax 之前打开窗口

```javascript
var newWindow = window.open()
newWindow.location = url
```

## jQuery AJAX 序列化表单添加参数
当 AJAX 请求头中的 `Content-Type` 字段设置为 `application/x-www-form-urlencoded; charset=utf-8`时，可以通过

```javascript
$("#form").serialize()
```

的方式序列化数据，传入 AJAX 进行提交。
这种方法的缺点在于只能提交简单数据，如包含数组则无法直接使用。
如果需要添加数组数据，需要额外添加：

```javascript
var data = $("#form").serialize()
var other_data = {
    num_iid: item_array,
    wireless_index_num_iid: wireless_index_num_iid,
}
data = data + '&' + decodeURIComponent($.param(other_data))
```

## jQuery 表单操作

```javascript
// 获取单选框的值：
$('input[name=img-detail]:checked').val()

// 设置单选框选中
 $('input:radio[name=img-detail]').filter('[value=1]').prop('checked', true)

// 禁用页面按钮，可在 button 使用；
$('.update-many').prop('disabled', true)
$('.update-many').prop('disabled', e => num < 1)

```

## Node.js base64 加密与解密：
[官方文档](https://nodejs.org/docs/latest/api/buffer.html#buffer_buffers_and_character_encodings)
```javascript
// base 64 加密：
Buffer.from('hello world', 'ascii').toString('base64')

// base 64 解密：
Buffer.from('aGVsbG8gd29ybGQ=', 'base64').toString()

```

## 利用 `storage` 事件来跨页面通信时，只能使用 localStorage
```javascript
// 事件监听
window.addEventListener("storage", function(e) {
    console.log('event', e)
})
// jQuery 的事件需要额外处理
$(window).on('storage', function(e){
    console.log('event', e)
    console.log('originalEvent', e.originalEvent)
})

```

## 关闭页面弹出提示
```javascript
var confirmTip = true
$(window).on('beforeunload', e => {
    if (confirmTip) {
        event.returnValue = '未保存设置，是否离开页面？'
    }
})

```


## 踩坑记录

1. Array.prototype.includes() 在360浏览器中不兼容，需要chrome 版本在 47 以上。`String` 和 `Array`的`includes`方法，是 ES6 加入的内容
2. 通过代码添加的自定义 data 不会在开发者工具中显示
3. jQuery 获取元素自定义 data, 如果是数字会自动转成 Number, 如果是 `true` 一也会自动转换为布尔值
4. 原生 DOM 方法 Element.closest() 在低版本 chrome 中不兼容。可以使用 jQuery 代替
