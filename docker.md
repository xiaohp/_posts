---
title: Dokcer 笔记
date: 2019-11-11 13:53:29
categories: 笔记本
toc: true
tags:
  - Docker
---

## 常用命令

```shell

# 搜索镜像
docker search ubuntu

# 下载镜像
docker pull ubuntu

# 列出本机所有镜像
docker images

```

## 启动容器

```shell
# 生成容器
docker run -d -t -p 8000:5000 --name demo ubuntu:18.04

# 停止
docker stop demo

# 启动
docker start demo

# 查看正在运行的容器
docker ps

# 查看所有容器
docker ps -a

# 删除停止的容器和运行种的容器
docker rm demo
docker rm -f demo1

# 在容器种安装软件
docker exec demo apt update
docker exec demo apt -y install python3 pyhon3-pip
docker exec demo apt pip3 install flask

# 拷贝文件
docker exec demo mkdir /code
docker cp a.py "demo:/code/a.py"
```
