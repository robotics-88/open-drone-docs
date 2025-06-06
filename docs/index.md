# Open Drone Stack

Welcome to the Open Drone Stack — a modular, ROS2-based system for autonomous drones. The full stack includes not only the ROS code to provide drone autonomy, but also a basic frontend and the on-drone server connection. Follow the complete [setup guide](setup.md) to use our stack as is, or jump to [development](development/index.md) to start modifying for your needs!

## Overview

The Open Drone Stack is composed of:

- A ROS 2-based flight stack
- A REST API server on drone
- A web-based frontend
- A set of modular ROS 2 packages
- Optional simulator for SITL testing

### Components

- `task_manager`: handles mission logic
- `drone_rest_server`: provides a RESTful API
- `drone_frontend`: user interface
- `*_nodes`: individual ROS 2 packages for sensors, planning, etc.

### Data Flow

```text
Frontend ──REST──▶ REST Server ──ROS 2 Topics──▶ ROS Nodes
```

## development
The ROS flight stack is modular, so e.g. you can swap out your own SLAM algorithm or path planner. Additional modules can be added as well. We'd love for someone to add reactive obstacle avoidance to the path manager!

This site contains setup instructions, usage examples, architecture details, and more.

➡️ To get started, head to the [Setup Guide](setup.md).
