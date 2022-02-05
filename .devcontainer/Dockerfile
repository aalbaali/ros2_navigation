FROM althack/ros2:foxy-dev 

# ** [Optional] Uncomment this section to install additional packages. **
#
#ENV DEBIAN_FRONTEND=noninteractive
#RUN apt-get update \
#   && apt-get -y install --no-install-recommends <your-package-list-here> \
#   # Clean up
#   && apt-get autoremove -y \
#   && apt-get clean -y \
#   && rm -rf /var/lib/apt/lists/*
#
#ENV DEBIAN_FRONTEND=dialog

# - Create dev_ws directory
# - Set locale:
#       locale  # check for UTF-8
#       
#       sudo apt update && sudo apt install locales
#       sudo locale-gen en_US en_US.UTF-8
#       sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
#       export LANG=en_US.UTF-8
#       
#       locale  # verify settings
# - Setup sources
#       sudo apt update && sudo apt install curl gnupg2 lsb-release
#       sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key  -o /usr/share/keyrings/ros-archive-keyring.gpg
# - Install Nav2
#       sudo apt install ros-foxy-navigation2 ros-foxy-nav2-bringup '~ros-foxy-turtlebot3-.*'
# - Setup Nav2
#   $ mkdir -p ~/nav2_ws/src && cd ~/nav2_ws/src && git clone https://github.com/ros-planning/navigation2.git --branch foxy-devel && cd ..
#   $ rosdep install -y -r -q --from-paths src --ignore-src --rosdistro foxy
#   $ colcon build --symlink-install # Took around 32 minutes to install
# - Store the following in ~/.bashrc:
#    source ~/nav2_ws/install/setup.bash
#    export TURTLEBOT3_MODEL=waffle
#    export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:/opt/ros/foxy/share/turtlebot3_gazebo/models
#    source /usr/share/gazebo/setup.sh
# - $ colcon build

# Set up auto-source of workspace for ros user
ARG WORKSPACE
RUN echo "if [ -f ${WORKSPACE}/install/setup.bash ]; then source ${WORKSPACE}/install/setup.bash; fi" >> /home/ros/.bashrc
