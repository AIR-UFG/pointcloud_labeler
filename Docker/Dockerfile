# Credits to Armin Niedermueller (@nerovalerius) for the Instructions
# https://gist.github.com/nerovalerius/80133f409f9ed0573522432244298195

# Use the official ROS humble-desktop-full image
FROM osrf/ros:humble-desktop-full

ARG DEBIAN_FRONTEND=noninteractive

# Add the GTSAM PPA to the package manager
RUN echo "deb http://ppa.launchpad.net/borglab/gtsam-release-4.2/ubuntu jammy main" | sudo tee -a /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-key 4545AE2E66D6266DA83C8DF9E67B3C12ACDAD9C5

# Update package list and install required packages
RUN apt update && \
    apt install -y \
    python3-pip \
    qt5-gtk2-platformtheme \
    nano \
    libgtsam-dev \
    libgtsam-unstable-dev && \
    rm -rf /var/lib/apt/lists/*

# Install catkin
RUN pip install catkin_tools catkin_tools_fetch empy

# Create a catkin workspace
WORKDIR /root/catkin_ws
RUN catkin init

WORKDIR /root/catkin_ws/src
# Clone the catkin repository
RUN git clone https://github.com/ros/catkin.git
# Clone the point_labeler repository into the catkin workspace
RUN git clone https://github.com/jbehley/point_labeler.git
# Clone the SuMa repository
RUN git clone https://github.com/jbehley/SuMa.git

# Fetch dependencies
RUN catkin deps fetch
# Build the packages
RUN catkin build --save-config -i --cmake-args -DCMAKE_BUILD_TYPE=Release -DOPENGL_VERSION=450 -DENABLE_NVIDIA_EXT=YES

# Change settings to velodyne vlp16 as default
RUN mv /root/catkin_ws/src/SuMa/config/default.xml /root/catkin_ws/src/SuMa/config/defaultBKP && \
    mv /root/catkin_ws/src/SuMa/config/vlp16_example.xml /root/catkin_ws/src/SuMa/config/default.xml

# Create the KITTI dataset directory structure
RUN mkdir -p /root/dataset/sequences/00/velodyne && \
    mkdir -p /root/dataset/sequences/00/labels

# Create the KITTI calibration file
RUN echo -e "P0: 1 0 0 0 0 1 0 0 0 0 1 0\n\
P1: 1 0 0 0 0 1 0 0 0 0 1 0\n\
P2: 1 0 0 0 0 1 0 0 0 0 1 0\n\
P3: 1 0 0 0 0 1 0 0 0 0 1 0\n\
Tr: 1 0 0 0 0 1 0 0 0 0 1 0" > /root/dataset/sequences/00/calib.txt

# Add aliases to the bashrc
RUN echo "alias visualizer='cd /root/catkin_ws/src/SuMa/bin && ./visualizer'" >> ~/.bashrc && \
    echo "alias labeler='cd /root/catkin_ws/src/point_labeler/bin && ./labeler'" >> ~/.bashrc

WORKDIR /root