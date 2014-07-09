FROM ubuntu:14.04
MAINTAINER m.maatkamp@gmail.com version: 0.1

RUN apt-get update 
RUN apt-get install -y git subversion build-essential axel wget
RUN apt-get install -y automake1.10 libtool libncurses5-dev autoconf2.13 pkg-config gnu-standards libcurl4-gnutls-dev
RUN apt-get clean 

RUN apt-get install -y opencl-base  opencl-intel-cpu libnuma1
RUN wget http://registrationcenter.intel.com/irc_nas/4181/intel_sdk_for_ocl_applications_2014_ubuntu_4.4.0.117_x64.tgz
RUN tar zxpPvf intel_sdk_for_ocl_applications_2014_ubuntu_4.4.0.117_x64.tgz
RUN cd intel_sdk_for_ocl_applications_2014_ubuntu_4.4.0.117_x64
RUN ./install-cpu.sh
RUN cd .. 

RUN git clone https://github.com/girino/x13-sgminer.git
RUN cd x13-sgminer 
RUN ./autogen.sh
RUN CFLAGS="-O2 -Wall -march=native" ./configure 
RUN make
EXPOSE 80

CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
