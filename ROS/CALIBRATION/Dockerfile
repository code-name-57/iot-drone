FROM ros:melodic-ros-core

WORKDIR /app
COPY ros_ws ros_ws

RUN apt-get update
RUN apt-get install -y build-essential

RUN apt-get install -y python-rosdep
RUN rosdep init
RUN rosdep update

WORKDIR /app/ros_ws

RUN rosdep install --from-paths src --ignore-src -r -y
RUN /bin/bash -c "source /opt/ros/$ROS_DISTRO/setup.bash ;\
                    catkin_make ;"

CMD [ "sleep", "infinity" ]
