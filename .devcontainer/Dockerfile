FROM althack/ros2:foxy-gazebo-nvidia

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
   && apt-get -y install --no-install-recommends ripgrep \
   && apt-get -y install --no-install-recommends ros-foxy-navigation2 \
   && apt-get -y install --no-install-recommends ros-foxy-nav2-bringup \
   && apt-get -y install --no-install-recommends ros-foxy-turtlebot3* \
   && apt-get -y install --no-install-recommends ros-foxy-slam-toolbox \
   && apt-get -y install --no-install-recommends ros-foxy-joint-state-publisher-gui \
   && apt-get -y install --no-install-recommends ros-foxy-xacro \
   && apt-get -y install --no-install-recommends ros-foxy-rqt-robot-steering \
   && apt-get -y install --no-install-recommends ros-foxy-robot-localization \
   && apt-get -y install --no-install-recommends ros-foxy-tf2-tools \
   && apt-get -y install --no-install-recommends ros-foxy-tf-transformations \
   && pip3 install --no-input transforms3d \
   #
   # Clean up
   && apt-get autoremove -y \
   && apt-get clean -y \
   && rm -rf /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND=dialog

# Add aliases
#   Git
RUN echo -e "\nalias gll='git log --graph --oneline --all --decorate'" >> ~/.bashrc
RUN echo "alias gs='git status'" >> ~/.bashrc
RUN echo "alias gm='git commit'" >> ~/.bashrc
RUN echo "alias ga='git add'" >> ~/.bashrc
RUN echo "alias gb='git branch'" >> ~/.bashrc
RUN echo "alias gc='git checkout'" >> ~/.bashrc
RUN echo -e "\n" >> ~/.bashrc

# Set up auto-source of workspace for ros user
ARG WORKSPACE
RUN echo "if [ -f ${WORKSPACE}/install/setup.bash ]; then source ${WORKSPACE}/install/setup.bash; fi" >> /home/ros/.bashrc

# Gazebe setup
RUN echo "\nexport TURTLEBOT3_MODEL=waffle" >> /home/ros/.bashrc

# Gazebo model paths
RUN echo "export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:/opt/ros/foxy/share/turtlebot3_gazebo/models" >> /home/ros/.bashrc
RUN echo "export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:/workspaces/ros2_navigation/src/basic_mobile_robot/models/" >> /home/ros/.bashrc

RUN echo "source /usr/share/gazebo/setup.sh" >> /home/ros/.bashrc

# Colcon autocomplete (https://docs.ros.org/en/foxy/Tutorials/Colcon-Tutorial.html#setup-colcon-tab-completion)
RUN echo "source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash" >> ~/.bashrc

# Source colcon_cd
RUN echo "\nsource /usr/share/colcon_cd/function/colcon_cd.sh" >> /home/ros/.bashrc
RUN echo "export _colcon_cd_root=${WORKSPACE}" >> /home/ros/.bashrc

RUN echo "complete -W \"\$(colcon_cd && colcon list | awk '{print \$1}')\" colcon_cd" >> /home/ros/.bashrc
RUN echo "alias ccd=\"colcon_cd \$@\"" >> /home/ros/.bashrc
RUN echo "complete -W \"\$(ccd && colcon list | awk '{print \$1}')\" ccd" >> /home/ros/.bashrc
