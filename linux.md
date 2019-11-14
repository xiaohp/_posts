---
title: linux 笔记
date: 2019-11-11 13:53:29
categories: 笔记本
toc: true
tags:
  - linux
---

## 常用命令

1. 帮助

```shell
# manual 缩写
# 查看帮助
man ls
# 查看指定章节
man 7 man
```

## 常见问题
中文乱码

```shell
# 查看使用语言
echo $LANG
# 查看语言信息
locale
# 安装中文
yum -y groupinstall "Chinese Support"
# 切换中文
LANG="zh_CN.UTF-8"
```
