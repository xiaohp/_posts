---
title: V2Ray 环境搭建简约笔记
date: 2019-12-30 13:53:29
categories: 笔记本
toc: true
tags:
  - V2Ray
---

## 购买机器域名

1. 购买机器, 可以使用 [vultr](https://www.vultr.com/?ref=7214221), [linode](https://www.linode.com/)等
2. 购买域名, 直接在阿里云或者腾讯云购买
3. 配置域名指向服务器
<!-- more -->

## 服务器基础配置

1. 配置开启 BBR
2. 配置端口, 关闭除了 443/80/22 以外的端口
3. 安装 Docker
4. 安装 Docker Compose

## 服务器 V2Ray 配置

1. 下载 [v2ray-tls-docker](https://github.com/Sparkness/v2ray-tls-docker)
2. 安装说明配置域名
3. Docker Compose 启动

## 客户端 V2Ray 配置

1. 下载服务器生成的 json 文件到本地
2. 将 json 文件导入客户端
