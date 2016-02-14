This docker image contains the latest build from osmocombb and its subprojects:

- osmocombb
- rtl-sdr
-osmo-tetra

Tested Docker host environments are:

- Ubuntu 
- CoreOS
- Mac

To run, simply use the following command-line:

    $ docker run -t -i --privileged -v /dev/bus/usb:/dev/bus/usb marcelmaatkamp/osmocombb /bin/bash

Then insert a rtl_sdr dongle and test it with:

    $ rtl_test
 
    Found 1 device(s):
    0:  Realtek, RTL2838UHIDIR, SN: 00000001
    Using device 0: Generic RTL2832U OEM
    Found Elonics E4000 tuner

    $ rtl_adsb

    Found 1 device(s):
    0:  Realtek, RTL2838UHIDIR, SN: 00000001
    Using device 0: Generic RTL2832U OEM
    Found Elonics E4000 tuner
    Tuner gain set to automatic.
    Tuned to 1090000000 Hz.
    Exact sample rate is: 2000000.052982 Hz
    Sampling at 2000000 S/s.


To use the osmocombb version:

    $ cd osmocom-bb/src/host/layer23/src/mobile/
    $ ./mobile -i 127.0.0.1

Should you get an error about the driver already being claimed, exit docker and add a blacklist in the host environment:

    $ sudo su -e "echo 'blacklist dvb_usb_rtl28xxu' >> /etc/modprobe.d/blacklist.conf"
    $ sudo update-initramfs -u
    $ sudo reboot

.. and try again.
   
Dockerfile can be found at [https://github.com/marcelmaatkamp/dockerfile-examples/tree/master/osmocombb/osmocombb-base][1]

  [1]: https://github.com/marcelmaatkamp/dockerfile-examples/tree/master/osmocombb/osmocombb-base
