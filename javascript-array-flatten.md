---
title: Javascript 拍平数组的 N 种方法
date: 2017-07-08 23:10:29
categories: 笔记本
toc: true
tags:
  - Javascript
---

## flatten one level

方法一 利用 `for` 循环处理
```javascript
var flatten = function(array) {
    var res = []
    for (var i = 0; i < array.length; i++) {
        var a = array[i]
        if (Array.isArray(a)) {
            for (var j = 0; j < a.length; j++) {
                var b = a[j]
                res.push(b)
            }
        } else {
            res.push(a)
        }
    }
    return res
}

flatten([1, [2, [3, [4]], 5]]) // => [1, 2, [3, [4]], 5]
```

方法二 利用数组的 `reduce` 方法
```javascript
var flatten = function(array) {
    var res = array.reduce(function(a, b) {
        return a.concat(b)
    }, [])
    return res
}

flatten([1, [2, [3, [4]], 5]]) // => [1, 2, [3, [4]], 5]
```

方法三 用 ES6 改写方法二
```javascript
const flatten = list => list.reduce(
    (a, b) => a.concat(b), []
)

flatten([1, [2, [3, [4]], 5]]) // => [1, 2, [3, [4]], 5]
```

方法四 利用数组的 `concat` 方法
```javascript
var flatten = function(array) {
    return Array.prototype.concat(...array)
}

flatten([1, [2, [3, [4]], 5]]) // => [1, 2, [3, [4]], 5]
```

## flatten deep
递归调用方法三
```javascript
const flatten_deep = list => list.reduce(
    (a, b) => a.concat(Array.isArray(b) ? flatten_deep(b) : b), []
)

flatten_deep([1, [2, [3, [4]], 5]]) // => [1, 2, 3, 4, 5]
```
