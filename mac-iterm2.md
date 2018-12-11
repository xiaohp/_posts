---
title: macOS iTerm2 配置备忘
date: 2018-04-15 16:40:29
categories: 笔记本
toc: true
tags:
  - macOS
  - iTerm2
  - 工具
  - CLI
---

最近在新电脑上配置了 macOS 的开发环境，记录一下 `iTerm2` 的配置过程。

## 下载安装 iTerm2
方案一, 在[iTerm2 官网](https://www.iterm2.com/) 下载安装

方案二, 使用 homebrew 进行安装

```bash
brew cask install iterm2
```

## 设置 zsh 与 oh-my-zsh

### 修改 `shell` 为 `zsh`

```bash
chsh -s /bin/zs
```

<!-- more -->

### 安装 `oh-my-zsh`

```bash
cd ~/
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.zshrc ~/.zshrc.orig
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```

### 修改 theme
打开配置文件

```bash
atom .zshrc
```

把里面的主题设置 `ZSH_THEME="robbyrussell"` 修改为

```
#ZSH_THEME="robbyrussell"
ZSH_THEME="agnoster"
```

即注释之前的内容, 修改主题.

### 修改 agnoster 的 theme source code
在终端输入

```bash
atom ~/.oh-my-zsh/themes/agnoster.zsh-theme
```

Atom 会打开 `agnoster.zsh-theme` 这个文件, 把这个文件的内容替换为 [这个链接](https://gist.github.com/agnoster/3712874/raw/c3107c06c04fb42b0ca27b0a81b15854819969c6/agnoster.zsh-theme ) 里面的内容.保存后关闭 Atom.

### 安装字体
在 [这里](https://gist.github.com/qrush/1595572) 点击 `Download ZIP` 下载字体文件.解压后安装.

## 设置背景
点击下载 [solarized](http://ethanschoonover.com/solarized/files/solarized.zip) 并解压缩
打开 iTerm2 的 `Preferences` 设置
更换背景
![](/images/article/1740122.jpg)
![](/images/article/30339310.jpg)
更换字体
![](/images/article/98871498.jpg)
按 `command + q` 退出再打开.可看到如下效果即设置完成.
![](/images/article/34191125.jpg)

### 隐藏用户名

在 `~/.zshrc` 添加默认用户名

```bash
DEFAULT_USER="你的用户名"     #增加这一项，可以隐藏掉路径前面那串用户名
```
