FROM golang:1.20.5
LABEL maintainer="Changjun Xiao"

# # The image is used to build chaosblade for musl
RUN wget http://www.musl-libc.org/releases/musl-1.1.21.tar.gz \
    && tar -zxvf musl-1.1.21.tar.gz \
    && rm musl-1.1.21.tar.gz \
    && cd musl* \
    && ./configure \
    && make \
    && make install \
    && rm -rf musl*

# install maven for java project compiled
RUN wget http://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/3.8.8/binaries/apache-maven-3.8.8-bin.tar.gz \
    && tar -zxvf apache-maven-3.8.8-bin.tar.gz \
    && rm apache-maven-3.8.8-bin.tar.gz \
    && mv apache-maven-3.8.8 /usr/local/apache-maven-3.8.8

RUN wget https://download.java.net/java/ga/jdk11/openjdk-11_linux-x64_bin.tar.gz -O /tmp/openjdk-11+28_linux-x64_bin.tar.gz \
    && mkdir -p /usr/lib/jvm/ \
    && tar xfvz /tmp/openjdk-11+28_linux-x64_bin.tar.gz --directory /usr/lib/jvm/ \
    && rm -rf /etc/alternatives/java \
    && ln -s /usr/lib/jvm/jdk-11/bin/java /etc/alternatives/java

RUN apt-get update \
    && apt-get install -y unzip

ENV CC /usr/local/musl/bin/musl-gcc
ENV GOOS linux
ENV java /usr/bin/java
ENV JAVA_HOME /usr/lib/jvm/jdk-11
ENV PATH /usr/local/apache-maven-3.8.8/bin:$JAVA_HOME/bin:$PATH


ENTRYPOINT [ "make" ]
