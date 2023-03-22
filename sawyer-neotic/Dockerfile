FROM osrf/ros:noetic-desktop-full

SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get install -y git && apt update
RUN echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc

# to have same alias as in local laptop
RUN echo "# alias " >> ~/.bashrc
RUN echo "alias sb='source ~/.bashrc' " >> ~/.bashrc
RUN echo "alias eb='gedit ~/.bashrc' " >> ~/.bashrc
RUN echo "alias cm='cd ~/catkin_ws/ && catkin_make' " >> ~/.bashrc
RUN echo "alias update='sudo apt update'" >> ~/.bashrc
RUN echo "alias upgrade='sudo apt upgrade'" >> ~/.bashrc
RUN echo "alias cw='cd ~/catkin_ws/ '" >> ~/.bashrc
RUN source ~/.bashrc

# for ease of use 
RUN apt install -y gedit 

RUN mkdir -p ~/catkin_ws/src 

RUN source /opt/ros/noetic/setup.bash 
RUN cd ~/catkin_ws 
RUN . /opt/ros/noetic/setup.sh && cd ~/catkin_ws/ &&\
    catkin_make

RUN echo "source ~/catkin_ws/devel/setup.bash " >> ~/.bashrc
RUN source ~/.bashrc

# install sawyer ros gazebo
RUN sudo apt-get install -y gazebo11 ros-noetic-gazebo-ros ros-noetic-gazebo-ros-control ros-noetic-gazebo-ros-pkgs ros-noetic-ros-control ros-noetic-control-toolbox ros-noetic-realtime-tools ros-noetic-ros-controllers ros-noetic-xacro python3-wstool ros-noetic-tf-conversions ros-noetic-kdl-parser


# install sawyer_simulator
RUN cd ~/catkin_ws/src
RUN git clone https://github.com/RethinkRobotics/sawyer_simulator.git -b noetic_devel
RUN cd ~/catkin_ws/src
RUN git clone https://github.com/RethinkRobotics-opensource/sns_ik.git
RUN wstool init ~/catkin_ws/src
RUN wstool merge sawyer_simulator/sawyer_simulator.rosinstall -t ~/catkin_ws/src
RUN wstool update -t ~/catkin_ws/src

# BUILD source 
RUN source /opt/ros/noetic/setup.bash
RUN cd ~/catkin_ws

# simulation
RUN cd ~/catkin_ws/src/intera_sdk
# RUN ./intera.sh sim

# Installing MoveIt
RUN sudo apt-get update
RUN sudo apt-get install -y ros-noetic-moveit

# Installing and building Sayer Moveit Repo 
RUN cd ~/catkin_ws/
RUN cd ~/catkin_ws/src/intera_sdk && ./intera.sh sim
RUN cd ~/catkin_ws/src
RUN wstool merge https://raw.githubusercontent.com/RethinkRobotics/sawyer_moveit/melodic_devel/sawyer_moveit.rosinstall -t ~/catkin_ws/src
RUN wstool update -t ~/catkin_ws/src
RUN cd ~/catkin_ws/

# create overlay_ws
RUN mkdir ~/catkin_ws/src/overlay_ws

# extra saywer stuff
RUN cp ~/catkin_ws/src/intera_sdk/intera.sh ../..