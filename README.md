
# DECADA - Robotics - Middleware Framework (RMF)
The OpenRMF platform from open-rmf for multi-fleet robot management, modified for Decada Robotics.

---
## Install ROS 2 Galactic

First, please follow the installation instructions for ROS 2 Galactic.
If you are on an Ubuntu 20.04 LTS machine (as recommended), [here is the binary install page for ROS 2 Galactic on Ubuntu 20.04](https://docs.ros.org/en/galactic/Installation/Ubuntu-Install-Debians.html).

## Setup Gazebo repositories

Setup your computer to accept Gazebo packages from packages.osrfoundation.org.

```bash
sudo apt update
sudo apt install -y wget
sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
wget https://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
```

## Building from sources (what we did)

If you want to get the latest developments you might want to install from sources and compile OpenRMF yourself.


### Additional Dependencies

Install all non-ROS dependencies of OpenRMF packages,

```bash
sudo apt update && sudo apt install \
  git cmake python3-vcstool curl \
  qt5-default \
  -y
python3 -m pip install flask-socketio
sudo apt-get install python3-colcon*
```

### Install rosdep

`rosdep` helps install dependencies for ROS packages across various distros. It can be installed with:

```bash
sudo apt install python3-rosdep
sudo rosdep init
rosdep update
```

### Download the source code
Setup a new ROS 2 workspace and pull in the demo repositories using `vcs`,

```bash
mkdir -p ~/rmf_ws/src
cd ~/rmf_ws
wget https://raw.githubusercontent.com/siot-decada-robotics/rmf/siot/trl_rmf.repos
vcs import src < trl_rmf.repos
```

Ensure all ROS 2 prerequisites are fulfilled,
```
cd ~/rmf_ws
rosdep install --from-paths src --ignore-src --rosdistro galactic -y
```

### Compiling Instructions

On `Ubuntu 20.04`:

```bash
cd ~/rmf_ws
source /opt/ros/galactic/setup.bash
colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release
```

> NOTE: The first time the build occurs, many simulation models will be downloaded from Ignition Fuel to populate the scene when the simulation is run.
As a result, the first build can take a very long time depending on the server load and your Internet connection (for example, 60 minutes).

## Run RMF Demos

Demonstrations of OpenRMF are shown in [rmf_demos](https://github.com/siot-decada-robotics/rmf_demos/).



## Roadmap

A near-term roadmap of the entire OpenRMF project (including and beyond `rmf_traffic`) can be found in the user manual [here](https://osrf.github.io/ros2multirobotbook/roadmap.html).

## Integrating with RMF

Instructions on how to integrate your system with OpenRMF can be found [here](https://osrf.github.io/ros2multirobotbook/integration.html).
