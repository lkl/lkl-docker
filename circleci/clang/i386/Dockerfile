FROM i386/ubuntu:18.04
LABEL authors="Hajime Tazaki <thehajime@gmail.com>, Octavian Purdila <tavi@cs.pub.ro>"

ENV LLVM_VERSION=8
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:git-core/ppa && \
    apt-get update && \
    apt-get install -y sudo build-essential bc git xfsprogs ccache \
                       btrfs-tools iputils-ping dosfstools \
                       python python-pip bison flex iproute2 \
                       libfuse-dev libarchive-dev \
                       linux-headers-`uname -r` \
                       valgrind libnuma-dev \
                       clang-$LLVM_VERSION lld-$LLVM_VERSION && \
    ln -sf `which clang-$LLVM_VERSION` /usr/bin/clang && \
    ln -sf `which ld.lld-$LLVM_VERSION` /usr/bin/ld.lld && \
    pip install yamlish junit_xml && \
    rm -rf /var/lib/apt/lists/*

RUN useradd -ms /bin/bash ubuntu && \
    adduser ubuntu sudo && \
    echo -n 'ubuntu:ubuntu' | chpasswd

# Enable passwordless sudo for users under the "sudo" group
RUN sed -i.bkp -e \
      's/%sudo\s\+ALL=(ALL\(:ALL\)\?)\s\+ALL/%sudo ALL=NOPASSWD:ALL/g' \
      /etc/sudoers

USER ubuntu
WORKDIR /home/ubuntu/

ENV PATH /usr/lib/ccache:${PATH}
