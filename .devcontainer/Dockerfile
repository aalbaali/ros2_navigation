FROM althack/ros2:galactic-gazebo-nvidia

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
  && apt-get -y install software-properties-common \
  && add-apt-repository -y ppa:ubuntu-toolchain-r/test \
  && apt-get -y install --no-install-recommends g++-11 \
  && apt-get -y install --no-install-recommends ripgrep \
  && apt-get -y install --no-install-recommends meld \
  && apt-get -y install --no-install-recommends ros-galactic-navigation2 \
  && apt-get -y install --no-install-recommends ros-galactic-nav2-bringup \
  && apt-get -y install --no-install-recommends ros-galactic-turtlebot3* \
  && apt-get -y install --no-install-recommends ros-galactic-slam-toolbox \
  && apt-get -y install --no-install-recommends ros-galactic-joint-state-publisher-gui \
  && apt-get -y install --no-install-recommends ros-galactic-xacro \
  && apt-get -y install --no-install-recommends ros-galactic-rqt-robot-steering \
  && apt-get -y install --no-install-recommends ros-galactic-robot-localization \
  && apt-get -y install --no-install-recommends ros-galactic-tf2-tools \
  && apt-get -y install --no-install-recommends ros-galactic-tf-transformations \
  && pip3 install --no-input transforms3d \
  && pip3 install --no-input pre-commit \
  #
  # Clean up
  && apt-get autoremove -y \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND=dialog

# Link the g++ binaries to g++-11 to make it the default compiler
# https://stackoverflow.com/questions/7832892/how-to-change-the-default-gcc-compiler-in-ubuntu
RUN update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 100
RUN update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 50
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 100
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 50
RUN update-alternatives --install /usr/bin/cpp cpp-bin /usr/bin/cpp-11 100
RUN update-alternatives --install /usr/bin/cpp cpp-bin /usr/bin/cpp-9 50
RUN update-alternatives --set g++ /usr/bin/g++-11
RUN update-alternatives --set gcc /usr/bin/gcc-11

# The following line was part of the suggested snippet in the link attached above. However, I'm not
# sure what it's doing or what it's used for so I'm not using it but keeping it here for reference.
# sudo update-alternatives --set cpp-bin /usr/bin/cpp-11

# Set default CXX variables
# ENV CXX=/usr/bin/g++


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
RUN echo "export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:/opt/ros/galactic/share/turtlebot3_gazebo/models" >> /home/ros/.bashrc
RUN echo "export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:/workspaces/ros2_navigation/src/basic_mobile_robot/models/" >> /home/ros/.bashrc

RUN echo "source /usr/share/gazebo/setup.sh" >> /home/ros/.bashrc

# Colcon autocomplete (https://docs.ros.org/en/galactic/Tutorials/Colcon-Tutorial.html#setup-colcon-tab-completion)
RUN echo "source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash" >> ~/.bashrc

# Source colcon_cd
RUN echo "\nsource /usr/share/colcon_cd/function/colcon_cd.sh" >> /home/ros/.bashrc
RUN echo "export _colcon_cd_root=${WORKSPACE}" >> /home/ros/.bashrc

RUN echo "complete -W \"\$(colcon_cd && colcon list | awk '{print \$1}')\" colcon_cd" >> /home/ros/.bashrc
RUN echo "alias ccd=\"colcon_cd \$@\"" >> /home/ros/.bashrc
RUN echo "complete -W \"\$(ccd && colcon list | awk '{print \$1}')\" ccd" >> /home/ros/.bashrc

# Add pre-commit-config installed path
RUN echo "export PATH=\"/home/ros/.local/bin:$PATH\"" >> ~/.bashrc

# Add custom workstation tools
RUN mkdir -p /home/ros/Dev
