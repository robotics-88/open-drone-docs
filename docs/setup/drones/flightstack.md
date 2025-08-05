# Flight Stack Setup

If you've confirmed your hardware is compatible, the next step is configuring core software. Note that [Quickstart](../../quickstart.md) provides instructions on using the setup script for a drone, which installs everything required for the complete integrated system on a drone. Instructions repeated below.

## ROS2 Workspace
This will clone everything assuming a brand new Jetson, including installing ROS2, with the assumption we are running Ubuntu 22.
```
cd
mkdir src
cd src
git clone https://github.com/robotics-88/open-drone-core.git
cd open-drone-core
./scripts/setup-drone.sh
source ~/.bashrc
```
