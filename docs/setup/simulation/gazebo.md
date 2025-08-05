# Gazebo

If you already ran the [quickstart script](../../quickstart.md), Gazebo sim should be ready to run, and you can jump to Launch below.

## Launch

### 1. Launch Gazebo
In a new terminal, start Gazebo with:
```
gz sim -v4 -r r88.sdf
```

### 2. Launch ArduPilot
Start the corresponding ArduPilot with:
```
cd ~/src/r88_ardupilot
./run_gazebo.sh
```

### 3. Launch ROS
Finally, start the ROS nodes. Gazebo is the default environment so no launch args are required. Run with:
```
cd open-drone-core
./run_sim.sh
```

TODO screenshots