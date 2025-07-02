# Config

Vehicle config files are `yaml` files describing the flight controller and sensors on a given platform. These live in [`vehicle_launch/config/vehicles/`](https://github.com/robotics-88/vehicle-launch/tree/main/config). We provide the config files for the Robotics 88 drones, Decco and Ecco, but other drones require adding your own config.

The format is:

```yaml
drone_id: decco_001
frame_id: base_link
simulated: false                                # true for sim, false for IRL

flight_controller:
  type: ardupilot                               # ardupilot or px4
  fcu_url: /dev/cubeorange:57600                # recommend setting up a symlink such as here for cubeorange

sensors:
  camera_front:                                 # cameras must be named camera_*
    type: mapir_rgn                             # this name must match the wrapper launch file, e.g. mapir_rgn.launch, which must live in vehicle_launch/launch/sensors
    topic: /mapir_rgn/image_raw
    frame: mapir_rgn
    stream: camera1                             # optional arg, required for any camera that will be streamed to frontend
    position: [0.094, 0.021, .057]              # with respect to base_link
    orientation_rpy: [0.0, 0.0, 0.0]            # with respect to base_link

  camera_thermal:                               # thermal cameras must include thermal in the name
    type: seek_thermal                          # this name must match the wrapper launch file, e.g. seek_thermal.launch, which must live in vehicle_launch/launch/sensors
    topic: /seek_thermal/image_raw
    frame: seek_thermal
    stream: camera2
    stream_width: 320                           # optional arg for streaming at different resolution than default (640x480)
    stream_height: 240                          # optional arg for streaming at different resolution than default (640x480)
    position: [0.094, 0.021, .057]
    orientation_rpy: [0.0, 0.0, 0.0]
  
  lidar_top:                                    # at present we only support LiDAR-based SLAM, so lidar_top must be included to enable SLAM
    type: mid360                                # this name must match the wrapper launch file, e.g. mid360.launch, which must live in vehicle_launch/launch/sensors
    topic: /livox/lidar
    frame: livox_frame
    position: [0.0138761, 0.0, 0.132799]
    orientation_rpy: [0.0, 0.3926991, 0.0]
```

## Key Details

To highlight the key details:

- Cameras must be named following `camera_*` format
- Thermal cameras must additionally include `thermal` in the name
- SLAM will only launch when `lidar_top` is included in the sensor list (Visual SLAM is on the docket of features to add)
- Cameras that should be streamed to a frontend must include the `stream` arg which must be set to `cameraX`