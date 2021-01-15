FROM ubuntu:bionic
ENV DEBIAN_FRONTEND=noninteractive
RUN sed -i -e 's/^# deb-src /deb-src /g' /etc/apt/sources.list
RUN apt-get -y update && \
    apt-get -y build-dep llvm && \
    apt-get -y install cmake chrpath texinfo sharutils libffi-dev python3-dev libedit-dev libncurses5-dev swig python3-sphinx binutils-dev libjsoncpp-dev pkg-config lcov help2man zlib1g-dev g++-multilib libjs-mathjax python3-recommonmark doxygen gfortran ocaml-nox ocaml-findlib libctypes-ocaml-dev dh-exec dh-ocaml libpfm4-dev python3-setuptools libz3-dev devscripts curl libssl-dev
RUN cd /usr/src && curl -L https://github.com/Kitware/CMake/tarball/v3.19.3/ | tar -xz
RUN cd /usr/src && ln -s Kitware-CMake-* CMake
RUN cd /usr/src/CMake && \
    ./configure --prefix=/usr --parallel="$(getconf _NPROCESSORS_ONLN)" && \
    make -j"$(getconf _NPROCESSORS_ONLN)" && \
    make install && \
    make clean
