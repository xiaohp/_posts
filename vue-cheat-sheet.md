---
title: Vue 备忘录
date: 2018-11-26 21:35:29
categories: 笔记本
toc: true
tags:
  - Javascript
  - Vue
---

最近换到新项目开始使用 `Vue` 了.记录一些经常搞混的内容:

## 指令

```html
<!-- v-bind 缩写 -->
<a v-bind:href="url">...</a>
<a :href="url">...</a>

<!-- v-on 缩写 -->
<a v-on:click="doSomething">...</a>
<a @click="doSomething">...</a>

<!-- class 绑定 -->
<div v-bind:class="{ active: isActive }"></div>

<!-- 条件渲染 -->
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>

 <!-- 背景图片绑定 -->
<div class="main" :style="{backgroundImage: 'url(' + src + ')'}">
    <div class="text-center">
        奖励
    </div>
</div>
```

<!-- more -->

## Prop

Prop 验证 与默认值

```js
Vue.component('my-component', {
  props: {
    // 基础的类型检查 (`null` 匹配任何类型)
    propA: Number,
    // 多个可能的类型
    propB: [String, Number],
    // 必填的字符串
    propC: {
      type: String,
      required: true
    },
    // 带有默认值的数字
    propD: {
      type: Number,
      default: 100
    },
    // 带有默认值的对象
    propE: {
      type: Object,
      // 对象或数组默认值必须从一个工厂函数获取
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
    }
  }
})
```
