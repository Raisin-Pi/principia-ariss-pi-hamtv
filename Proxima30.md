# Proxima-ariss-displaypi

Scripts to allow a Pi to function as a display for the MPEG2/MP2 Transport Stream stripped from the ISS DVB-S by Tutioune.

## Pi Setup

```
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install vim rpi-update openvpn git
sudo git clone https://github.com/philcrump/principia-ariss-pi-hamtv.git
sudo rpi-update
reboot
```

## Install omxplayer from source

```
cd principia-ariss-pi-hamtv
sudo git submodule update --init
cd omxplayer/
sudo apt-get update && sudo apt-get install  subversion libpcre3-dev libidn11-dev libboost1.50-dev libusb-1.0-0-dev libdbus-1-dev libssl-dev libssh-dev libsmbclient-dev gcc-4.7 g++-4.7
sudo ./prepare-native-raspbian.sh
sudo apt-get install smbclient
sudo make ffmpeg
make
sudo make install
```

## Install OpenVG Libraries

```
sudo apt-get install libjpeg8-dev indent libfreetype6-dev ttf-dejavu-core
cd ../openvg/
sudo make
sudo make library
sudo make install
```

## Compile Graphics (only required for new code / new arch)
```
cd ../graphic/
make
```

## Installation

```
[clone git and cd]
sudo cp boot-config.txt /boot/config.txt
sudo cp rc.local /etc/rc.local
```

Edit /etc/rc.local to enable the relevant script (goonhilly/landrover)

```
reboot
```
## Demo Setup

Setup to read a local stream to the video projector

* Download a TS video file to the rpi for demonstration
* Install pv package
```
sudo apt-get install pv
```
* Launch tsplayer.sh on the rpi (will wait for data on 1234 tcp port)
* Launch netcat tcp with the recorded file on the rpi:
```
$ cat Goonhilly\ -\ Bristol.TS | pv -L 2000k | nc 127.0.0.1 1234
```
