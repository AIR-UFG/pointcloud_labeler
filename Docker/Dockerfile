# Use the official Ubuntu image
FROM ubuntu:22.04

ARG DEBIAN_FRONTEND=noninteractive

# Update package list and install required packages
RUN apt update && \
    apt install -y \
    g++ \
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

# Copy the kiss-icp repository
COPY /files/kiss-icp /root/kiss-icp

# Build the kiss-icp library
WORKDIR /root/kiss-icp
RUN make editable

# Install the polyscope library (for visualization)
RUN pip install polyscope

# Copy the point_labeler repository
COPY /files/point_labeler /root/point_labeler

WORKDIR /root/point_labeler
RUN cmake -S . -B build
RUN cmake --build build

# Create the KITTI dataset directory structure
RUN mkdir -p /root/dataset/sequences/00/velodyne && \
    mkdir -p /root/dataset/sequences/00/labels

# Copy the KITTI calibration file
COPY /files/calib.txt /root/dataset/sequences/00/calib.txt

# Add aliases to the bashrc
RUN echo "alias labeler='cd /root/point_labeler/bin && ./labeler'" >> ~/.bashrc

WORKDIR /root