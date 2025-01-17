# autonomous-skid-steering-robot
Autonomous Skid-Steering Based Mobile Robot-Manipulation System for Automating Warehouse Operations

## Software Requirements for Social Navigation Part
* ROS installation
* Ubuntu
* Eigen3 (Please install Eigen3 from the following link:https://eigen.tuxfamily.org/index.php?title=Main_Page)
* rqt_multiplot

## Installation instructions
This set of instructions was tested for Ubuntu18 with ROS-Melodic. Additionally, we assume that you already have a complete ROS installation.

* Please follow the following instructions:
```
sudo apt-get install ros-melodic-jackal-control ros-melodic-jackal-gazebo ros-melodic-jackal-simulator ros-melodic-jackal-description ros-melodic-jackal-desktop ros-melodic-jackal-navigation ros-melodic-jackal-viz ros-melodic-people-msgs
cd {CATKIN_WORKSPACE}/src
git clone https://github.com/kurshakuz/graduation-project.git
cd ../
rosdep install --from-paths src --ignore-src -r -y
cd {CATKIN_WORKSPACE}
catkin_make
source devel/setup.bash
```

## Full simulation launch procedure
1. Start LMPCC Obstacle Feed
```console
roslaunch lmpcc_obstacle_feed lmpcc_obstacle_feed.launch
```
2. Start Pedsim simulator with pedestrian trajectories
```console
roslaunch pedsim_swarm_simulation pedsim_office_populated.launch
```
3. Start Gazebo simulation with Office world
```console
roslaunch cpr_office_gazebo office_world_with_plugin.launch
```
4. Start localization node and load map
```console
roslaunch jackal_navigation amcl_demo.launch map_file:={CATKIN_WORKSPACE}/src/graduation-project/robot_swarm/pedsim_swarm_simulation/maps/mymap.yaml
```
5. Start RViz node
```console
roslaunch jackal_viz view_robot.launch config:=localization
```
6. Start LMPCC Controller
```console
roslaunch lmpcc lmpcc.launch
```
7. Start static collision avoidance node
```console
roslaunch static_collision_avoidance static_collision_avoidance.launch
```
8. Start rqt_reconfigure
```console
rosrun rqt_reconfigure rqt_reconfigure
```
        1. Click on the lmpcc parameters to start the robot motion by press the enable_output button
        2. Click on the lmpcc parameters to start planning by pressing the plan button


## Running MPC
* Simulation Environment

        1. roslaunch jackal_gazebo empty_world.launch
        2. roslaunch mocap_rover mocap_bridge_gazebo.launch

* Start NMPC and trajectory

        1. roslaunch nmpc_pc_rover nmpc_pc_gazebo.launch
        2. roslaunch trajectory_rover trajectory_rover.launch

* Start rqt_multiplot 

        1. rqt_multiplot (use included files)
        
## Running LMPCC
* Simulation Environment

        1. Start Jackal Gazebo Simulation
            * roslaunch jackal_gazebo jackal_world.launch
        2. Start Pedestrian Simulator
            * roslaunch pedsim_simulator corridor.launch
* Start lmpcc_obstacle_feed

        1. roslaunch lmpcc_obstacle_feed lmpcc_obstacle_feed.launch

* Start lmpcc controller

        1. roslaunch lmpcc lmpcc.launch

* Start rqt_reconfigure

        1. rosrun rqt_reconfigure rqt_reconfigure
        2. Click on the lmpcc parameters to start the robot motion by press the enable_output button
        3. Click on the lmpcc parameters to start planning by pressing the plan button

## Run Gazebo and Pedsim based LMPCC navigation

* Launch Gazebo simulation world

        1. roslaunch cpr_office_gazebo office_world_with_plugin.launch

* Start LMPCC Obstacle Feed and Controller

        1. roslaunch lmpcc_obstacle_feed lmpcc_obstacle_feed.launch
        2. roslaunch lmpcc lmpcc.launch

* Spawn pedsim people and start vizualization in rviz

        1. roslaunch pedsim_swarm_simulation pedsim_office_populated.launch

* Start rqt_reconfigure

        1. rosrun rqt_reconfigure rqt_reconfigure
        2. Click on the lmpcc parameters to start the robot motion by press the enable_output button
        3. Click on the lmpcc parameters to start planning by pressing the plan button

