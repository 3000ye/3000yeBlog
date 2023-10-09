---
title: Elegant LaTeX
description: How to elegantly use LaTeX to create
date: 2023-10-09T17:18:55+08:00
image: assets/latex.jpg
math: true
toc: true
categories:
    - Note tools
tags:
    - Latex
---

# 使用 $\LaTeX$ 优雅地完成创作

$\LaTeX$ 是一个文档准备系统 (Document Preparing System)，它非常适用于生成高印刷质量的科技类和数学类文档。它也能够生成所有其他种类的文档，小到简单的信件，大到完整的书籍。 $\LaTeX$ 使用 $\TeX$ 作为它的排版引擎，学习 $\LaTeX$ 是一个漫长而痛苦的过程，我们应该充分利用已知的资料，来尽量完成我们的需求。

## 从安装 $\TeX$ 引擎开始

$\TeX$ 引擎类似于 `gcc/g++` 或 `Python`，用于编译 $\LaTeX$ 文档。

不同平台中 $\TeX$ 的安装方法不尽相同，本文提供：`Windows11`、`Linux(Ubuntu 22.04)`、`MacOs(12.7)`、`Windows11-wsl2(Ubuntu22.04)`的安装方法。

### Windows11

进入网站[tug.org for windows](https://tug.org/texlive/windows.html#install)，点击`install-tl-windows.exe`下载 $\TeX$ 安装器，然后运行安装即可。

<div style="display: flex; justify-content: center;">
<img src="assets/windowsInstall.png" alt="img" style="zoom:100%"/>
</div>

不过，这种方法需要一直联网安装，网速不好的环境可以直接下载`iso`镜像进行本地安装。本文给出清华源镜像地址：[mirrors.tuna](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/)，下载后缀为`.iso`的文件（只用下载一个）。

下载完成后双击文件挂载镜像，然后打开镜像文件夹，右键点击`install-tl-windows.bat`文件，使用管理员打开，然后按照指引安装即可。

最新版本的安装器会自动添加环境变量，安装完成后打开`cma`然后输入：

```shell
tex --version
```

若能输出 $\TeX$ 版本信息则安装成功：

```shell
TeX 3.141592653 (TeX Live 2023/W32TeX)
kpathsea version 6.3.5
Copyright 2021 D.E. Knuth.
```

### Linux(Ubuntu22.04)

打开终端，然后执行安装命令：

```shell
sudo apt update
sudo apt upgrade
sudo apt install texlive-full
```

等待安装完成即可，安装完成后执行命令：

```shell
tex --version
```

若能输出 $\TeX$ 版本信息则安装成功：

```shell
TeX 3.141592653 (TeX Live 2023/Debian)
kpathsea version 6.3.5
Copyright 2021 D.E. Knuth.
```

### MacOs(12.7)

打开终端，然后执行安装命令（推荐安装无窗体版本）：

```shell
brew install mactex-no-gui
```

等待安装完成即可，安装完成后执行命令：

```shell
tex --version
```

若能输出 $\TeX$ 版本信息则安装成功：

```shell
TeX 3.141592653 (TeX Live 2023)
kpathsea version 6.3.5
Copyright 2023 D.E. Knuth.
```

### Windows11-wsl2(Ubuntu22.04)

在`wsl2`中安装方式与在`Linux`中一样。