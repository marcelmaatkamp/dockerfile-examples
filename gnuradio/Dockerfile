FROM ubuntu:14.04

MAINTAINER m.maatkamp@gmail.com version: 0.1

RUN apt-get update
RUN apt-get dist-upgrade -yf
RUN apt-get clean
RUN apt-get autoremove

RUN apt-get install -y git subversion axel wget zip unzip 

# --- 
RUN wget http://www.sbrac.org/files/build-gnuradio && chmod a+x ./build-gnuradio && printf "y\ny\ny\n" | ./build-gnuradio
RUN "export PYTHONPATH=/usr/local/lib/python2.7/dist-packages" > ~/.bashrc

RUN svn co https://www.cgran.org/svn/projects/multimode
RUN cd multimode/trunk && make install

WORKDIR         /
# ENTRYPOINT      ["/bin/bash"]
