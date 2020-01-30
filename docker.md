---
title: Docker 笔记
date: 2019-11-11 13:53:29
categories: 笔记本
toc: true
tags:
  - Docker
---

## 镜像常用命令

```shell
# 搜索镜像
docker search ubuntu

# 下载镜像
docker pull ubuntu

# 列出本机所有镜像
docker images
docker image ls

# 删除镜像, 通过 image id
docker image rm 16508e5c265d
# 删除镜像, 通过 REPOSITORY:TAG
docker rmi ubuntu:latest
```
<!-- more -->
## 容器常用命令

```shell
# 生成容器
# 启动容器并映射端口
docker run -d -t -p 8080:5000 --name demo ubuntu:18.04
# 参数说明
# -d --detach 在后台运行容器，打印容器 id
# -t --tty 分配一个虚拟 shell
# -p 端口映射
# -i --interactive 保持 STDIN 打开

# 进入容器的终端
docker exec -it demo bash

# 停止
docker stop demo

# 启动
docker start demo

# 查看正在运行的容器
docker ps

# 查看所有容器
docker ps -a

# 删除停止的容器
docker rm demo
# 删除运行中的容器需要 -f force
docker rm -f demo1
```

## 使用 Dockerfile 构建镜像
```shell
# -t 指定镜像名城为 imagename. 最后的点表示工作目录为当前目录
docker build -t imagename .
```

## 对容器进行操作

```shell
# 在容器中运行命令安装软件
docker exec demo apt update
docker exec demo apt -y install python3 pyhon3-pip
docker exec demo apt pip3 install flask

# 拷贝文件
docker exec demo mkdir /code
docker cp a.py "demo:/code/a.py"
```
