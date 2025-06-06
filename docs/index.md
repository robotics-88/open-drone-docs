# Open Drone Stack

Welcome to the Open Drone Stack — a modular, ROS2-based system for autonomous drones. The full stack includes not only the ROS code to provide drone autonomy, but also a basic frontend and the on-drone server connection. Follow the complete [setup guide](setup/index.md) to use our stack as is, or jump to [development](development/index.md) to start modifying for your needs!

## overview

The Open Drone Stack is composed of:

- A ROS 2-based flight stack
- A REST API server on drone
- A web-based frontend
- A set of modular ROS 2 packages
- Optional simulator for SITL testing

### primary repos

- [`open-drone-core`](https://github.com/robotics-88/open-drone-core): main point of access for ROS2 flight stack
- [`open-drone-server`](https://github.com/robotics-88/open-drone-server): provides a RESTful API on the drone
- [`open-drone-frontend`](https://github.com/robotics-88/open-drone-frontend): web app, map-based user interface

#### ROS2 flight stack

The 2 most critical repos are [task-manager](https://github.com/robotics-88/task-manager) and [vehicle-launch](https://github.com/robotics-88/vehicle-launch). Everything else in the stack is technically optional, but these are required for basic node and mission startup. However, to make the most use of the stack, we recommend at minimum the following:

* [task-manager](https://github.com/robotics-88/task-manager): state machine, receives and executes mission, manages flight controller
    - *This is where you add new missions*
* [vehicle-launch](https://github.com/robotics-88/vehicle-launch): launch and vehicle config management
    - *This is where you set up new vehicle configs or change perception modules*
* [opencv_cam](https://github.com/robotics-88/opencv_cam): camera manager, starts/stops mp4 recording on arm/disarm
* [bag_recorder_2](https://github.com/robotics-88/bag_recorder_2): bag recorder, starts/stops ROS2 mcap on arm/disarm
* [image_to_v4l2loopback_ros2](https://github.com/robotics-88/image_to_v4l2loopback_ros2): makes ROS2 image topic available for RTSP streaming

Setup for additional perception capabilities such as SLAM, path planning, exploration, thermal image processing, and more are detailed in the [setup guide](setup/index.md).

### Data Flow

```text
Frontend ──REST──▶ REST Server ──ROS 2 Topics──▶ ROS Nodes
```

## development
The ROS flight stack is modular, so e.g. you can swap out your own SLAM algorithm or path planner. Additional modules can be added as well. We'd love for someone to add reactive obstacle avoidance to the path manager!

This site contains setup instructions, usage examples, architecture details, and more.

➡️ To get started, head to the [Setup Guide](setup/index.md).
