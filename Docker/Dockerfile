# Use the official Ubuntu image
FROM ubuntu:22.04

ARG DEBIAN_FRONTEND=noninteractive

# Update package list and install required packages
RUN apt update && \
    apt install -y \
    python3-pip \
    git \
    nano \
    build-essential \
    cmake \
    libeigen3-dev \
    libboost-all-dev \
    qtbase5-dev \
    libglew-dev && \
    rm -rf /var/lib/apt/lists/*

# Install catkin
RUN pip install catkin_tools catkin_tools_fetch empy

# Copy the SuMa repository
COPY /files/SuMa /root/SuMa

# Change settings to velodyne vlp16 as default
RUN mv /root/SuMa/config/default.xml /root/SuMa/config/HDL-64E && \
    mv /root/SuMa/config/vlp16_example.xml /root/SuMa/config/default.xml

# Build the SuMa project
WORKDIR /root/SuMa/build
RUN cmake .. -DCMAKE_BUILD_TYPE=Release -DOPENGL_VERSION=450 -DENABLE_NVIDIA_EXT=YES
RUN make

# Copy the point_labeler repository
COPY /files/point_labeler /root/point_labeler

WORKDIR /root/point_labeler
RUN cmake -S . -B build
RUN cmake --build build

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
RUN echo "alias visualizer='cd /root/SuMa/bin && ./visualizer'" >> ~/.bashrc && \
    echo "alias labeler='cd /root/point_labeler/bin && ./labeler'" >> ~/.bashrc

WORKDIR /root