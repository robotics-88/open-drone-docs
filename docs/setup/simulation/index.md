# Sim Drones

The flight stack can be tested in sim using either AirSim or Gazebo. It is highly recommended to test any new changes in sim prior to flight on a real drone! The following pages detail sim setup for each. Note that [Quickstart](../../quickstart.md) provides instructions on using the setup script for a workspace, which installs everything required for Gazebo sim. If you ran that and don't need AirSim, no need to do anything further for sim setup! However AirSim requires manually getting access to Unreal Engine so proceed to [AirSim](airsim.md) for further details on that, or if you wish to do a manual workspace setup, read on.

!!! info
    Future work, add details on testing with PX4 in sim.

To begin, the first step is install [ArduPilot](ardupilot.md).

Then, the setup order depends on which environment you plan to use. If you want to test both, start with [AirSim](airsim.md) as it has preliminary setup requirements.