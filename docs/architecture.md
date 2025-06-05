# System Architecture

## Overview

The Open Drone Stack is composed of:

- A ROS 2-based flight stack
- A REST API server
- A web-based frontend
- A set of modular ROS 2 packages
- Optional simulator and perception modules

## Components

- `task_manager`: handles mission logic
- `drone_rest_server`: provides a RESTful API
- `drone_frontend`: user interface
- `*_nodes`: individual ROS 2 packages for sensors, planning, etc.

## Data Flow

```text
Frontend ──REST──▶ REST Server ──ROS 2 Topics──▶ ROS Nodes
```
