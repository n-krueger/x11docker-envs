# x11docker-envs
This is a collection of Docker-based development environments that require involved setup or
target a specific OS. The goal is to provide images that are immediately ready to be used
regardless of what OS is used as the host.

## Prerequisites
* Docker >= 19.03 (distributions often package Docker, e.g. `docker.io` in debian, otherwise get Docker-CE here: https://docs.docker.com/engine/install/)
* x11docker >= 6.0.0 (https://github.com/mviereck/x11docker#installation)
* Python >= 3.6

## Usage
### x11envs management tool

List environments that are available for installation (x marks whether the environment is installed):
```bash
$ ./x11envs list available
ENV                       PRESET     IMAGE      ADDONS
x11env-ros-melodic:latest x          x          
x11env-ros-melodic:carla                             
```

List environments that are currently installed (x marks whether the environment is installed):
```bash
$ ./x11envs list installed
ENV                       PRESET     IMAGE      ADDONS
x11env-ros-melodic:latest x          x          
```

Install an environment:
```bash
$ ./x11envs install x11env-ros-melodic:carla
...docker build output...
```

Run an environment (this will run `bash` inside the container):
```bash
$ x11docker --preset x11env-ros-melodic:carla
...x11docker output...
```
Often you will want to have a second terminal inside the environment. Use `docker exec` to achieve this:
```bash
$ docker container ls
CONTAINER ID        IMAGE                      COMMAND                  CREATED             STATUS              PORTS               NAMES
a487c79a2f7b        x11env-ros-melodic:carla   "env /usr/local/bin/…"   12 minutes ago      Up 12 minutes                           x11docker_X1_x11env-ros-melodic-carla_42924550588
$ docker exec -it a487c79a2f7b /ros_entrypoint.sh bash
```

Remove an environment:
```bash
$ ./x11envs remove x11env-ros-melodic:carla
```

### Development environment
The following examples use `🤖` instead of `$` as the prefix to indicate that
we are using `bash` inside the ROS container.

```bash
🤖 roscore
```
```bash
🤖 rosrun turtlesim turtlesim_node
```
```bash
🤖 cd /opt/carla-simulator/
🤖 ./bin/CarlaUE4.sh
```

### sudo password in the development environment
Some applications like CARLA-Simulator need access to `sudo`. In environments with applications that need `sudo`,
the password is `x11docker`, otherwise `sudo` is not available. This is to discourage using it to install packages,
as these modifications will be lost when the container restarts. Only the content in the home directory of the
container is preserved.

### Accessing files from the development environment from the host
The home directories of development environments are mounted to `~/x11docker/<environment_name>`. For 
`x11env-ros-melodic:carla` that would be `~/x11docker/x11env-ros-melodic:carla`.

### NVIDIA GPU acceleration
Utilizing NVIDIA GPUs requires the NVIDIA drivers to be installed inside the development environment. The x11docker
wiki explains how to achieve this: https://github.com/mviereck/x11docker/wiki/NVIDIA-driver-support-for-docker-container#automated-install-of-nvidia-driver-during-container-startup

## Addons
COMING SOON
