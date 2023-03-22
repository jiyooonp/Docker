FROM osrf/ros:melodic-desktop-full

SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get install -y git && apt update
RUN echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc

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
RUN cd ~/catkin_ws 
RUN . /opt/ros/melodic/setup.sh && cd ~/catkin_ws/ &&\
    catkin_make

RUN echo "source ~/catkin_ws/devel/setup.bash " >> ~/.bashrc
RUN source ~/.bashrc

# install sawyer ros gazebo
RUN sudo apt-get install -y gazebo9 ros-melodic-qt-build ros-melodic-gazebo-ros-control ros-melodic-gazebo-ros-pkgs ros-melodic-ros-control ros-melodic-control-toolbox ros-melodic-realtime-tools ros-melodic-ros-controllers ros-melodic-xacro python-wstool ros-melodic-tf-conversions ros-melodic-kdl-parser


# install sawyer_simulator
RUN cd ~/catkin_ws/src && git clone https://github.com/RethinkRobotics/sawyer_simulator.git
RUN cd ~/catkin_ws/src && git clone https://github.com/RethinkRobotics-opensource/sns_ik.git
RUN wstool init ~/catkin_ws/src
RUN wstool merge ~/catkin_ws/src/sawyer_simulator/sawyer_simulator.rosinstall -t ~/catkin_ws/src
RUN wstool update -t ~/catkin_ws/src

# BUILD source 
RUN source /opt/ros/melodic/setup.bash
RUN cd ~/catkin_ws

# simulation
RUN cd ~/catkin_ws/src/intera_sdk

# Installing MoveIt
RUN sudo apt-get update
RUN sudo apt-get install -y ros-melodic-moveit

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
RUN cp ~/catkin_ws/src/intera_sdk/intera.sh ../

