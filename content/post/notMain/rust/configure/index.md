---
title: "Rust Configure"
description: 
date: 2025-01-06T20:50:10+08:00
image: assets/rust.png
math: true
toc: true
tags:
    - Rust
---

# Rust 安装与配置

## 安装
### 安装 Rust

官网安装：一路回车就行了

```shell
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

换源安装（中科大源）：

```shell
curl --proto 'https' --tlsv1.2 https://mirrors.ustc.edu.cn/misc/rustup-install.sh -sSf > rust.sh && chmod +x rust.sh

export RUSTUP_DIST_SERVER=https://mirrors.ustc.edu.cn/rust-static
export RUSTUP_UPDATE_ROOT=https://mirrors.ustc.edu.cn/rust-static/rustup

sudo bash rust.sh
```

### 查看 Rust 版本

```shell
rustc -V
cargo -V
```

## 配置
### 包管理器换源

可以直接新建 `~/.cargo/config.toml` 文件，写入：

```shell
[source.crates-io]
replace-with = 'ustc'

[source.ustc]
registry = "sparse+https://mirrors.ustc.edu.cn/crates.io-index/"
```

或者安装 `crm` 镜像源管理器：[crm](https://github.com/wtklbm/crm)

```shell
cargo install crm

crm best
```