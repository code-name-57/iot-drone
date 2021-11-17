# FROM dustynv/ros:melodic-ros-base-l4t-r32.5.0
FROM ros:melodic-ros-core

WORKDIR /app
COPY ros_ws ros_ws
RUN mkdir ANKUR
SHELL ["/bin/bash", "-c"] 
RUN source "/opt/ros/$ROS_DISTRO/setup.bash"
RUN rostopic --help
# RUN apt-get update
# RUN apt-get install build-essential

# # RUN apt-get install ros-melodic-cv-bridge
# RUN apt-get install python-rosdep
# RUN rosdep init
# RUN rosdep update

# RUN cd ros_ws
# RUN rosdep install --from-paths src --ignore-src -r -y
RUN catkin_make

CMD [ "roscore" ]
