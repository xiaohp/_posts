---
title: HTTP 请求头中的 Content-Type 设置与解析
date: 2017-10-24 09:13:29
categories: 笔记本
toc: true
tags:
  - Javascript
  - HTTP
---

前端通过 `AJAX` 发送数据时，设置的 `HTTP` 请求头一般有两种。分别是 `application/x-www-form-urlencoded` 和 `application/json`。区别在于发送数据时的编码方式，对应的解析方法自然也不同。

## application/x-www-form-urlencoded

这种方式把数据编码成 URL 中参数的形式，键值之间通过 `=` 分隔，键值对之间通过 `&` 分隔。

<!-- more -->

### 设置

若是使用 jQuery 的 `AJAX`，请求头默认设置为这种。若传入的数据是 Object 对象键值对，也会进行自动编码。

### 解析
以 `Node.js` 常用的 Web 框架 `express` 为例，通过 `body-parser` 这个模块解析请求中的 body:

```javascript
const express = require('express')
const bodyParser = require('body-parser')

const app = express()
app.use(bodyParser.urlencoded({
	extended: true,
}))
```

## application/json

### 设置
直接在 `AJAX` 中设置请求头：

```javascript
var ajax = function(method, path, data, reseponseCallback) {
    var r = new XMLHttpRequest()
    r.open(method, path, true)
    r.setRequestHeader('Content-Type', 'application/json')
    r.onreadystatechange = function() {
        if(r.readyState === 4) {
            var res = JSON.parse(r.response)
            reseponseCallback(res)
        }
    }
    data = JSON.stringify(data)
    r.send(data)
}
```

这里把发送数据的序列化和反序列化过程都封装在 `AJAX` 中，使用时直接使用数据。

### 解析
同样使用 `body-parser` 这个库，设置的解析方式有所不同：

```javascript
const express = require('express')
const bodyParser = require('body-parser')

const app = express()
app.use(bodyParser.json())
```

在 `express` 中，数据是通过中间件的形式逐级处理。若需同时使用两种请求头（比如旧项目中有通过 form 表单提交的请求，需要兼容），对 `express` 实例应用两种设置处理即可。
