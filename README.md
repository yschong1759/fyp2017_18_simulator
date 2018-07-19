fyp2017_18_simulator
---------------------

This Gazebo simulator setup is for a Final Year Project in NTU MAE under supervision of Prof Gerald Seet. It is referred from [here](www/moorerobots.com/blog).

There are 4 folders.

```
   mybot_gazebo       : define the models in a simulation world
   mybot_description  : specific the structure and appearance of a robot
   mybot_navigation   : create SLAM maps, enable tele-operation
   mybot_control      : seldom used, refer [here](www/moorerobots.com/blog)
```
Put these folder in the src folder of a catkin_workspace.


Edit a simulation world
------------------------

Load an empty world and insert your model.
You may use the model database by Gazebo or create your own model.

* Access model databse via
  `Insert` -> `http://gazebosim.org/models`

* To create a model
  Refer to the Gazebo tutorial: 
  [Build a robot, import mesh, add sensor](http://gazebosim.org/)tutorials?tut=build_robot&cat=build_robot

* [Understanding how Gazebo and ROS communicate](http://gazebosim.org/tutorials?tut=ros_roslaunch&cat=connect_ros)

Save after editing. It will be in a `.sdf` file. To use the world in `roslaunch`, the `.sdf` file needs to be specified in the `.launch` file.

Start Gazebo and ROS
--------------------

### Launch Gazebo with "ROS-enabled"

In a new terminal, enter `roslaunch mybot_gazebo mybot_world.launch`

### Launch rviz

In a new terminal, enter `roslaunch mybot_description mybot_rviz.launch`

### Run your ROS packages

Next, you can run corresponding ROS package to interact with the simulation.


Troubleshooting
---------------

1. 
    If you get an error, 
    `ERROR: cannot launch node of type [gazebo_ros/gzserver]: can't locate node [gzserver] in package [gazebo_ros]
    ERROR: cannot launch node of type [gazebo_ros/gzclient]: can't locate node [gzclient] in package [gazebo_ros]
    ERROR: cannot launch node of type [gazebo_ros/spawn_model]: can't locate node [spawn_model] in package [gazebo_ros]`

    It is likely because ROS could not locate Gazebo. To solve,

    * In a new terminal, enter `source /opt/ros/<distro-version>/setup.bash`
    * Add your catkin workspace to `ROS_PACKAGE_PATH`, enter `ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:/path/to/your/workspace/src`
    * Then, launch Gazebo again with `roslaunch`

2. 
    Unable to load the table and chair in Gazebo, it may be because unable to locate the mesh files of the table or chair
    
    Replace path to table and chair model in `worlds/mybot.world` by
    `path_to_your_catkin_workspace/src/mybot_gazebo/worlds/stefan_chair.dae`
    `path_to_your_catkin_workspace/src/mybot_gazebo/worlds/lerhamn_table.dae`
