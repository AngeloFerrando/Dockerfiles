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

# Install Z3
RUN git clone https://github.com/Z3Prover/z3.git
WORKDIR /z3
RUN python3 scripts/mk_make.py
WORKDIR /z3/build
RUN make
RUN make install
WORKDIR /z3
RUN pip install z3-solver

WORKDIR /
# Install CVC5
RUN apt-get update
RUN apt-get install -y cmake python3.10-venv m4
RUN git clone https://github.com/cvc5/cvc5.git
WORKDIR /cvc5
RUN ./configure.sh --auto-download
WORKDIR /cvc5/build
RUN make
RUN make install

WORKDIR /
# Install Solvent
RUN git clone https://github.com/AngeloFerrando/Solvent.git
WORKDIR /Solvent
RUN pip3 install -r requirements.txt

