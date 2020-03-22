---
title: Vue 组件通信的几种方式
date: 2020-03-22 16:13:29
categories: 笔记本
toc: true
tags:
  - Vue.js
---

## Prop 和 事件回调
父组件通过 `prop` 向子组件传递数据

```html
<post title="hello"></post>
```

子组件通过自定义事件向父组件传递数据
<!-- more -->
```html
<!-- 子组件触发 -->
<button v-on:click="$emit('hello')">
    Click me to be welcomed
</button>
<!-- 父组件监听 -->
<example v-on:hello="world"></example>
```

## Vuex
复杂项目可以使用 [Vuex](https://vuex.vuejs.org/zh/) 进行状态管理，配合 [vue-devtools](https://github.com/vuejs/vue-devtools) 能够更好的追踪状态。

## 单独的事件管理中心 EventBus
单独使用一个 Vue 实例来管理事件 [文档的例子](https://cn.vuejs.org/v2/guide/migration.html#dispatch-%E5%92%8C-broadcast-%E6%9B%BF%E6%8D%A2)，但是在复杂的场景下，事件的触发和监听可能散落在各个地方，不利于维护，更推荐使用 `Vuex`。

## 依赖注入 `provide` 和 `inject`
类似 `React` 里面的 `context`，相当于大范围有效的 prop。[文档的例子](https://cn.vuejs.org/v2/guide/components-edge-cases.html#%E4%BE%9D%E8%B5%96%E6%B3%A8%E5%85%A5) ，在项目中使用不多。

## 访问组件实例
`$root` 属性用来从一个子组件访问根组件的实例，`$parent` 属性访问父组件的实例。不利于组件解耦，不推荐使用。

## 总结

| 方案 | 适用场景 | 是否推荐使用 |
| :----: | :----: | :----: |
| Prop | 父子组件 | 推荐 |
| Vuex | 单元格 | 推荐 |
| EventBus | 任意组件之间 | 复杂项目不推荐 |
| 依赖注入 | 子孙组件之间 | 复杂项目不推荐 |
