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

# Copy the point_labeler repository
COPY /files/point_labeler /root/point_labeler

WORKDIR /root/point_labeler
RUN cmake -S . -B build
RUN cmake --build build

# Add aliases to the bashrc
RUN echo "alias labeler='cd /root/point_labeler/bin && ./labeler'" >> ~/.bashrc

WORKDIR /root