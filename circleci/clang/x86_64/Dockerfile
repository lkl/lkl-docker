FROM lkldocker/circleci:0.5
LABEL authors="Hajime Tazaki <thehajime@gmail.com>, Octavian Purdila <tavi@cs.pub.ro>"

ENV LLVM_VERSION=8
RUN sudo apt-get update && \
    sudo apt-get install -y wget && \
    wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | sudo apt-key add - && \
    sudo add-apt-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-$LLVM_VERSION main" && \
    sudo apt-get update && \
    sudo apt-get install -y libfuse-dev libarchive-dev \
                       linux-headers-4.4.0-97-generic \
                       valgrind libnuma-dev \
                       clang-$LLVM_VERSION lld-$LLVM_VERSION && \
    sudo ln -sf `which clang-$LLVM_VERSION` /usr/bin/clang && \
    sudo ln -sf `which ld.lld-$LLVM_VERSION` /usr/bin/ld.lld && \
    sudo rm -rf /var/lib/apt/lists/*
