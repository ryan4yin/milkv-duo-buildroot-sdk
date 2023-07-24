FROM ubuntu:22.04

USER root
WORKDIR /root

RUN sed -i 's@\(archive\|security\).ubuntu.com@mirrors.bfsu.edu.cn@g' /etc/apt/sources.list

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get -y install tzdata && \
    apt-get install -y \
      pkg-config build-essential ninja-build \
      automake autoconf libtool \
      wget curl git \
      gcc libssl-dev bc slib squashfs-tools \
      android-sdk-libsparse-utils jq python3-distutils scons parallel \
      tree python3-dev python3-pip device-tree-compiler  \
      ssh cpio fakeroot libncurses5 flex bison  \
      libncurses5-dev genext2fs rsync unzip dosfstools mtools tcl openssh-client \
      cmake && \
    apt clean && rm -rf /var/cache/apt ~/.cache

RUN echo "deb http://security.ubuntu.com/ubuntu focal-security main" | tee /etc/apt/sources.list.d/focal-security.list && \
    apt-get update && \
    apt-get install -y libssl1.1 && \
    apt clean && rm -rf /var/cache/apt ~/.cache


WORKDIR /root/sdk
