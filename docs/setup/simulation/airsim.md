# AirSim
AirSim is an Unreal plugin developed by Microsoft but no longer maintained, so don't use the Microsoft version. We are now using our own fork of Colosseum because when we last checked theirs didn't work on Ubuntu 22 (TODO check again).

## Unreal Setup

1. Download and extract [Unreal 5.4](https://github.com/EpicGames/UnrealEngine/releases/tag/5.4.0-release) to `~/src`
2. Build:
    
    ```bash
    cd ~/src/UnrealEngine-5.4.0-release
    ./Setup.sh
    ./GenerateProjectFiles.sh
    make
    ```
    
3. If asked during Setup to register Unreal file types, say yes. Upon completion of the script, the “SUCCESS” message should print.
4. *Unclear if this is always required, but
    1. make sure you’re using an NVIDIA driver, you’ll get a warning about Vulkan driver missing if not;
    2. if Unreal opens but the project fails, or if you get an error about incompatible versions/open with null source code, [remove](https://forums.unrealengine.com/t/how-to-solve-engine-modules-are-out-of-date/564119/5) the args “-NoEngineChanges -NoHotReloadFromIDE” from DesktopPlatformBase.cpp, then make again

## Colosseum Setup
    
First add libs for vulkan.

```jsx
wget -qO- https://packages.lunarg.com/lunarg-signing-key-pub.asc | sudo tee /etc/apt/trusted.gpg.d/lunarg.asc
sudo wget -qO /etc/apt/sources.list.d/lunarg-vulkan-jammy.list http://packages.lunarg.com/vulkan/lunarg-vulkan-jammy.list
sudo apt update
```

Then for libunwind:

```bash
sudo apt-get update
sudo apt-get install libunwind-dev
```

Then:

```bash
cd ~/src
git clone git@github.com:robotics-88/Colosseum.git
cd Colosseum
git checkout r88_5.2
./setup.sh
./build.sh
```

+

Add to `~/.bashrc`:

```bash
export AIRSIM_DIR="/home/$USER/src/Colosseum"
source ~/.bashrc
```

## ROS2
Our AirSim ROS2 wrapper depends on finding Colosseum/AirSim, so if you jump to this section the build will fail without the above. Assuming the prior steps are complete:

### Clone and Build

```bash
cd ~/src
git clone https://github.com/robotics-88/open-drone-core.git
cd open-drone-core
./scripts/setup_workspace.sh
colcon build
```

### Launch
Start Unreal:
```bash
cd ~/src/Unreal
./Engine/Binaries/Linux/UnrealEditor
```
If running for the first time, you'll need to use the project browser to locate the R88 world. If you check "open last project on start," then next time you run this terminal command, it will take you straight to the sim.

Start ArduPilot:
```bash
cd ~/src/r88_ardupilot
./run_airsim.sh
```

In Unreal, press play (shortcut `Alt + P`).

Run the flight stack with:
```bash
cd open-drone-core
./run_sim.sh do_airsim:=true do_gazebo:=false
```
!!! note
    Note, when you want to stop the sim, press stop in Unreal (shortcut ESC) BEFORE `Ctrl+C` in ArduPilot, or the window will freeze.