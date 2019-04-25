---
title: Flexbox 布局笔记
date: 2019-03-14 20:05:29
categories: 笔记本
toc: true
tags:
  - Flex
  - CSS
---

最近编写移动端布局需要使用 `Flexbox` 布局, 重新复习一遍.

## 容器属性

在父元素设置 `flex` 布局:

```css
.flex-container {
    display: flex;
}
```

设置容器方向:

```css
.flex-container {
    flex-direction: row;
}
```

<!-- more -->

设置项目换行:

```css
.flex-container {
    flex-wrap: wrap;
}
```

以上两项可以缩写:

```css
.flex-container {
    flex-flow: row wrap;
}
```

主轴方向对齐方式:

```css
.flex-container {
    justify-content: flex-start;
}
```

交叉轴对齐方式:

```css
.flex-container {
    align-items: center;
}
```

多行时在交叉轴的对齐方式:

```css
.flex-container {
    align-content: stretch;
}
```

## 项目属性

控制项目排列顺序:

```css
.flex-item {
    order: 1;
}
```

项目的放大比例:

```css
.flex-item {
    flex-grow: 2;
}
```

项目的缩小比例:

```css
.flex-item {
    flex-shrink: 0;
}
```

项目的初始尺寸:

```css
.flex-item {
    flex-basis: 200px;
}
```

以上 3 项的缩写:

```css
.flex-item {
    flex: 1 1 200px;
}
```

设置项目自身的对齐方式, 覆盖默认对齐方式:

```css
.flex-item {
    align-self: center;
}
```

参考链接：
[图解CSS3 Flexbox属性](https://www.w3cplus.com/css3/a-visual-guide-to-css3-flexbox-properties.html)
[Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
[Flex 布局教程：实例篇](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)
