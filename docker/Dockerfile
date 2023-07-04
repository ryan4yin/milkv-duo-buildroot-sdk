FROM ubuntu:20.04

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
      android-sdk-libsparse-utils android-sdk-ext4-utils \
      jq python3-distutils tclsh scons parallel \
      ssh-client tree python3-dev python3-pip device-tree-compiler \
      ssh cpio fakeroot libncurses5 \
      flex bison libncurses5-dev genext2fs \
      rsync unzip dosfstools mtools && \
    apt clean && rm -rf /var/cache ~/.cache

# install cmake
RUN curl -L https://github.com/Kitware/CMake/releases/download/v3.26.4/cmake-3.26.4-linux-x86_64.sh -o cmake.sh && \
    chmod +x cmake.sh && \
    ./cmake.sh --skip-license --prefix=/usr/local/ && \
    rm cmake.sh
