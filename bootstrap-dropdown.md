---
title: Bootstrap 下拉菜单实现自适应
date: 2017-08-10 16:13:29
categories: 笔记本
toc: true
tags:
  - Javascript
  - Bootstrap
---

`Bootstrap`的下拉菜单有时会用在列表中，若菜单在页面底部，且选项较多时，会产生溢出。

![问题图](http://oih6hf7qs.bkt.clouddn.com/blog/20170810-164757127.png)

比较理想的做法是类似浏览器中的右键菜单，根据不同位置实现不同的展开方向。

![浏览器图](http://oih6hf7qs.bkt.clouddn.com/blog/20170810-164849596.png)

官方文档只提供了向下展开的方法，没有向上展开的选项。
查阅信息后发现其实有预留一个接口，通过添加 `dropup` 的class来实现。
HTML代码如下

```html
<div class="dropdown">
    <button id="dLabel" type="button" class="btn" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
        点击展开菜单
        <span class="caret"></span>
     </button>
    <ul class="dropdown-menu" role="menu" aria-labelledby="dLabel">
        <li role="presentation">
            <a role="menuitem" tabindex="-1" href="">菜单第1项</a>
        </li>
        <li role="presentation" class="divider"></li>
        <li role="presentation">
            <a role="menuitem" tabindex="-1" href="">菜单第2项</a>
        </li>
        <li role="presentation">
            <a role="menuitem" tabindex="-1" href="">菜单第3项</a>
        </li>
        <li role="presentation">
            <a role="menuitem" tabindex="-1" href="">菜单第4项</a>
        </li>
    </ul>
</div>
```

在 javascript 中需要检测菜单位置，然后根据结果添加不同 class

```javascript
var determineDropDirection = function() {
    $(".dropdown-menu").each(function() {
        // 设置样式后可计算出实际高度
        $(this).css({
            visibility: "hidden",
            display: "block",
        })
        // 统一初始化为下拉菜单
        $(this).parent().removeClass("dropup")
        // 页面顶部菜单保持向下
        if ($(this).offset().top * 2 < $(document).height()) {
            $(this).removeAttr("style")
            return
        }
        // 判断菜单在页面位置，如果位置不够则向上展开
        if ($(this).offset().top + $(this).outerHeight() > $(window).height() + $(window).scrollTop()) {
            $(this).parent().addClass("dropup")
        }
        // 还原属性设置
        $(this).removeAttr("style")
    })
}
```

有两个时间点需要检测，一个是页面初始化完成时。一个是页面信息通过 AJAX 动态添加后，需要再次初始化。

```javascript
$(document).ready(function() {
    // 首次初始化
    determineDropDirection()
    // // 绑定鼠标进入时初始化，列表内容变动时需要更新
    $('body').on('mouseenter', '.dropdown', function(e) {
        determineDropDirection()
    })
})
```

由于用到下拉菜单的页面可能比较多，若在每次AJAX请求结束后进行检测，需要修改很多地方。这里是采用事件委托的方式，每次鼠标进入菜单进行检测。

![页面效果预览](http://oih6hf7qs.bkt.clouddn.com/blog/20170810-164936046.png)

参考链接：
[Bootstrap 官方文档](http://getbootstrap.com/javascript/#dropdowns)
[stackoverflow](https://stackoverflow.com/questions/32746598/bootstrap-dropdown-list-position-up-bottom-based-on-document-height)
