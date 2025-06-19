# Quick Start

## Single Script Setup

There is a support script to install, build, and launch everything at once.

```bash
cd open-drone-core
./quickstart.sh
```

This brings up Gazebo, ArduCopter, ROS2 nodes, and the frontend, even if you start from a fresh Ubuntu install without ROS2. Should look like this when launching is complete:

![Quickstart Complete](images/quickstart.png)

## Test Setpoint Mission

Send your first setpoint mission from the frontend at [http://127.0.0.1:8040/](http://127.0.0.1:8040/) by setting the IP in the Mission Panel to localhost and dropping a pin on the map. Watch the drone take off in Rviz or Gazebo.

![Setpoint Mission](images/firstsetpoint.png)