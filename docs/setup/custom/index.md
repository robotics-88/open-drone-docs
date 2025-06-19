# Custom

1. Config

    For custom drone setup, the first step is to create a vehicle config file with all your sensors as described [here](../drones/config.md).

2. Sensors

    If you're adding a new sensor, you need to provide a launch file in `vehicle_launch`. This can simply be a reference to another launch file, but it must match the name scheme in the config file you just created.

3. Launch
    
    Test that your new config is launching as expected with:

    `ros2 launch vehicle_launch opendrone.launch.py config_file:=myconfig.yaml`

4. Systemd

    It's generally preferable to create a systemd service so your ROS2 config launches on boot.

    TODO add a systemd creator shell script.

That's it! :tada:

If you've already set up the [frontend](../drones/frontend.md) on a machine that's on the same network as your vehicle, you should now be able to connect [here](http://127.0.0.1:8040/).