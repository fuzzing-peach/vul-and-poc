FROM buildpack-deps:bullseye

ARG version

RUN echo OpenSSL Version: $version

RUN apt install apt-transport-https ca-certificates

RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && apt clean

# Install common dependencies
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
    wget ca-certificates gnupg2 \
    apt-utils git build-essential curl sudo bison flex autoconf automake \
    libtool pkg-config git vim lsb-release software-properties-common \
    && rm -rf /var/lib/apt/lists

# Add a new user ubuntu, pass: ubuntu
RUN groupadd ubuntu && \
    useradd -rm -d /home/ubuntu -s /bin/bash -g ubuntu -G sudo -u 1000 ubuntu -p "$(openssl passwd -1 ubuntu)" && \
    echo "ubuntu ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Use ubuntu as default username
USER ubuntu
WORKDIR /home/ubuntu

RUN git config --global http.version HTTP/1.1 

ENV ASAN_OPTIONS='abort_on_error=1:symbolize=0:detect_leaks=0:detect_stack_use_after_return=1:detect_container_overflow=0:poison_array_cookie=0:malloc_fill_byte=0:max_malloc_fill_size=16777216'

# Clone openssl code repository from github or gitee
RUN git clone https://gitee.com/mirrors/openssl.git && \
    cd openssl && \
    git checkout openssl-${version} && \
    cd /home/ubuntu/openssl && \
    CFLAGS="-fsanitize=address -fno-omit-frame-pointer" CXXFLAGS="-fsanitize=address -fno-omit-frame-pointer" ./config shared zlib --prefix=/usr/local/openssl && \
    make -j

# LLVM
RUN wget https://apt.llvm.org/llvm.sh && \
    chmod +x llvm.sh

USER root

# Install OpenSSL
RUN cd /home/ubuntu/openssl && \
    make install && \
    echo "/usr/local/openssl/lib64" >> /etc/ld.so.conf && \
    ldconfig

# Install LLVM
RUN ./llvm.sh 17

ENV PATH="/usr/local/openssl/bin:${PATH}"