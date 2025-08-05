# System

This page details all currently available ROS2 nodes, both core and optional. The main node in the system is Task Manager. This contains the state machine and the comms link to the REST API. The entire system architecture is detailed below, and the state machine is further detailed in [State Machine](statemachine.md).

## Core ROS2 Nodes

### Mission & Flight Management
Core, required nodes.

* [task-manager](https://github.com/robotics-88/task-manager): state machine, receives and processes mission, manages flight controller params
    - *This is where you add new missions*
* [vehicle-launch](https://github.com/robotics-88/vehicle-launch): launch and vehicle config management
    - *This is where you set up new vehicle configs or change perception modules*
* [path_manager](https://github.com/robotics-88/path-manager): takes task manager mission outputs and converts those goals to executable MAVROS setpoints (can be used with or without SLAM &path planner)
    - ***This is where you get to decide how smart the drone really is, at minimum by enabling path planning, up to enabling full decision-making about what constitutes a good destination***

### Data Management
Handles generic cameras, video streaming, and data recording.

* [opencv_cam](https://github.com/robotics-88/opencv_cam): camera manager, starts/stops mp4 recording on arm/disarm, uses Nvidia hardware encoding if available
* [bag_recorder_2](https://github.com/robotics-88/bag_recorder_2): bag recorder, starts/stops ROS2 mcap on arm/disarm
* [image_to_v4l2loopback_ros2](https://github.com/robotics-88/image_to_v4l2loopback_ros2): makes ROS2 image topic available for RTSP streaming

## Optional Nodes

### Mapping

* [fast-lio2](https://github.com/robotics-88/fast-lio2): SLAM for LiDAR
    - Works with Livox and Velodyne/Ouster types 
    - Strongly recommend Livox for cluttered environment, Velodyne/Ouster proved insufficient for detecting small twigs and are so much more expensive and heavy -- Livox is awesome
* [path-planner](https://github.com/robotics-88/path-planner): path planning for LiDAR SLAM registered pointclouds
* [pcl-analysis](https://github.com/robotics-88/pcl-analysis): pointcloud aggregation and filtering, saves .laz file at flight conclusion

### Perception

* [thermal-pipeline](https://github.com/robotics-88/thermal-pipeline): analyzes thermal imagery for fire perimeter and hot spots (with optional NIR fusion to reduce false positives)
* [image-segment](https://github.com/robotics-88/image-segment): (TODO make public) runs ML segmentation model on a ROS2 image topic
* [pcl-analysis](https://github.com/robotics-88/pcl-analysis): (TODO separate this into another node?) detects powerlines and vegetation encroachment

### Sensors
Sensor specific ROS wrappers:

* Livox
    - [Livox-SDK2](https://github.com/Livox-SDK/Livox-SDK2): Livox SDK
    - [livox-ros-driver2](https://github.com/Livox-SDK/livox_ros_driver2): Livox ROS wrapper (ROS1/2)
* [seek-thermal](https://github.com/robotics-88/seek-thermal): ROS2 wrapper for this [thermal camera](https://www.thermal.com/mosaic-core.html)
* [i2c_temperature](https://github.com/robotics-88/i2c_temperature): reads sensor data from [this](https://www.adafruit.com/product/4821)