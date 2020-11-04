FROM rosindustrial/tesseract:noetic

RUN apt update && \
    apt install -y git \
    python3-catkin-tools \
    python3-rosdep \
    python3-rosinstall-generator \
    python3-vcstool \
    python3-pip \
    build-essential \
    bison \
    ros-noetic-catkin \
    ros-noetic-rqt \
    ros-noetic-pcl-ros \
    ros-noetic-moveit \
    ros-noetic-ifopt \
    ros-noetic-octomap-ros \
    ros-noetic-ros-control \
    ros-noetic-ros-controllers \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install catkin_tools

RUN mkdir -p /dev_ws/src
WORKDIR /dev_ws/src

RUN git clone https://github.com/ros-industrial-consortium/tesseract.git && \
    git clone https://github.com/ros-industrial-consortium/tesseract_ros.git && \
    git clone https://github.com/grdwyer/iiwa_fri_description.git


WORKDIR /dev_ws

RUN ["/bin/bash", "-c", "source /opt/ros/noetic/setup.bash &&\
    wstool init src &&\
    catkin init &&\
    catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release &&\
    cd src &&\
    wstool merge ./tesseract/dependencies.rosinstall &&\
    wstool up &&\
    catkin build"]
