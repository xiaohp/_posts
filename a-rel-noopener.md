---
title: 通过 a 标签在新页面打开链接时使用rel=noopener
date: 2018-12-25 16:13:29
categories: 笔记本
toc: true
tags:
  - HTML
  - Web
---

通过 `Vue CLI` 生成项目后, 发现组件链接中的 `a` 标签有个属性 `rel=noopener`

```html
<a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a>
```

这里是为了安全性考虑, 如果没有使用这个属性, 新页面可以通过 `window.opener` 访问当前页面对象, 可以使用 `window.opener.location = newURL` 将当前页面导航到其他地址.
所以在通过 `a` 标签在新页面打开链接时, 建议都使用 `rel=noopener` .

参考链接：
- [网站使用 rel="noopener" 打开外部锚](https://developers.google.com/web/tools/lighthouse/audits/noopener)
- [About rel=noopener](https://mathiasbynens.github.io/rel-noopener/)
