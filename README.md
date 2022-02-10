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

# Building `Nav2` from source
The `Nav2` repo is listed in the [`src/ros2.repos`](src/ros2.repos) file.
1. Clone the repository by runnnign the VSC task *import from workspace file*.
1. Install necessary dependencies by running the VSC task *install dependencies*.
1. Build packages by running the VSC task *build*.
1. Open a *new* terminal (it'll automatically source the workspace) and have fun!

To test, [run](https://automaticaddison.com/how-to-install-ros-2-navigation-nav2/#:~:text=cd%20~/nav2_ws-,ros2%20launch%20nav2_bringup%20tb3_simulation_launch.py,-rviz2%20will%20open)
```bash
ros2 launch nav2_bringup tb3_simulation_launch.py
```

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
- Check topics verbosely
```bash
ros2 topic info <topic-name> -v
```

# `EMPTY_DIR` files
Git does not support uploading empty directories, but some of these directories are needed for a successful test.
As such, empty directories that are required to be uploaded to Github are populated with an empty file named `EMPTY_DIR`.

# Resources
- [Automatic Addison](https://automaticaddison.com/) ROS2 Navigation Stack [Guide](https://automaticaddison.com/the-ultimate-guide-to-the-ros-2-navigation-stack/).
  - [Adding GPS](https://automaticaddison.com/category/robotics/page/15/)
- [Allison Thackston](https://www.allisonthackston.com/articles/vscode-docker-ros2.html).
- [Nav2](https://navigation.ros.org/getting_started/index.html#running-the-example) package.
- [ROS frames](https://www.ros.org/reps/rep-0105.html)