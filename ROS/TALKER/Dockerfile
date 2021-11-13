FROM dustynv/ros:melodic-ros-base-l4t-r32.5.0

RUN echo =====****Updating apt*****=====
RUN apt-get update
RUN echo =====****installing pkgs*****=====
RUN apt-get install -y ros-melodic-ros-tutorials ros-melodic-common-tutorials

CMD [ "/bin/bash" ]
