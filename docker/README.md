# Milk-V Duo 玩耍笔记

官方 SDK: https://github.com/ryan4yin/milkv-duo-buildroot-sdk

特点：基于 buildroot 构建框架搭建的 Linux SDK.


## 运行 htop

首先修改 buildroot 的 configs 文件（暂时必须手动改配置，不能 make menuconfig），添加 HTOP 的安装参数。

然后编译启动系统，并通过如下命令运行 htop:

```
# 设置时间，不然没有 btime htop 跑不起来
date -s "2023-07-04"
# 启用全彩终端显示效果
export TERM=xterm-256color
# 运行 htop
htop
```

## CV1800B 芯片简介

看算能的官方文档，这块芯片提供了比较强的图像处理能力以及 AI 推理能力，有待后续发掘。

- https://community.milkv.io/c/duo/5
- https://milkv.io/zh/docs/duo/resources/mmf


## 常见根文件系统构建框架

1. buildroot
   1. 优点：构建简单，易于理解，能构建完整镜像。
   2. 缺点：无包管理器，要安装包，要么自己 make install，要么就得重新构建整个根文件系统重新烧录
2. ubuntu
   1. 优点：构建方便，包管理工具应用广泛，还支持一些 ROS 操作系统
   2. 缺点：构建的文件系统较大
3. debian
   1. 优点：构建方便，包管理工具跟 ubuntu 一样也是 apt-get/dpkg，还有可视化配置界面。
   2. 缺点：跟 ubuntu 一样，也是文件系统较大
4. yocto
   1. 优点：支持的框架较多，能构建完整镜像
   2. 缺点：配置较复杂，不适合新手
5. busybox
   1. 优点：体积小，支持所有常见 Linux 命令，常用于定制特定功能的最小系统
   2. 缺点：功能不全，无包管理工具。（仅使用 busybox 的系统基本不会有人想登录上去使用）



## ION 内存控制

64M 内存默认情况下 Linux 用户空间仅有 28M 可用，因为有一部分RAM被分配绐了 [ION](https://github.com/milkv-duo/duo-buildroot-sdk/blob/develop/build/boards/default/dts/cv180x/cv180x_default_memmap.dtsi#L15)，您可以修改这个 [ION_SIZE](https://github.com/milkv-duo/duo-buildroot-sdk/blob/develop/build/boards/cv180x/cv1800b_milkv_duo_sd/memmap.py#L43) 的值然后重新编译生成固件.

> https://ricardolu.gitbook.io/trantor/ion-memory-control

那 ION 到底是个啥呢？根据查到的资料介绍，ION 是 Android 4.0 引入的一套内存管理机制，用于改善对于当前不同平台的android设备，使用各种不同内存管理接口来管理相应内存的状况，ION将内存管理机制抽象成一系列通用的接口，可集中分配各类不同内存(ion_heap_type区分)。
