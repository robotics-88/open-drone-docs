# ArduPilot

We provide a custom fork of ArduPilot with tuned flight params built-in for our drones (real and sim) and support scripts.

## Install
```bash
cd ~/src
git clone --recurse-submodules git@github.com:robotics-88/r88_ardupilot.git
cd r88_ardupilot
Tools/environment_install/install-prereqs-ubuntu.sh -y
export PATH=$PATH:$HOME/src/r88_ardupilot/Tools/autotest
export PATH=/usr/lib/ccache:$PATH
. ~/.profile
```

!!! note
    The ArduPilot tools script installs a conflicting version of empy (conflicts with mavros). Fix it with `pip install empy==3.3.4`.

## Usage
To use in sim, run this for AirSim:
```bash
cd r88_ardupilot
./run_airsim.sh
```

And this for Gazebo:
```bash
cd r88_ardupilot
./run_gazebo.sh
```
Until the corresponding sim environment is setup and running, this script will fail to find a drone to connect to. Proceed next to the desired sim setup.