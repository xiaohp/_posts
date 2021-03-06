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

Dockerfile 编写

```
FROM node:10
COPY ./ /app
WORKDIR /app
RUN npm install && npm run build

FROM nginx
RUN mkdir /app
COPY --from=0 /app/dist /app
COPY nginx.conf /etc/nginx/nginx.conf
```

这里用到了多阶段构建, 可以将构建环境和运行环境分开, 减小镜像体积, 生成的镜像以最后一条为准
`COPY` 的 `--from=0` 参数, 从前面阶段拷贝文件到当前阶段
多个FROM语句时, 0 代表第一个阶段, 除了使用数字, 还可以给阶段命名

构建 Docker 镜像
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

## 使用数据卷 volume

```shell
# 创建 volume
docker volume create testvolume
# 列出 volume
docker volume ls
# 删除 volume
docker volume rm testvolume

# 启动容器时挂载数据卷到指定目录
--mount source=testvolume,target=/volume
# 例子
docker run -p 8080:5000 \
--name demo \
--mount source=testvolume,target=/volume ubuntu:18.04

# 共享目录
# 可以挂载文件和目录, 支持多个
--mount type=bind,source="${PWD}",target=/share
# 例子
docker run -p 8080:5000 \
--name demo \
--mount type=bind,source="${PWD}",target=/share ubuntu:18.04
```
