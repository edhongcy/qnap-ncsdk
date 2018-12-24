FROM bobthesheep/ncsdk_container
LABEL maintainer="edhongcy@gmail.com"

USER root
VOLUME ["/dev/bus/usb:/dev/bus/usb:shared"]

RUN apt-get update \
    && apt-get -y install libtool apt-utils \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

#Install libusb#
RUN cd /tmp \
    && wget https://github.com/libusb/libusb/archive/v1.0.22.zip \
    && unzip v1.0.22.zip \
    && cd libusb-1.0.22 \
    && ./bootstrap.sh \
    && ./configure --disable-udev --enable-shared \
    && make && make install \
    && cd / && rm -rf /tmp/v1.0.22.zip /tmp/libusb-1.0.22

RUN apt-get update \
    && apt-get upgrade -y

CMD ["/bin/bash"]
