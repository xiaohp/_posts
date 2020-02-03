---
title: git 代理配置
date: 2020-02-03 09:53:29
categories: 笔记本
toc: true
tags:
  - git
---

因为疫情关系开始在家办公。之前使用的 iOA NGN 版本，拉取内网代码需要额外设置代理。
现在使用 VPN 版本拉取代码会报错，需要取消代理。

## 全局设置代理

```shell
git config --global http.proxy 'socks5://127.0.0.1:8080'
git config --global https.proxy http://127.0.0.1:8080
# 取消代理
git config --global --unset http.http://github.com.proxy
git config --global --unset http.https://github.com.proxy
```

<!-- more -->

## 对指定网址设置代理

```shell
git config --global http.http://github.com.proxy http://127.0.0.1:8080
git config --global http.https://github.com.proxy http://127.0.0.1:8080

// 取消代理
git config --global --unset http.http://github.com.proxy
git config --global --unset http.https://github.com.proxy
```

## FAQ

执行取消报错时, 可以直接编辑 `.gitconfig` 文件, 删除对应配置信息
