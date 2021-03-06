FROM dorowu/ubuntu-desktop-lxde-vnc:bionic

ENV DEBIAN_FRONTEND noninteractive
ENV DEV_NAME=rosdev
ENV ROS_DISTRO=melodic
ENV GROUP_NAME=ros
ENV ROS_WORKSPACE=catkin_ws

RUN echo "Set disable_coredump false" >> /etc/sudo.conf

RUN apt update
RUN apt install -y dirmngr curl

# Setup your computer to accept software from packages.ros.org
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -

RUN apt update
RUN apt install -yq ros-${ROS_DISTRO}-ros-base \
                    python-rosdep \
                    ros-${ROS_DISTRO}-rviz \
                    ros-${ROS_DISTRO}-dwa-local-planner \
                    ros-${ROS_DISTRO}-turtlebot3-navigation \
                    ros-${ROS_DISTRO}-gmapping \
                    git

RUN apt install -yq vim \
                    iputils-ping \
                    net-tools \
                    python-pip \
                    ros-${ROS_DISTRO}-robot-state-publisher \
                    ros-${ROS_DISTRO}-moveit \
                    ros-${ROS_DISTRO}-rosbridge-suite \
                    ros-${ROS_DISTRO}-joy \
                    ros-${ROS_DISTRO}-ros-control \
                    ros-${ROS_DISTRO}-ros-controllers \
                    ros-${ROS_DISTRO}-tf2-web-republisher \
                    dos2unix

RUN sudo -H pip install rospkg jsonpickle

RUN useradd --create-home --home-dir /home/${DEV_NAME} --shell /bin/bash --user-group --groups adm,sudo ${DEV_NAME} && \
    echo "$DEV_NAME:$DEV_NAME" | chpasswd && \
    echo "$DEV_NAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN git clone https://github.com/Unity-Technologies/ROS-TCP-Endpoint /home/${DEV_NAME}/${ROS_WORKSPACE}/src/ros_tcp_endpoint -b v0.6.0

COPY --chown=${DEV_NAME} ./ros_ws/src /home/${DEV_NAME}/${ROS_WORKSPACE}/src

WORKDIR /home/${DEV_NAME}/${ROS_WORKSPACE}

RUN echo "ROS_IP: 0.0.0.0" > /home/${DEV_NAME}/${ROS_WORKSPACE}/src/ros_tcp_endpoint/config/params.yaml

RUN rosdep init
RUN rosdep update

RUN /bin/bash -c "find /home/${DEV_NAME}/${ROS_WORKSPACE} -type f -print0 | xargs -0 dos2unix"

RUN /bin/bash -c "source /opt/ros/$ROS_DISTRO/setup.bash ;\
rosdep install --from-paths src --ignore-src -r -y;\
    catkin_make ;"


RUN chmod +x src/ros_tcp_endpoint/src/ros_tcp_endpoint/*.py

ENV TURTLEBOT3_MODEL=waffle_pi
                    
RUN echo "source /home/${DEV_NAME}/${ROS_WORKSPACE}/devel/setup.bash" >> /home/${DEV_NAME}/.bashrc

# Informs the environment that the default user is not root, but instead DEV_NAME
ENV USER ${DEV_NAME}

