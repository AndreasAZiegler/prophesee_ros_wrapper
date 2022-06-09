FROM osrf/ros:noetic-desktop

# Get dependencies
RUN apt-get update && apt-get install -y git gdb cmake-curses-gui

# Get ROS dependencies
RUN apt-get install -y python3-vcstool python3-catkin-tools python3-osrf-pycommon ros-noetic-rqt*

# Install OpenEB
#RUN apt -y install apt-utils build-essential software-properties-common wget unzip curl
#RUN apt -y install cmake libopencv-dev git
#RUN apt -y install libboost-all-dev libusb-1.0-0-dev libeigen3-dev
#RUN apt -y install libglew-dev libglfw3-dev
#RUN apt -y install libgtest-dev
#RUN apt -y install python3-pip python3-distutils  # the python package installer
#RUN python3 -m pip install pip --upgrade  # upgrade pip
#RUN python3 -m pip install "numpy==1.19.5" "opencv-python>=4.2.0.34" pytest

#RUN cd ~ && \
#    git clone https://github.com/prophesee-ai/openeb.git && \
#    cd openeb && \
#    mkdir build && cd build && \
#    cmake .. -DBUILD_TESTING=OFF -DCOMPILE_PYTHON3_BINDINGS=OFF && \
#    cmake --build . --config Release -- -j && \
#    cmake --build . --target install

#ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib

# Install metavision
RUN apt-get install -y libcanberra-gtk-module mesa-utils ffmpeg
RUN apt-get install -y cmake libboost-program-options-dev libeigen3-dev
RUN apt-get install -y python3-pip python3-tk
RUN apt-get install -y python3.8-dev
RUN python3 -m pip install pip --upgrade
RUN python3 -m pip install "opencv-python>=4.5.5.64" "sk-video==1.1.10" "fire==0.4.0" "numpy<=1.21" pandas scipy h5py
RUN python3 -m pip install jupyter jupyterlab matplotlib "ipywidgets==7.6.5"

ADD metavision.list /etc/apt/sources.list.d/metavision.list
RUN apt-get update && apt-get install -y metavision-sdk

# Install profiling tools
RUN apt-get update && apt-get install -y linux-tools-generic hotspot
RUN rm /usr/bin/perf
RUN ln -s /usr/lib/linux-tools/5.4.0-80-generic/perf /usr/bin/perf

# Add utility scripts
RUN apt -y install jq
ADD merge-compile-commands /usr/local/bin/merge-compile-commands
RUN chmod +x /usr/local/bin/merge-compile-commands

ADD catkin-update-compile-commands /usr/local/bin/catkin-update-compile-commands
RUN chmod +x /usr/local/bin/catkin-update-compile-commands
