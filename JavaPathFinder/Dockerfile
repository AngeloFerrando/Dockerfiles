FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
    git \
	vim \
    openjdk-11-jdk \
    wget \
    unzip

# this SHELL command is needed to allow using source
SHELL ["/bin/bash", "-c"]  

# Install Gradle
RUN wget https://services.gradle.org/distributions/gradle-8.4-bin.zip
RUN mkdir /opt/gradle
RUN unzip -d /opt/gradle gradle-8.4-bin.zip

# Set Gradle in the environment variables
ENV GRADLE_HOME /opt/gradle/gradle-8.4
ENV PATH $PATH:/opt/gradle/gradle-8.4/bin

# Clone JavaPathFinder repository
RUN git clone https://github.com/javapathfinder/jpf-core

# Build JavaPathFinder
WORKDIR /jpf-core
RUN ./gradlew buildJars



