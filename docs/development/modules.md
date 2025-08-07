# Perception Modules
Passive process that can optionally be enabled during any mission. E.g., thermal hotspot ID could be active during setpoint or lawnmower missions. When modules are added following the instructions on this page, they will be available for toggling on/off for any given mission through our frontend's Mission Center (unless they are set as required by the mission in its config file).

```json
{
    "lidar_slam": {
      "node": "fastlio_mapping",
      "hardware_required": ["lidar"]
    },
    "trail_detection": {
      "node": "trail_follower_node",
      "hardware_required": ["lidar"]
    },
    "thermal_fire": {
      "node": "thermal_pipeline",
      "hardware_required": ["thermal"]
    }
}
```
Note that hardware_required options can be any of the following: ["lidar", "thermal", "rgb", "nir"]

If you add a new perception module, first add your module to the perception json in vehicle_launch (`vehicle_launch/config/perception.json`). Then add the following code snippets to your module.

## C++

In your header, add:
```c
// Parameter handling for toggle on/off
bool is_active_; // Set false here or at the start of your constructor!
std::shared_ptr<rclcpp::ParameterEventHandler> param_subscriber_;
std::shared_ptr<rclcpp::ParameterCallbackHandle> cb_handle_;
rclcpp::TimerBase::SharedPtr param_monitor_timer_;
void parameterCallback(const rclcpp::Parameter &param);
void startParamMonitoring();
// End parameter handling
```

In your class file, add this to the end of your constructor:

```c
is_active_ = false;
param_subscriber_ = std::make_shared<rclcpp::ParameterEventHandler>(this);
startParamMonitoring(); // Use timer to wait for task_manager to load perception registry
```

Then add these methods. Note this is the only code snippet where you need to modify with your own class and node names:
```c
void ClassName::parameterCallback(const rclcpp::Parameter &param) {
    is_active_ = param.as_bool();
    RCLCPP_INFO(this->get_logger(), "ClassName node active: %s", is_active_ ? "true" : "false");
}

void ClassName::startParamMonitoring() {
    param_monitor_timer_ = this->create_wall_timer(
        std::chrono::seconds(1),
        [this]() {
            static bool callback_registered = false;

            if (!callback_registered) {
                try {
                    cb_handle_ = param_subscriber_->add_parameter_callback(
                        "/task_manager/node_name/set_node_active",
                        std::bind(&ClassName::parameterCallback, this, std::placeholders::_1),
                        "task_manager/task_manager"
                    );
                    RCLCPP_INFO(this->get_logger(), "✅ Parameter callback registered for task_manager:node_name/set_node_active");
                    callback_registered = true;
                    param_monitor_timer_->cancel();  // stop retrying
                } catch (const std::exception &e) {
                    RCLCPP_WARN(this->get_logger(), "Waiting for task_manager param to become available: %s", e.what());
                }
            }
        });
}
```

Finally, insert the flag in your node's process:
```c
// at the top of your primary method
if (!is_active_) {
    return;
}
```

## Python
TODO