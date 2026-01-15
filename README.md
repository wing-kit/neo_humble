# ROS2 Humble Environment Setup

## Purpose
What this docker image offers
1. NoVNC enabled (so that you can use just a browser to access the GUI desktop env. `export DISPLAY=":1"`)
2. xRDP enabled (so that you can use mstsc to access the GUI desktop env. `export DISPLAY=":10"`)
3. SSH enabled (so that you can even use remote dev in decent IDE)
4. True cross-platform ROS2 dev ready (tested on MacOS 26 M3 arm64 and Ubuntu 20.04 x86)


## Getting Started

### Init
```
mkdir -p ~/projects/aic_swarm/ros2_workspaces/ws1
mkdir -p ~/projects/aic_swarm/ros2_workspaces/shared/nginx-conf
touch ~/projects/aic_swarm/ros2_workspaces/shared/nginx-conf/doc.conf
touch ~/projects/aic_swarm/ros2_workspaces/shared/bashrc
touch ~/projects/aic_swarm/ros2_workspaces/ws1/bashrc
```

### Clone neo workspace
```
cd ~/projects/aic_swarm/ros2_workspaces/shared/
git clone --recurse-submodules https://github.com/wing-kit/neo_humble_ws.git neobotix_workspace
```

### Start Up
`docker compose up -d`


### NoVNC
After about a minute you should be able to use your host browser to visit http://localhost:36081 with password (See [docker-compose.yml](https://github.com/wing-kit/neo_humble/blob/main/docker-compose.yml))

1. Open terminal and build the neobotix_workspace
  ```
  cd ~/shared/neobotix_workspace
  source /usr/share/gazebo/setup.sh
  source /opt/ros/humble/setup.bash
  colcon build --symlink-install
  ```

  Successful build should look like:
![WhatsApp Image 2026-01-14 at 12 14 12](https://github.com/user-attachments/assets/0cb1c4c3-2941-49c0-b364-17264b4b8fbf)


2. Run the example simulator
   ```
   source /usr/share/gazebo/setup.sh
   source /opt/ros/humble/setup.bash
   source /home/ubuntu/shared/neobotix_workspace/install/setup.bash
   ros2 launch neo_simulation2 simulation.launch.py my_robot:=mpo_700 world:=neo_workshop
   ```

3. You should now see the gazebo world loaded and spawned the mpo_700 robot with keyboard teleop ready.
   <img width="663" height="517" alt="Screenshot 2026-01-14 at 11 45 15 AM" src="https://github.com/user-attachments/assets/a9b14bbe-943d-4de6-85fe-1406987b703d" />



### Take down

Before taking down the container please note that ONLY ~/shared and ~/ros2_ws are persistant to your host. All other files would be gone. Be careful.

`docker compose down --remove-orphans`
