# JunBotGUI

## Config ROS plugin for QtCreator

1. Add Pugin

[Link](https://github.com/ros-industrial/ros_qtc_plugin#plugin-installation)

```
sudo apt install libarchive-tools # needed for bsdtar
export QTC_ROOT=~/Qt/Tools/QtCreator # online installer
# export QTC_ROOT=~/qtcreator-6.0.0 # offline installer
export PLUGIN_URL=`curl -s https://api.github.com/repos/ros-industrial/ros_qtc_plugin/releases/latest | grep -E 'browser_download_url.*ROSProjectManager-.*-Linux-.*.zip' | cut -d'"' -f 4`
curl -SL $PLUGIN_URL | bsdtar -xzf - -C $QTC_ROOT
```

2. Config workspace

- Install catkin_tools

```
sudo sh \
    -c 'echo "deb http://packages.ros.org/ros/ubuntu `lsb_release -sc` main" \
        > /etc/apt/sources.list.d/ros-latest.list'

wget http://packages.ros.org/ros.key -O - | sudo apt-key add -

sudo apt-get update

sudo apt-get install python3-catkin-tools

sudo apt-get install -y ros-noetic-move-base-msgs
```
- QtCreator => New project => Other project => ROS workspace

- Build 

3. Run test with TurtleBot 3 simulation

3.1. Run Turtlebot 3 simulation

<b> Note </b>: You need run SLAM before this step (if you do not have a map)

```
# Terminal 1: Simulation Node 
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_gazebo turtlebot3_world.launch

# Terminal 2: Navigation Node
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
```

3.2. Run app

```
rosrun junbot_gui junbot_gui
```

## App detail

### Use case

![Fig.1](https://github.com/ScarecrowStraw/JunbotGUI/blob/main/data/readme/JunbotGUI-1.png?raw=true)

## TODO

- [x] ~~Delete unnecessary widget/screen/dashboard/button~~
- [ ] Test with LCD
- [ ] Add Initial Pose Estimation Button (Run ACML automatic)
- [ ] Update icon
- [x] Linux Embedded

