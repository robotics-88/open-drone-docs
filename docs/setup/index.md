# Setup Guide

The flight stack can be tested with physical hardware or entirely in simulation. (point to hardware and sim docs)

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


