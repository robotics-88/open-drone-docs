# Usage

## Starting the Stack

1. Build and source the workspace:

```bash
colcon build
source install/setup.bash
```

2. Launch the full system:

```bash
ros2 launch task_manager bringup.launch.py
```

## Example Mission

```bash
curl -X POST http://localhost:8000/mission   -H "Content-Type: application/json"   -d '{"type": "lawnmower", "geometry": {...}}'
```
