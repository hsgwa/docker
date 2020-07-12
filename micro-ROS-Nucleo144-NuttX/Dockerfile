FROM microros/base:dashing

WORKDIR /uros_ws

RUN apt update && apt install -y ed flex bison libncurses5-dev gcc-arm-none-eabi clang clang-tidy usbutils gperf openocd automake

SHELL ["/bin/bash", "-c"]

RUN . /micro-ros_entrypoint.sh && \
	ros2 run micro_ros_setup create_firmware_ws.sh nuttx nucleo-144 && \
	ros2 run micro_ros_setup configure_firmware.sh f767-netnsh

RUN git clone https://bitbucket.org/nuttx/tools.git ~/tools
RUN (cd ~/tools/kconfig-frontends && \
        ./configure --enable-mconf --disable-nconf --disable-gconf --disable-qconf && \
        LD_RUN_PATH=/usr/local/lib && make && make install && ldconfig)

RUN cd firmware/NuttX && \
    tools/configure.sh configs/nucleo-144/f767-netnsh && \
    cd ../..
