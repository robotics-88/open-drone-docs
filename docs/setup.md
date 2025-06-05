# Setup Guide

## Prerequisites

- Ubuntu 22.04
- ROS 2 Humble
- `colcon`, `vcs`, `python3-pip`
- Git

## Clone and Build

```bash
sudo apt install python3-colcon-common-extensions python3-vcstool
git clone https://github.com/robotics-88/open-drone-stack.git
cd open-drone-stack
vcs import < drone.repos
rosdep install --from-paths src --ignore-src -r -y
colcon build
```

## Launch

```bash
source install/setup.bash
ros2 launch task_manager bringup.launch.py
```
