---
title: CSS 工具箱
date: 2016-12-16 13:53:29
categories: 杂物间
toc: true
tags:
  - CSS
---

## 工具网站：
综合：
1. [MDN](https://developer.mozilla.org/zh-CN/)
2. [W3Schools](http://www.w3schools.com/)

查询兼容性：
1. [Can i use](http://caniuse.com/)

动画：
1. [Animate.css](https://daneden.github.io/animate.css/)
2. [cssanimate](http://cssanimate.com/)

CSS3 generator:
1. http://www.css3generator.in/
2. http://css3generator.com/
3. http://css3.me/


## 垂直居中
```css
.vertical-center {
    position: absolute;;
    top: 50%;
    transform: translateY(-50%);
}
```

## 水平居中

block 元素：
```css
/* 方法一 */
.block {
    margin: 0 auto;
}
/* 方法二 */
.center {
    position: absolute;;
    left: 50%;
    transform: translateX(-50%);
}

```

inline-block 和 inline 元素设置父元素的 text-align
```css

.container {
    text-align: center;
}

```

## 消除 inline-block 元素之间的间隙
```css
/* 设置父元素的 font-size */
.modal {
    font-size: 0;
}
```

## margin 的缩写
有4 2 3个值时对应关系，padding 类似
```
margin: top  right  bottom  left
margin: (top/bottom)  (right/left)
margin: top  (right/left)  bottom
```
备注：元素之间的 margin 会重叠

## 圆形头像
```
border-radius: 50%;
```
备注： outline 属性与 border 类似，但是不改变页面布局，仅作查看效果。
