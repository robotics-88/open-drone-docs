# support software
These are support libraries we use to make life easier. E.g., simplify ssh, file access, video streaming, etc.

## mDNS
For convenience. This will make it so on any connected network, your drone hostname shows up as `drone.local` instead of requiring a specific IP.
```
sudo apt update
sudo apt install avahi-daemon avahi-utils
sudo hostnamectl set-hostname drone
```
And so that it starts on boot:
```
sudo systemctl enable avahi-daemon
sudo systemctl start avahi-daemon
```
From here on, instructions will assume the drone can be pinged/ssh'd at `decco@drone.local`. If you skip this step, replace this with the usual `decco@ipaddr`.
