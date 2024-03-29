ARG ROS_DISTRO=noetic

FROM ros:$ROS_DISTRO-ros-base

ARG ROS_DISTRO

ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive
ENV TERM xterm-256color

RUN apt-get update && apt-get install -y --no-install-recommends\
    ssh \
    git \
    curl \
    wget \
    build-essential \
    cmake \
    python3-pip \
    python3-flake8 \
    terminator \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y --no-install-recommends\
    pkg-config \
    python3-catkin-tools \
    python3-rosdep \
    python3-rosinstall-generator \
    ros-$ROS_DISTRO-rqt \
    ros-$ROS_DISTRO-rqt-common-plugins \
    ros-$ROS_DISTRO-rqt-robot-plugins \
    ros-$ROS_DISTRO-roslint \
    ros-$ROS_DISTRO-rqt-gui \
    ros-$ROS_DISTRO-rqt-gui-py \
    ros-$ROS_DISTRO-rqt-py-common \
    ros-$ROS_DISTRO-rviz \
    ros-$ROS_DISTRO-urdf \
    ros-$ROS_DISTRO-xacro \
    ros-$ROS_DISTRO-ecl-threads \
    ros-$ROS_DISTRO-ecl-geometry \
    ros-$ROS_DISTRO-ecl-streams \
    ros-$ROS_DISTRO-kdl-conversions \
    ros-$ROS_DISTRO-image-geometry \
    ros-$ROS_DISTRO-diagnostics \
    ros-$ROS_DISTRO-robot-state-publisher \
    ros-$ROS_DISTRO-gazebo-ros \   
    ros-$ROS_DISTRO-gazebo-plugins \
    ros-$ROS_DISTRO-geometry-msgs \
    ros-$ROS_DISTRO-rtabmap-demos \
    ros-$ROS_DISTRO-turtlebot3 \
    ros-$ROS_DISTRO-turtlebot3-msgs \
    ros-$ROS_DISTRO-turtlebot3-simulations \
    ros-$ROS_DISTRO-turtlebot3-navigation \
    ros-$ROS_DISTRO-dwa-local-planner \
    ros-$ROS_DISTRO-joy \
    ros-$ROS_DISTRO-teleop-twist-joy \
    ros-$ROS_DISTRO-teleop-twist-keyboard \
    ros-$ROS_DISTRO-laser-proc \
    ros-$ROS_DISTRO-rgbd-launch \
    ros-$ROS_DISTRO-amcl \
    ros-$ROS_DISTRO-gmapping \
    ros-$ROS_DISTRO-navigation \
    ros-$ROS_DISTRO-map-server \
    ros-$ROS_DISTRO-move-base \
    ros-$ROS_DISTRO-compressed-image-transport \
    ros-$ROS_DISTRO-interactive-markers \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

WORKDIR /
RUN mkdir -p dev_ws/src

COPY . /dev_ws/src/

WORKDIR /dev_ws

RUN ["/bin/bash", "-c", "source /opt/ros/$ROS_DISTRO/setup.bash &&\
    catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release &&\
    catkin build \
    "]

RUN ["/bin/bash", "-c", "cp /dev_ws/src/.docker/entrypoint.sh /entrypoint.sh && chmod 777 /entrypoint.sh"]
RUN ["/bin/bash", "-c", "cp /dev_ws/src/.docker/setup.bash /dev_ws/setup.bash && chmod 777 /dev_ws/setup.bash"]
ENTRYPOINT ["bash", "/entrypoint.sh" ]

CMD ["bash"]
