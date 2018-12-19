FROM ubuntu:16.04
LABEL maintainer="edhongcy@gmail.com"

USER root
VOLUME ["/dev/bus/usb:/dev/bus/usb:shared"]

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y build-essential git lsb-release sudo udev usbutils wget libtool apt-utils pyhton3-pip \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

#Build movidius

WORKDIR /root
RUN wget https://github.com/lhelontra/tensorflow-on-arm/releases/download/v1.4.0/tensorflow-1.4.0-cp35-none-linux_aarch64.whl
RUN pip3 install /root/tensorflow-1.4.0-cp35-none-linux_aarch64.whl
RUN git clone https://github.com/HanYangZhao/ncsdk.git
WORKDIR /root/ncsdk
RUN make install
RUN udevadm trigger
RUN usermod -a -G users root

#Install libusb
RUN cd /tmp \
    && wget https://github.com/libusb/libusb/archive/v1.0.22.zip \
    && unzip v1.0.22.zip \
    && cd libusb-1.0.22 \
    && ./bootstrap.sh \
    && ./configure --disable-udev --enable-shared \
    && make && make install \
    && cd / && rm -rf /tmp/v1.0.22.zip /tmp/libusb-1.0.22

#Create libusb link
RUN ln -sf /usr/local/lib/libusb-1.0.so.0.1.0 /lib/aarch64-linux-gnu/libusb-1.0.so.0

CMD ["/bin/bash"]
