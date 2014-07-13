FROM ubuntu:14.04

MAINTAINER m.maatkamp@gmail.com version: 0.1

RUN apt-get update
RUN apt-get dist-upgrade -yf
RUN apt-get clean
RUN apt-get autoremove

RUN apt-get install -y git subversion axel wget zip unzip 

# --- 
RUN apt-get -y install git-core cmake g++ python-dev swig pkg-config libfftw3-dev libboost1.53-all-dev libcppunit-dev libgsl0-dev libusb-dev libsdl1.2-dev python-wxgtk2.8 python-numpy python-cheetah python-lxml doxygen libxi-dev python-sip libqt4-opengl-dev libqwt-dev libfontconfig1-dev libxrender-dev libgruel3.6.1
RUN apt-get -y remove python-qwt5-qt4
RUN apt-get install python-sip python-sip-dev
RUN mkdir -p /opt/qt
RUN echo "export PATH=/opt/qt/bin:$PATH" >> ~/.bashrc
RUN echo "export LD_LIBRARY_PATH=/opt/qt/lib:/usr/local/lib:$LD_LIBRARY_PATH" >> ~/.bashrc
RUN echo "export PYTHONPATH=/opt/qt/lib/python2.7/dist-packages:$PYTHONPATH" >> ~/.bashrc
RUN echo "export PKG_CONFIG_PATH=/opt/qt/lib/pkgconfig:$PKG_CONFIG_PATH" >> ~/.bashrc
RUN source ~/.bashrc

# ---
RUN mkdir -p pyqt
RUN cd pyqt && wget http://sourceforge.net/projects/pyqt/files/PyQt4/PyQt-4.11.1/PyQt-x11-gpl-4.11.1.tar.gz
RUN cd pyqt && tar zxpPvf PyQt-x11-gpl-4.11.1.tar.gz
RUN cd pyqt/PyQt-x11-gpl-4.11.1 && python configure.py -b /opt/qt/bin -d /opt/qt/lib/python2.7/dist-packages -v /opt/qt/share/sip
RUN cd pyqt/PyQt-x11-gpl-4.11.1 && make && make install 

# ---
RUN cd pyqt && wget "http://downloads.sourceforge.net/project/pyqwt/pyqwt5/PyQwt-5.2.0/PyQwt-5.2.0.tar.gz?r=http%3A%2F%2Fpyqwt.sourceforge.net%2Fdownload.html&ts=1405252089&use_mirror=skylink"

WORKDIR         /
# ENTRYPOINT      ["/bin/bash"]
