FROM ros:melodic-ros-base

ENV ROS_WORKSPACE=/catkin_ws

RUN git clone https://github.com/Unity-Technologies/ROS-TCP-Endpoint $ROS_WORKSPACE/src/ros_tcp_endpoint -b v0.6.0

WORKDIR $ROS_WORKSPACE

RUN echo "ROS_IP: 0.0.0.0" > $ROS_WORKSPACE/src/ros_tcp_endpoint/config/params.yaml

RUN /bin/bash -c "source /opt/ros/$ROS_DISTRO/setup.bash ;\
                    catkin_make ;"



RUN chmod +x src/ros_tcp_endpoint/src/ros_tcp_endpoint/*.py

RUN /bin/bash -c "source /opt/ros/$ROS_DISTRO/setup.bash ;\
                    catkin_make ;"
                    
RUN echo ". devel/setup.bash" >> ~/.bashrc

CMD [ "sleep", "infinity" ]