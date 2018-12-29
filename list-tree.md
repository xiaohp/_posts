---
title: macOS 使用 tree 列出文件目录树
date: 2018-12-29 13:53:29
categories: 笔记本
toc: true
tags:
  - CLI
  - macOS
  - 工具
---

# 效果

```
.
├── SQLite
│   └── tysql.sqlite
├── TeachYourselfSQL_MySQL
│   ├── README.pdf
│   ├── create.txt
│   └── populate.txt
├── TeachYourselfSQL_MySQL.zip
└── TeachYourselfSQL_SQLite.zip
```

<!-- more -->

# 安装

```bash
brew install tree
```

# 使用

## 直接使用

```bash
tree
```

## 解决中文乱码

```bash
tree -N
```

## 指定目录深度

```bash
tree -L 2

# 其他命令说明可以在 help 中查看
tree --help
```
