# Missions
Active process that changes the flight behavior. E.g., a lawnmower flight pattern is an industry-standard mission. Trail-following is a somewhat more advanced mission.

## Mission Specification
The mission file must be saved as `mission_name.json` in `task_manager/missions/`. Mission definition examples are provided.

We provide 2 basic starter missions (setpoint, lawnmower), and 1 more advanced (trail_follow). The setpoint mission is `setpoint.json`:

```json
{
  "mission": {
    "name": "SETPOINT"
  },
  "requirements": {
    "perception": {
      "required": ["lidar_slam"],
      "optional": ["obstacle_avoidance"]
    },
    "input_geometry": "point"
  }
}
```

Note that the mission name must be unique, and must match the enum label in Task Manager. Also note the required versus optional perception. Technically, all perception modules can optionally be run with any mission. This field should only be used for perception that changes the mission behavior when enabled. Input geometry tells the frontend what to require before sending the mission. Options are `point` and `polygon`. Compare with the trail following mission, `trail_follow.json`:

```json
{
  "mission": {
    "name": "TRAIL_FOLLOW"
  },
  "requirements": {
    "perception": {
      "required": ["lidar_slam", 
                  "obstacle_avoidance", 
                  "trail_detection"]
    },
    "input_geometry": ""
  }
}
```

## Task Manager Integration

Missions must be integrated into Task Manager so the state machine is aware of them. The frontend will be notified by Task Manager as long as the above-defined mission config file is present, as Task Manager searches that folder. However, even if sent by the frontend, TM won't do anything with this mission unless you do the following.

1. Add mission name to TaskManager::MissionType enum in `task_manager/include/task_manager/task_manager.h` (must match the name of the config file! e.g. `setpoint.json` and `MissionType::SETPOINT`)
2. Add switch for the new enum in TaskManager::switchMission() in `task_manager/src/task_manager.cpp`
3. Add mission method called within switch, defining the method as `TaskManager::handleMissionName` (if adding your own ROS package in the optional step below, this is where the service start or callback publisher should be sent from)

## (Optional) Add Mission Capability ROS Package

Simple missions can be contained entirely within Task Manager methods. However, for anything beyond the most basic functionality, a new package should be created. There is significantly more flexibility with this approach. Your ROS2 package should provide a service or callback which is activated by the corresponding TM method. Beyond that, you must also:

1. Add package to `open-drone-core/src/decco.repos`
2. Add package launch to `vehicle_launch/launch/opendrone.launch.py`