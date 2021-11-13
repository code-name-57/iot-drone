FROM dustynv/ros:melodic-ros-base-l4t-r32.5.0

RUN apt-get update && apt-get install -y \
    ros-melodic-ros-tutorials \
    ros-melodic-common-tutorials \
    && rm -rf /var/lib/apt/lists/

CMD [ "/bin/bash" ]
