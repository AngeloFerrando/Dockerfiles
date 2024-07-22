FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
    git \
	vim \
    python3 \
    pip \
    wget \
    software-properties-common \
    dirmngr \
    gpg \
    gpg-agent \
    locales \
    graphviz

# this SHELL command is needed to allow using source
SHELL ["/bin/bash", "-c"]  

ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8

## This was not needed before but we need it now
ENV DEBIAN_FRONTEND noninteractive

## Otherwise timedatectl will get called which leads to 'no systemd' inside Docker
ENV TZ UTC

# Install g++
RUN add-apt-repository ppa:ubuntu-toolchain-r/volatile \
        && apt-get update \
        && apt-get install -y --no-install-recommends \
           gcc-11 \
           g++-11 \
           gfortran-11 \
           r-base-dev \
           r-cran-rcpp \
        && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 60 \
                               --slave /usr/bin/g++ g++ /usr/bin/g++-11 \
                               --slave /usr/bin/gfortran gfortran /usr/bin/gfortran-11 \
 	&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds \
 	&& rm -rf /var/lib/apt/lists/*

# Install SPOT
RUN wget http://www.lrde.epita.fr/dload/spot/spot-2.12.tar.gz
RUN tar -xf spot-2.12.tar.gz 
WORKDIR /spot-2.12
RUN ./configure --prefix ~/.local
RUN make
RUN make install
WORKDIR /

RUN pip install notebook
