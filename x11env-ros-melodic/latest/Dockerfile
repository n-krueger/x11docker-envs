FROM ros:melodic-ros-base-bionic

# XFCE desktop setup taken from https://github.com/mviereck/dockerfile-x11docker-xfce
RUN apt-get update && apt-mark hold iptables && \
    env DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
      libpulse0 \
      libxv1 \
      mesa-utils \
      mesa-utils-extra \
      va-driver-all

# ros:melodic-ros-base-bionic understandably does not include the full desktop package
RUN apt-get update && apt-get install -y \
    ros-melodic-desktop-full

CMD ["/bin/bash"]
