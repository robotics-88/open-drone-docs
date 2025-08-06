# Custom

Even if you are using a custom drone, it is best to first install all required packages per the [Quickstart](../../quickstart.md) instructions. Once complete, next do the following 4 steps to configure the software for your custom drone.

1. Config

    For custom drone setup, the first step is to create a vehicle config file with all your sensors as described [here](../drones/config.md).

2. Sensors

    If you're adding a new sensor, you need to add a launch file in `vehicle_launch/launch/sensors`. This can simply launch another package's launch file, but it must match the name scheme in the config file you just created.

3. Launch
    
    Test that your new config is launching as expected with:

    `ros2 launch vehicle_launch opendrone.launch.py config_file:=myconfig.yaml`

    If this works, update the systemd service in the next step so your config is the system default.

4. Systemd

    The quickstart instructions set up a systemd service so the ROS nodes start on boot. Update the script to use your config file as a launch arg:

    ```bash
    cd ~/src/open-drone-core
    nano run_drone.sh
    ```

    Change the script on the config_file line:

    ```bash
    #!/bin/bash

    source /opt/ros/humble/setup.bash
    source /home/$USER/src/open-drone-core/install/setup.bash
    source /home/$USER/src/livox_ros_driver2/install/setup.bash

    # Get UTC date for logging
    date=$(date -u '+%Y-%m-%d_%H-%M-%S')
    data_directory=/home/$USER/r88_public/records/$date/
    mkdir -p $data_directory

    stdbuf -oL ros2 launch vehicle_launch opendrone.launch.py \
        config_file:=myconfig.yaml \ # <------ change this to your config 
        data_directory:=$data_directory $@ 2>&1 | tee $data_directory/distal_stdout_$date.log
    ```

    Restart the service for the change to take effect:
    ```
    sudo systemctl restart drone.service
    ```


That's it! :tada:

If you've already set up the [frontend](../drones/frontend.md) on a machine that's on the same network as your vehicle, you should now be able to connect [here](http://127.0.0.1:8040/).