---
title: CSS 工具箱
date: 2016-12-16 13:53:29
categories: 笔记本
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

<!-- more -->

## 水平居中

```css
/* block 元素： */
/* 方法一 */
.block {
    margin: 0 auto;
    width: 200px;
}

/* 方法二 */
.center {
    position: absolute;;
    left: 50%;
    transform: translateX(-50%);
}

/* 方法三 flex */
.container {
    display: flex;
    justify-content: center;
}

/* inline-block 和 inline 元素设置父元素的 text-align */
.container {
    text-align: center;
}
```


## 水平垂直居中
方法一：`absolute`
CSS
```css
.absolute-box {
    position: relative;
}
.absolute-box .content {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
}
```
HTML
```html
<div class="container absolute-box">
    <div class="content">
        水平垂直居中
    </div>
</div>
```
方法二：`flex`
CSS
```css
.container {
    width: 400px;
    height: 200px;
    background-color: #ccc;
    margin: 20px;
}
.flex-box {
    display: flex;
    align-items: center;
    justify-content: center;
}
```
HTML
```html
<div class="container flex-box">
    <div class="content">
        水平垂直居中
    </div>
</div>
```


## 消除 inline-block 元素之间的间隙
```css
/* 设置父元素的 font-size */
.modal {
    font-size: 0;
}
```


## margin 的缩写
有2、3、4个值时对应关系，padding 类似
```css
div {
    margin: top  right  bottom  left;
    margin: (top/bottom)  (right/left);
    margin: top  (right/left)  bottom;
}
```
备注：块级元素之间的 margin 在垂直方向会重叠，参见 `外边距合并 margin collapsing`


## 圆形头像
```css
.portrait {
    border-radius: 50%;
}
```


## 文本溢出显示省略号
单行文本
```css
.text {
    overflow: hidden;
    text-overflow:ellipsis;
    white-space: nowrap;
}
```


## 多行文本在最后一行溢出显示省略号
```css
.text {
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;
    overflow: hidden;
}
```


## CSS 阴影效果被挡住问题
```css
.shadow {
    position: relative;
    box-shadow: 0 0 20px 0px #000000;
    z-index: 2;
}
```


## img map 链接点击时不显示 outline
HTML
```html
<img class="map" src="..." usemap="...">
```
CSS
```css
img[usemap], map area{
    outline: none;
}
```
备注： outline 属性与 border 类似，但是不改变页面布局，仅作查看效果。


## 文字和数字混排时强制换行，默认数字会连在一起
```css
.content {
    word-break: break-all;

}
```


## 外边距合并 margin collapsing
方向：与当前的渲染方向垂直。比如正常情况下竖直方向会发生，修改 writing-mode 属性更改方向后，改为在水平方向发生。
仅在 BFC 中发生。display 属性设置为 inline-block 时为 IFC，不会发生外边距合并


## BFC 与 IFC 是什么
FC（Formatting Contexts） 是 W3C 规范中的概念，表示页面中的一块渲染区域，有一套自己的规则决定了子元素如何定位，以及和其他元素的影响。
CSS 2.1 中规定了 `BFC` 和 `IFC` 两种类型。CSS3 新增了 `GFC` 和 `FFC` 两种类型。

BFC(Block Formatting Contexts) 是竖着排块级盒子的上下文，一个名词。对应 `display: block;`

IFC(Inline Formatting Contexts) 是行内元素排列的上下文。`display: inline-block;`
GFC(GridLayout Formatting Contexts)对应 `display: grid;`
FFC(Flex Formatting Contexts) 对应 `display: flex;`
