---
title: linux 命令行笔记
date: 2018-06-18 16:40:29
categories: 笔记本
toc: true
tags:
  - linux
  - CLI
---

## 文件与目录
`pwd` print working directory 输出当前所在位置
`cd` change directory 改变工作目录

```bash
cd Desktop
cd /etc
cd ../git
```

`ls` list 列出目录内容
选项 `a` 表示 all, 会列出包含隐藏文件
选项 `l` 表示 long, 会列出目录下文件的更多信息, 包含权限, 用户, 体积等

```bash
ls -a
ls -l
ls -la
```

`mkdir` make directories 创建新目录
`touch` 创建一个空白文件
`mv` move 移动文件和重命名文件

```bash
# 如果 b 目录已经存在, 移动文件
mv a.txt b
# 重命名文件夹
mv hosts hosts_bak
# 移动到临时文件目录的方式来删除文件
mv a.txt /tmp
```

`cp` copy 复制指定的文件与目录

```bash
# 将 a.txt 复制到 b 目录
cp a.txt b
# 复制目录及其子目录和文件, 使用 -R 选项
cp -R b c
```

`cat` 输出文件内容
可以另外安装 [bat](https://github.com/sharkdp/bat) 输出带语法高亮的内容
`tail` 输出文件里的最后一小部分内容


### 特殊符号
~
波浪号, 表示用户主目录, 如果当前是 root 用户, 则执行 `cd ~` 会进入`/Users/root` 目录
/
斜杠, 表示根目录
.
一个点, 表示当前目录
..
两个点, 表示上一级目录

## 使用 vi 编辑文件

```
vi README.md
```

按小写 `i` 进入 vi 的编辑模式;
按 `esc` 退出编辑模式;
按 `/` 搜索文件内容,输入要搜索的关键词, `n` 继续查找, `N` 往前查找
保存并退出 `:wq`
不保存退出 `:q!`

## 其他资源
[explainshell.com](https://explainshell.com/) 这个网站可以查询命令的参数
