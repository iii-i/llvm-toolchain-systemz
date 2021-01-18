FROM ubuntu:bionic as img
ENV DEBIAN_FRONTEND=noninteractive
RUN sed -i -e 's/^# deb-src /deb-src /g' /etc/apt/sources.list
RUN apt-get -y update && \
    apt-get -y install \
        apt-transport-https \
        binutils-dev \
        ca-certificates \
        chrpath \
        cmake \
        curl \
        devscripts \
        dh-exec \
        dh-ocaml \
        doxygen \
        dpkg-dev \
        gfortran \
        g++-multilib \
        gnupg \
        help2man \
        lcov \
        libctypes-ocaml-dev \
        libedit-dev \
        libffi-dev \
        libjs-mathjax \
        libjsoncpp-dev \
        libncurses5-dev \
        libpfm4-dev \
        libssl-dev \
        libz3-dev \
        ocaml-findlib \
        ocaml-nox \
        pkg-config \
        python3-dev \
        python3-recommonmark \
        python3-setuptools \
        python3-sphinx \
        qtbase5-dev \
        quilt \
        sharutils \
        software-properties-common \
        swig \
        texinfo \
        wget \
        zlib1g-dev
RUN wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | gpg --dearmor - | tee /etc/apt/trusted.gpg.d/kitware.gpg >/dev/null
RUN apt-add-repository -s 'deb https://apt.kitware.com/ubuntu/ bionic main'
RUN cd /usr/src && apt-get -y update && apt-get source cmake

FROM img as tmp
RUN cd /usr/src/cmake-*/ && DEB_BUILD_OPTIONS=nocheck debuild -i -us -uc -b

FROM img as img
COPY --from=tmp /usr/src/*.deb /tmp/cmake-debs/
RUN dpkg -i /tmp/cmake-debs/*
