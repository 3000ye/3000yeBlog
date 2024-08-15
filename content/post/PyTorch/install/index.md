---
title: Install PyTorch on MaxOS
description: Install PyTorch and use M1 GPU
date: 2024-08-15T16:25:46+08:00
image: assets/pytorch.png
math: true
toc: true
categories:
    - PyTorch
tags:
    - Python
---

# MaxOS 安装 PyTorch

## 安装 Conda

根据官方文档安装 MiniConda：https://docs.anaconda.com/miniconda/

```shell
mkdir -p ~/miniconda3
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh -o ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh

~/miniconda3/bin/conda init zsh
```

查看 Conda 版本：

```shell
conda --version
```

## 新建 Conda 环境

新建 Conda 环境，Python 版本最好高于 `3.8`：

```shell
conda create -n pytorch_learn python = 3.10

conda activate pytorch_learn
```

## 安装 PyTorch

根据 PyTorch 官网的提示安装：https://pytorch.org

```shell
pip3 install torch torchvision torchaudio
```

重装 `numpy`（非必须），有可能 PyTorch 自带的 `numpy` 版本过低，可以手动重装：

```shell
pip3 uninstall numpy
pip3 install numpy
```

## 配置 Jupyter GPU Kernel

为了使用 MaxOS M 芯片的 GPU，需要安装一个新的 Jupyter 内核：

```shell
conda activate pytorch_learn //注意替换成自己的虚拟环境名
conda install ipykernel //安装ipykernel
sudo python -m ipykernel install --name pytorch_learn //在ipykernel中安装当前环境 
conda deactivate
```

启动 Jupyter 后切换 内核：

<div style='display: flex; justify-content: center;'>
<img src='assets/kernel.jpg' alt='img' style='zoom:60%;' />
</div>

## 测试 PyTorch

```python
import torch

print(torch.backends.mps.is_available())
print(torch.backends.mps.is_built())

device = torch.device("mps" if torch.backends.mps.is_available() else "cpu")
```