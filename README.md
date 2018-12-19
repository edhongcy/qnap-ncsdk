# qnap-ncsdk

This project is run ncsdk on QNAP NAS.

Docker hub:
https://hub.docker.com/r/edhongcy/qnap-ncsdk/

Docker run sdk:
```
docker run -u root --rm --net=host -it --privileged -v /dev/bus/usb:/dev/bus/usb:shared edhongcy/qnap-ncsdk /bin/bash
```
