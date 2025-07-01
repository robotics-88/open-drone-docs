# Missions

## Mission Specification
The mission file must be saved as `mission_name.json` in `task_manager/missions/`. Mission definition examples are provided.

We provide 2 basic starter missions (setpoint, lawnmower), and 1 more advanced (trail_follow). The setpoint mission is:

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

Note that the mission name must be unique, and must match the enum label in Task Manager. Also note the required versus optional perception. Technically, all perception modules can optionally be run with any mission. This field should only be used for perception that changes the mission behavior when enabled. Input geometry tells the frontend what to require before sending the mission. Options are `point` and `polygon`. Compare with the trail following mission:

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

## Mission Integration

Missions must be integrated into Task Manager so the state machine is aware of them. The frontend will be notified by Task Manager simply because the mission config file is present, as Task Manager searches that folder.

!!! note
    TODO add deets on integrating with TM