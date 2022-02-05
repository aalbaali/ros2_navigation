# In this repo
This repository is used as a playground to learn [ROS2](https://docs.ros.org/en/foxy/index.html) and the tools needed for it. Specifically, it is used to learn using the [Nav2](https://navigation.ros.org/) ROS2 toolbox.
The software is mainly written in C++.

# Objectives
This project is quite large, so there are multiple objectives. They are summarized as follows:
- Setting up the development environments (e.g., using Github, Dockerfiles, webhooks, linters, etc.)
- Familiarization with [ROS2](https://docs.ros.org/en/foxy/index.html).
- Running a full navigation pipeline in simulation using ROS2.
- Customizing the existing code for better performance (e.g., using g2o's factor graphs)
- Implementing the software on a real physical robot.

# Sourcing workspaces
It's possible to source multiple workspaces on the same system. For example, it's possible to have a workspace at `~/nav2_ws/` and another at `~/dev_ws`.

## Sourcing the underlay
Some packages can be installed using `apt` package managers.
For example, it's possible to install [turtlesim](https://docs.ros.org/en/foxy/Tutorials/Turtlesim/Introducing-Turtlesim.html) by running
```bash
sudo apt install ros-foxy-turtlesim
```
To use these packages, they must be sourced using
```bash
source /opt/ros/foxy/setup.bash
```
But what if we want to modify the source files? Do we have to keep track of the original and the modified versions?
Well that's where sourcing different workspaces comes into play, which is discussed in the following section.

## Sourcing an overlay
A specific workspace (e.g., `~/nav2_ws/`) could be sourced by going into the workspace and then sourcing the (local) `local_setup.bash` script.
For example,
```bash
cd ~/nav2_ws
source install/local_setup.bash
# Or 
# source install/setup.bash
```
Running `source install/local_setup.bash` sources the current workspace only, whereas `install/setup.bash` sources `install/local_setup.bash` then sources the underlay `/opt/ros/foxy/setup.bash`.
Sourcing the overlay overrides sourcing the underlay. Thus, sourcing `~/nav2_ws` would run the turtlesim version stored in the Nav2 workspace.

# Key commands
- Checking dependencies 
```bash
# cd to workspace root (e.g., ~/nav2_ws)
rosdep install -i --from-path src --rosdistro foxy -y
```
# Resources
- [Automatic Addison](https://automaticaddison.com/) ROS2 Navigation Stack [Guide](https://automaticaddison.com/the-ultimate-guide-to-the-ros-2-navigation-stack/).
- [Allison Thackston](https://www.allisonthackston.com/articles/vscode-docker-ros2.html).
- [Nav2](https://navigation.ros.org/getting_started/index.html#running-the-example) package.