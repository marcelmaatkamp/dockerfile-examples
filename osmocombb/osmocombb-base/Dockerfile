FROM ubuntu:14.04

MAINTAINER m.maatkamp@gmail.com version: 0.1

RUN apt-get update
RUN apt-get dist-upgrade -yf
RUN apt-get clean
RUN apt-get autoremove

# ---
RUN apt-get install -y git subversion build-essential axel wget make automake1.10 libtool libncurses5-dev autoconf2.13 pkg-config gnu-standards libcurl4-openssl-dev ssh-client openssh-server
RUN apt-get install -y libtool shtool automake autoconf git-core pkg-config make gcc

# ---
RUN git clone git://git.osmocom.org/osmocom-bb.git
RUN cd osmocom-bb/src && make

# ---
WORKDIR         /cpuminer
ENTRYPOINT      ["./minerd"]
