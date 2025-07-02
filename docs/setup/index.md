# Setup Guide

The flight stack can be tested with physical hardware or entirely in simulation. For hardware setup, start [here](drones/index.md). For simulation setup, start [here](simulation/index.md). If you are going to integrate the stack on a custom drone, we recommend starting with simulation setup to verify your configuration, then proceed to [Custom](custom/index.md).

## Prerequisites
The machine where the flight stack runs, on drone or in sim on a computer, must be running Ubuntu 22.04. All dependent software including ROS2 will be installed with the setup script. To summarize, we require:

- Ubuntu 22.04
- ROS 2 Humble
- `colcon`, `vcs`, `python3-pip`
- Git

!!! info
    Future work: upgrade to ROS2 Kilted.

## Setup Overview
Open drone setup includes cloning the ROS2 workspace, setting up a sim environment, and launching for the first time. If using the frontend, you can proceed to launching your first setpoint mission through the map interface. If you are setting up a physical vehicle of your own, there is additional vehicle config setup.

### Vehicle Configs

The system is built to automatically launch all perception features enabled by the types of sensors on your vehicle. For that to be possible, you must set up a config file as described [here](drones/config.md).