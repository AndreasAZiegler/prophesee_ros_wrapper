FROM osrf/ros:noetic-desktop

# Get dependencies
RUN apt-get update && apt-get install -y python3-vcstool python3-catkin-tools python3-osrf-pycommon git

# Get ROS dependencies
RUN apt-get install -y ros-noetic-rqt*

# Install OpenEB
RUN apt -y install apt-utils build-essential software-properties-common wget unzip curl
RUN apt -y install cmake  libopencv-dev git # CMake, OpenCV, and Git
RUN apt -y install libboost-all-dev libboost-program-options-dev libusb-1.0-0-dev libeigen3-dev # Boost, Libusb and eigen3
RUN apt -y install libglew-dev libglfw3-dev
RUN apt -y install libgtest-dev  # gtest
RUN apt -y install libcanberra-gtk-module mesa-utils
RUN apt -y install python3-pip python3-distutils  # the python package installer
RUN python3 -m pip install pip --upgrade  # upgrade pip
RUN python3 -m pip install pytest "numpy==1.19.5"

RUN cd ~ && \
    git clone https://github.com/prophesee-ai/openeb.git && \
    cd openeb && \
    mkdir build && cd build && \
    cmake .. -DBUILD_TESTING=OFF -DCOMPILE_PYTHON3_BINDINGS=OFF && \
    cmake --build . --config Release -- -j && \
    cmake --build . --target install

ADD essentials.list /etc/apt/sources.list.d/essentials.list
RUN apt-get update && apt-get install -y metavision-*

# Add utility scripts
ADD merge-compile-commands /usr/local/bin/merge-compile-commands
RUN chmod +x /usr/local/bin/merge-compile-commands

ADD catkin-update-compile-commands /usr/local/bin/catkin-update-compile-commands
RUN chmod +x /usr/local/bin/catkin-update-compile-commands
