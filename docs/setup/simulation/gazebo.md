# Gazebo

If you haven't yet run

## Clone and Build

```bash
cd ~/src
git clone https://github.com/robotics-88/open-drone-core.git
cd open-drone-core
./scripts/setup_workspace.sh -s
colcon build
```

## Launch
In a new terminal, any directory, start Gazebo with:
```
gz sim -v4 -r r88.sdf
```

Start the corresponding ArduPilot with:
```
cd ~/src/r88_ardupilot
./run_gazebo.sh
```

Finally, start the ROS nodes. Gazebo is the default environment so no launch args are required. Run with:
```
cd open-drone-core
./run_sim.sh
```

TODO screenshots