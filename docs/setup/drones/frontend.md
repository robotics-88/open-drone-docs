# Frontend
We have provided a generic frontend for accessing drone status and sending missions. This is akin to something like QGroundControl, except that where QGC is targeted for manual and low-level drone control, this interface is targeted for high-level mission control.

## REST Server


### Start on Boot
Make this file `sudo nano /etc/systemd/system/drone-server.service` and paste in it:
```
[Unit]
Description=Drone REST Server
After=network.target

[Service]
User=decco
WorkingDirectory=/home/decco/src/open-drone-server
ExecStart=/bin/bash -c 'source /opt/ros/humble/setup.bash && source .env/bin/activate && python main.py'
Restart=on-failure
Environment=PYTHONUNBUFFERED=1

[Install]
WantedBy=multi-user.target
```