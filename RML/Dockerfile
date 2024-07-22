FROM ubuntu:22.04

RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install -y curl
RUN apt install git -y
RUN apt-get update -y

RUN apt-get install openjdk-17-jdk -y
RUN apt-get update -y

RUN apt-get update -y
RUN apt-get install swi-prolog -y

RUN git clone https://github.com/RMLatDIBRIS/compiler.git
WORKDIR /compiler/
RUN ./gradlew build
WORKDIR /
RUN git clone https://github.com/RMLatDIBRIS/monitor.git
RUN git clone https://github.com/RMLatDIBRIS/running_examples.git