FROM ubuntu:12.04

MAINTAINER m.maatkamp@gmail.com version: 0.1

RUN apt-get update
RUN apt-get dist-upgrade -yf
RUN apt-get clean
RUN apt-get autoremove

RUN apt-get install -y git subversion axel wget zip unzip 

# ---
# Install cross-compile
# ---

RUN mkdir -p gnu-arm
RUN cd gnu-arm
RUN cd gnu-arm && wget http://bb.osmocom.org/trac/raw-attachment/wiki/GnuArmToolchain/gnu-arm-build.2.sh
RUN cd gnu-arm && chmod a+rx gnu-arm-build.2.sh
RUN apt-get install -y build-essential libgmp3-dev libmpfr-dev libx11-6 libx11-dev texinfo flex bison libncurses5 libncurses5-dbg libncurses5-dev libncursesw5 libncursesw5-dbg libncursesw5-dev zlibc zlib1g-dev libmpfr4 libmpc-dev
RUN cd gnu-arm && mkdir build install src
RUN cd gnu-arm/src && wget http://ftp.gnu.org/gnu/gcc/gcc-4.5.2/gcc-4.5.2.tar.bz2
RUN cd gnu-arm/src && wget http://ftp.gnu.org/gnu/binutils/binutils-2.21.1a.tar.bz2
RUN cd gnu-arm/src && wget ftp://sources.redhat.com/pub/newlib/newlib-1.19.0.tar.gz
RUN cd gnu-arm && ./gnu-arm-build.2.sh

# ---
# default libraries 

RUN apt-get install -y libtool shtool automake autoconf git-core pkg-config make gcc

# ---
# libosmocore
 
RUN git clone git://git.osmocom.org/libosmocore.git
RUN cd libosmocore && autoreconf -i && ./configure && make && make install

# ---
# osmocom-bb

RUN git clone git://git.osmocom.org/osmocom-bb.git
RUN cd osmocom-bb/src && PATH=/gnu-arm/install/bin:$PATH make 

# ---
# osmo-tetra

RUN git clone git://git.osmocom.org/osmo-tetra.git
RUN cd osmo-tetra/src && make 

# ---
# rtl-sdr

RUN git clone git://git.osmocom.org/rtl-sdr.git
RUN apt-get install -y cmake libusb-1.0-0-dev
RUN cd rtl-sdr && mkdir build && cd build && cmake .. && make && make install && ldconfig

# ---
# osmo-sdr

RUN git clone git://git.osmocom.org/osmo-sdr.git
RUN cd osmo-sdr/software/libosmosdr && mkdir build && cd build && cmake .. && make && make install

# ---
# gnuradio
# RUN pass=$(perl -e 'print crypt($ARGV[0], "gnuradio")' $password) && useradd -m -p $pass -s /bin/bash gnuradio && echo 'gnuradio ALL=(ALL:ALL) ALL' >> /etc/sudoers 
# RUN su - gnuradio -c "wget http://www.sbrac.org/files/build-gnuradio && chmod a+x ./build-gnuradio && ./build-gnuradio <<< 'y
# y
# gnuradio
# '"

# ---
# gr-osmosdr

# RUN git clone git://git.osmocom.org/gr-osmosdr
# RUN apt-get install -y libboost-all-dev 
# RUN cd gr-osmosdr && mkdir build && cd build && cmake .. && make && make install

# ---
WORKDIR         /cpuminer
# ENTRYPOINT      ["/bin/bash"]
