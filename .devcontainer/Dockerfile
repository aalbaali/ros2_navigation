FROM althack/ros2:foxy-gazebo-nvidia

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
   && apt-get -y install --no-install-recommends ripgrep \
   && apt -y install --no-install-recommends ros-foxy-navigation2 \
   && apt -y install --no-install-recommends ros-foxy-nav2-bringup \
   && apt -y install --no-install-recommends ros-foxy-turtlebot3* \
   && apt -y install --no-install-recommends ros-foxy-slam-toolbox \
   #
   # Clean up
   && apt-get autoremove -y \
   && apt-get clean -y \
   && rm -rf /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND=dialog

# Set up auto-source of workspace for ros user
ARG WORKSPACE
RUN echo "if [ -f ${WORKSPACE}/install/setup.bash ]; then source ${WORKSPACE}/install/setup.bash; fi" >> /home/ros/.bashrc

# Gazebe setup
RUN echo "export TURTLEBOT3_MODEL=waffle" >> /home/ros/.bashrc
RUN echo "export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:/opt/ros/foxy/share/turtlebot3_gazebo/models" >> /home/ros/.bashrc
RUN echo "source /usr/share/gazebo/setup.sh" >> /home/ros/.bashrc