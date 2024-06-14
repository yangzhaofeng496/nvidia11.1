FROM nvidia/cuda:11.1.1-cudnn8-devel-ubuntu20.04
LABEL author="yang"

ENV PASSWORD="123456" 

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone \
    && sed -i "s/archive.ubuntu.com/mirrors.aliyun.com/g" /etc/apt/sources.list \
    && sed -i "s/security.ubuntu.com/mirrors.aliyun.com/g" /etc/apt/sources.list \
    && apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/3bf863cc.pub \
    && apt clean && apt update && apt install -yq --no-install-recommends sudo \
    && sudo apt install -yq --no-install-recommends python3 python3-pip libgl1-mesa-glx libglib2.0-0 libsm6 libxext6 libxrender-dev openssh-server \
    && sudo pip3 install --upgrade pip \
    && sudo pip3 config set global.index-url https://mirrors.aliyun.com/pypi/simple \
    && sudo pip3 install setuptools \
    && sed -i "s/#PubkeyAuthentication/PubkeyAuthentication/g" /etc/ssh/sshd_config \
    && sed -i "s/#AuthorizedKeysFile/AuthorizedKeysFile/g" /etc/ssh/sshd_config \
    && sed -i "s/#PermitRootLogin prohibit-password/PermitRootLogin yes/g" /etc/ssh/sshd_config \
    && sudo /etc/init.d/ssh restart \
    && echo "root:${PASSWORD}" | chpasswd
ENTRYPOINT /etc/init.d/ssh restart && /bin/bash
