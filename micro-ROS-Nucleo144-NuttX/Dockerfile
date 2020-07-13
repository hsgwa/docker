FROM microros/base:dashing

WORKDIR /uros_ws

RUN apt update && apt install -y ed flex bison libncurses5-dev gcc-arm-none-eabi clang clang-tidy usbutils gperf  automake libtool libusb-1.0-0-dev


# install kconfig-frontends 
RUN git clone https://bitbucket.org/nuttx/tools.git ~/tools
RUN (cd ~/tools/kconfig-frontends && \
        ./configure --enable-mconf --disable-nconf --disable-gconf --disable-qconf && \
        LD_RUN_PATH=/usr/local/lib && make && make install && ldconfig)

# install latest OpenOCD
RUN cd /tmp && \
	git clone https://github.com/ntfreak/openocd.git && \
	cd /tmp/openocd && \
	./bootstrap && \
 	./configure && \
	make && \
	make install && cd /uros_ws


SHELL ["/bin/bash", "-c"]

RUN . /micro-ros_entrypoint.sh && \
	ros2 run micro_ros_setup create_firmware_ws.sh nuttx nucleo-144
