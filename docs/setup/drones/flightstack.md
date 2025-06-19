# Flight Stack Setup

If you've confirmed your hardware is compatible, the next step is configuring core software.

## ROS2 Workspace
This will clone everything assuming a brand new Jetson, including installing ROS2, with the assumption we are running Ubuntu 22.
```
cd
mkdir src
cd src
git clone https://github.com/robotics-88/open-drone-core.git
cd open-drone-core
./setup-workspace.sh
colcon build
source ~/.bashrc
```

## Systemd Service

Technically optional, but it makes things simpler for flight tests. TODO deets.