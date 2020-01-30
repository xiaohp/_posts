---
title: linux 命令行笔记
date: 2018-06-18 16:40:29
categories: 笔记本
toc: true
tags:
  - linux
  - CLI
  - macOS
---

## 帮助

```shell
# manual 缩写
# 查看帮助
man ls
# 查看指定章节
man 7 man
```

<!-- more -->

## 文件与目录
`pwd` print working directory 输出当前所在位置
`cd` change directory 改变工作目录

```bash
# 绝对路径
cd /etc
# 相对路径
cd ../git
```

`ls` list 列出目录内容, 后面可以加目录
`-a` 表示 all, 会列出包含隐藏文件
`-l` 表示 long, 长格式显示
`-r` 表示 reverse, 逆序显示
`-t` 表示 time, 按修改时间顺序显示
`-R` 表示 Recursively, 递归显示子目录

```bash
ls -a
ls -l
ls -la
ls -l /root / 分别列出对应目录
```

`mkdir` make directories 创建新目录
`touch` 创建一个空白文件
`mv` move 移动文件和重命名文件

```bash
# 创建嵌套目录
mkdir -p a/b/c
# 如果 b 目录已经存在, 移动文件
mv a.txt b
# 重命名文件夹
mv hosts hosts_bak
# 移动到临时文件目录的方式来删除文件
mv a.txt /tmp
```

`cp` copy 复制指定的文件与目录

```bash
# 复制文件
cp a.txt b.txt
# 将 a.txt 复制到 b 目录, 保留文件名
cp a.txt b
# 复制目录及其子目录和文件, 使用 -R 选项
cp -R b c
```

`cat` 输出文件内容
可以另外安装 [bat](https://github.com/sharkdp/bat) 输出带语法高亮的内容

`tail` 输出文件里的最后一小部分内容

```bash
tail filename
# 使用参数 -f 可以循环读取文件内容, 常用来查阅正在改变的日志文件
tail -f filename
```

`tar` 命令可以解压

```bash
tar zxvf node_modules.tar.gz -C /home/frontend
```

`grep` 查找文件里符合条件的字符串

```bash
grep '促销活动' error_log20180717004
# 查找前缀有 error_log20180717 的文件中包含 促销活动 字符串的文件
grep '促销活动' error_log20180717*
```

`open` macOS 下打开文件或目录

```bash
# 打开当前目录
open .
# 打开指定目录
open ~/Documents
# 打开指定文件(使用关联的应用)
open a.txt
```

## 用户

```bash
# 显示当前用户
whoami
# 切换用户并进入该用户的 home 目录
sudo su - username
# 仅切换用户, 停留在当前目录
sudo su username
# 切换到 root 用户
su - root
```

root 修改普通用户密码

```bash
passwd username
```

然后连续两次输入新的用户密码即可

## 特殊符号

`~` 波浪号, 表示用户主目录, 如果当前是 root 用户, 则执行 `cd ~` 会进入`/Users/root` 目录
`/` 斜杠, 表示根目录
`.` 一个点, 表示当前目录
`|` 管道
`..` 两个点, 表示上一级目录
`>` 重定向符号, 将命令的输出重定向到文件中, 覆盖式
`>>` 追加式重定向

```bash
echo "hello" > a.txt
```

## 查找相关

`history` 查看历史命令
`grep` 查找

```bash
history | grep touch
```

`ps` 查看进程

```bash
# 查看带 node 字符串的进程
ps ax | grep node
```

## 使用 vi 编辑文件

```bash
vi README.md
```

按小写 `i` 进入 vi 的编辑模式;
按 `esc` 退出编辑模式;
按 `/` 搜索文件内容,输入要搜索的关键词, `n` 继续查找, `N` 往前查找
保存并退出 `:wq`
不保存退出 `:q!`

## 终端走代理

在 macOS 下, 设置系统代理后, 对普通应用有效, 但是终端需要额外设置

```bash
export http_proxy="http://127.0.0.1:1087"
export https_proxy="http://127.0.0.1:1087"
# 使用 shadowsocks
export ALL_PROXY="socks5://127.0.0.1:1086"
```

## 网络

`telnet` 测试网络是否连通

```bash
telnet 59.37.96.63 80
```

查看本机 ip

```bash
# 方法一
ifconfig

# 方法二
ip addr show
```

`curl` 查看网址

```bash
curl google.com

# <HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
# <TITLE>301 Moved</TITLE></HEAD><BODY>
# <H1>301 Moved</H1>
# The document has moved
# <A HREF="http://www.google.com/">here</A>.
# </BODY></HTML>

# -I --head
# 仅拉取 http 头
curl -I google.com

# HTTP/1.1 301 Moved Permanently
# Location: http://www.google.com/
# Content-Type: text/html; charset=UTF-8
# Date: Mon, 19 Aug 2019 12:59:01 GMT
# Expires: Wed, 18 Sep 2019 12:59:01 GMT
# Cache-Control: public, max-age=2592000
# Server: gws
# Content-Length: 219
# X-XSS-Protection: 0
# X-Frame-Options: SAMEORIGIN

# -i, --include
# 在结果中包含 http 头
curl -i google.com

# HTTP/1.1 301 Moved Permanently
# Location: http://www.google.com/
# Content-Type: text/html; charset=UTF-8
# Date: Mon, 19 Aug 2019 12:58:57 GMT
# Expires: Wed, 18 Sep 2019 12:58:57 GMT
# Cache-Control: public, max-age=2592000
# Server: gws
# Content-Length: 219
# X-XSS-Protection: 0
# X-Frame-Options: SAMEORIGIN
#
# <HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
# <TITLE>301 Moved</TITLE></HEAD><BODY>
# <H1>301 Moved</H1>
# The document has moved
# <A HREF="http://www.google.com/">here</A>.
# </BODY></HTML>
```

`wget` 下载文件

```bash
wget http://example.com/file.iso
# -m 下载所有文件, 相当于 mirror
wget -m http://example.com
```

`scp` 传输文件

```bash
# 上传 app 目录到服务器 /path 目录
scp -r app username@ip:/path
# 下载
scp -r username@ip:/path /home/app
```

`dig` 解析域名

```bash
dig baidu.com
nslookup baidu.com

指定 DNS
dig @10.10.10.10 baidu.com
```


## 进程
查看端口号占用
```bash
# 可能需要 sudo
lsof -i:8080
# COMMAND   PID USER   FD   TYPE   DEVICE SIZE/OFF NODE NAME
# node    30246 root   11y  IPv6 12345678      0t0  TCP *:8080 (LISTEN)
```

结束进程
```bash
# 可能需要 sudo, PID 在上一步得到
kill -9 PID
# kill -9 26993
```

## 其他

adb 安装 apk, 文件路径可以通过把 apk 拖动到终端中来生成.
```bash
adb install -r /Users/fredxiao/Desktop/app-debug.apk
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


## 其他资源
[explainshell.com](https://explainshell.com/) 可以查询命令的参数
[TLDR pages](https://tldr.sh/) 更简洁的帮忙文档
[bat](https://github.com/sharkdp/bat) 代码高亮版 `cat`
