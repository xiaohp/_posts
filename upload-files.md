---
title: AJAX 上传文件
date: 2017-07-26 14:10:29
categories: 笔记本
toc: true
tags:
  - Javascript
  - jQuery
  - AJAX
---

## form 表单上传

传统的上传文件方式，不支持回调，会刷新页面

```html
<form action="/upload/avatar" method="post" enctype="multipart/form-data">
    <input id="upload-file" type="file" name="avatar" required>
    <img src="" alt="" class="preview-img">
    <button id="submit-button">上传</button>
</form>
```

如果是上传图片，可以先在本地预览

```javascript
$('.upload-file').on("change", function(e) {
    var picture = this
    // 文件格式检测
    if (!(/\.jpg$|\.jpeg$|\.png$|\.gif$/i).test(picture.value)) {
        alert("上传图片格式不正确，请重新选择!")
        return false
    }
    // 预览图片
    var file = picture.files[0]
    // log('文件信息', file)
    var img_src = window.URL.createObjectURL(file)
    $('.preview-img')[0].src = img_src
})
```

## AJAX 上传

AJAX 方式获取数据有两种方式，可以使用 `form` 表单，也可以通过构造 `FormData` 上传，这里用的第二种

```html
<div>
    <input id="upload-file" type="file" name="avatar" required>
    <img src="" alt="" class="preview-img">
    <button id="submit-button">上传</button>
</div>
```

Javascript

```javascript

var fd = null

var upload = function(form_data) {
    var request = {
        url: '/upload/avatar',
        method: 'post',
        data: form_data,
        contentType: false,
        processData: false,
        success: function(r) {
            log('上传成功', r)
        },
        error: function(e) {
            log('debug e', e)
        }
    }
    $.ajax(request)
}

var bind_evetns = function() {
    $('#upload-file').on('change', () => {
        var element = $('#upload-file')
        var file = element.get(0).files[0]
        preview(file)
        fd = new FormData()
        fd.append('avatar', file)
    })

    $('#submit-button').on('click', (e) => {
        upload(fd)
    })
}

var preview = function(file) {
    var img_src = window.URL.createObjectURL(file)
    $('.preview-img')[0].src = img_src
}

bind_evetns()
```

参考链接：
[FormData](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData)
[FormData 对象的使用](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData/Using_FormData_Objects)
