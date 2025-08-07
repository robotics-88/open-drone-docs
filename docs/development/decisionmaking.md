# Decision-Making

The path manager includes a decision-making algorithm for modifying destination targets. Decisions are the result of a weighted average of user-defined criteria. The criteria can be anything that better serves your application. E.g., to modify destination targets in a subcanopy environment, the SAFETY criteria is used to push targets away from obstacles detected by LiDAR. And to improve ash tree finding, the ASH criterion is used to push targets toward areas more likely to include ash trees.

Built-in criteria are:

* DIST: Mimimize distance to target
* INFO: Seek targets close to unexplored areas
* EFFICIENCY: Minimize distance between target and prior goal
* SAFETY: Maximize distance from target to nearest obstacle
* ASH: Seek targets where the terrain is a local valley (requires DEM)

Each criteria requires a utility function. E.g., DIST uses Euclidean distance from the drone to the target as its utility function. This is not a perfect representation of the actual distance that will be traveled, just a prediction. We could have instead run the path planner, but fast is better than perfect. Utility functions should be fast, as they will be run on all destinations to identify the optimal next target. Right now, we produce 10 possible destinations, and all destinations are evaluated across all criteria.

To add a new criterion:

1. **DECLARE**: Add the criterion to the `DecisionMaker::Criteria` enum in `path_manager/explorer/decision_maker.h`
2. **LAUNCH**: Add the criterion and its weight to the launch args list in `vehicle_launch/launch/opendrone.launch.py` in this line:

    ```xml
    DeclareLaunchArgument('criteria', default_value='DIST,INFO,SAFETY,MYCRITERIA'),
    DeclareLaunchArgument('weights', default_value='0.2,0.1,0.6,MYWEIGHT')
    ```

    Weights should sum to 1. They will be normalized if they do not, which may result in misaligned preferences.

3. **DEFINE**: Add the criterion's corresponding utility function to the switch in `DecisionMaker::utilityFunction` in `path_manager/explorer/decision_maker.cpp`. If it is more complex than a single line of code, make a new method and call it from the switch. 

    🚨 IMPORTANT: utility functions must be written such that high scores are better! Otherwise it will optimize for the opposite of your criterion.