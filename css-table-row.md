---
title: 使用CSS table-row 实现表单布局
date: 2017-03-02 22:53:29
categories: 笔记本
toc: true
tags:
  - CSS
---
效果图：
![](http://oih6hf7qs.bkt.clouddn.com/17-3-3/72338246-file_1488500455600_6b2a.jpg)
里面的表单分为左右两块，以中间为分割，左边靠右对齐，右边靠左对齐。
使用 table-row 可以方便的实现。
HTML代码
```html
<form class="" action="index.html" method="post">
    <div class="tableRow">
        <p>请输入邮箱地址：</p>
        <p>
            <input class="right" type="text" name="" value="" placeholder="这是一个文本输入框"> <br>
            <span class="tips">邮箱地址请按格式输入</span>
        </p>
    </div>
    <div class="tableRow">
        <p>请输入密码：</p>
        <p>
            <input class="right" type="text" name="" value="" placeholder="这是一个文本输入框">
        </p>
    </div>
    <div class="tableRow">
        <p>请重复输入密码：</p>
        <p>
            <input class="right" type="text" name="" value="" placeholder="这是一个文本输入框"> <br>
            <span class="tips">密码请为6-16位英文数字</span>
        </p>
    </div>
    <div class="tableRow">
        <p>性别：</p>
        <p>
            <input class="right" type="radio" name="gender" value="man">男
            <input type="radio" name="gender" value="woman">女
        </p>
    </div>
    <div class="tableRow">
        <p>城市：</p>
        <p>
            <select class="city right" name="">
                <option value="beijing">北京</option>
                <option value="shanghai">上海</option>
                <option value="guangzhou">广州</option>
                <option value="shenzhen">深圳</option>
            </select>
        </p>
    </div>
    <div class="tableRow">
        <p>爱好：</p>
        <p>
            <input type="checkbox" name="hobby" value="">游泳
            <input type="checkbox" name="hobby" value="">跑步
            <input type="checkbox" name="hobby" value="">阅读
        </p>
    </div>
    <div class="tableRow">
        <p>个人描述：</p>
        <p>
            <textarea class="right" name="name" rows="8" cols="80" placeholder="这是一个多行输入框"></textarea>
            <button class="sub" type="button" name="button">确认提交</button>
        </p>
    </div>

</form>
```
在页面中每一行使用div包起来，然后左侧和右侧分别放在p标签中。设置div为table-row布局，子元素p为table-cell布局。
CSS
```css
div.tableRow {
    display: table-row;
}

div.tableRow p {
    display: table-cell;
    width: 200px;
    vertical-align: top;
	padding: 4px;
}
div.tableRow p:first-child {
    text-align: right;
}
```
其中第一个子元素可通过伪元素设置右对齐。
