FROM x11env-ros-melodic:latest

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 92635A407F7A020C
RUN echo "deb [arch=amd64 trusted=yes] http://dist.carla.org/carla-0.9.9/ all main" > /etc/apt/sources.list.d/carla-0-9-9.list
RUN apt-get update && apt-get install -y \
    carla-simulator
