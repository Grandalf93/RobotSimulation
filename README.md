# ROS2 COURSE: URDF | RVIZ | GAZEBO
This ROS2-based repository hosts the project developed in the course [ROS2 for beginners level 2: TF | URDF | Gazebo ](https://www.udemy.com/course/ros2-tf-urdf-rviz-gazebo/) taught by the instructor [Edouard Renard](https://www.udemy.com/user/edouard-renard/)

the project delves into concepts such as transforms, urdf files, xacro functionalities and gazebo as it creates a custom robotics application for both a robotic manipulator and a mobile robot, paving the journey to deeper explore ROS frameworks including Nav Stack and Moveit.

![image](https://github.com/user-attachments/assets/9fabb5b1-31a9-4660-b76c-9eb338e3322f)



## Dependencies
It is advisable to use [VS Code](https://code.visualstudio.com/) as the main IDE. Make sure you have also installed in your host:
 1. [docker-ce](https://docs.docker.com/install/)
 2. [Dev-container extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) 
 3. [VcXsrv Windows X Server](https://sourceforge.net/projects/vcxsrv/)

**for further documentation on dockerizing ROS2: **  [Setup docker and ROS2](https://docs.ros.org/en/foxy/How-To-Guides/Setup-ROS-2-with-VSCode-and-Docker-Container.html)
 
## structure and packages
The ROS2 workspace consists of two packages: `my_robot_bringup` so as to spawn the robot in gabezo and  `my_robot_bringup` used for debugging purposes

```
├── build
│   ├── my_robot_bringup
│   │   ├── ament_cmake_core
│   │   │   └── stamps
│   │   ├── ament_cmake_environment_hooks
│   │   ├── ament_cmake_index
│   │   │   └── share
│   │   ├── ament_cmake_package_templates
│   │   ├── ament_cmake_symlink_install
│   │   ├── ament_cmake_uninstall_target
│   │   ├── ament_lint_cmake
│   │   └── ament_xmllint
│   └── my_robot_description
│       ├── ament_cmake_core
│       │   └── stamps
│       ├── ament_cmake_environment_hooks
│       ├── ament_cmake_index
│       │   └── share
│       ├── ament_cmake_package_templates
│       ├── ament_cmake_symlink_install
│       └── ament_cmake_uninstall_target
├── install
│   ├── my_robot_bringup
│   │   └── share
│   │       ├── colcon-core
│   │       │   └── packages
│   │       └── my_robot_bringup
│   │           ├── cmake
│   │           ├── environment
│   │           ├── hook
│   │           ├── launch
│   │           ├── rviz
│   │           └── worlds
│   └── my_robot_description
│       └── share
│           ├── colcon-core
│           │   └── packages
│           └── my_robot_description
│               ├── cmake
│               ├── environment
│               ├── hook
│               ├── launch
│               │   └── __pycache__
│               ├── rviz
│               └── urdf
├── log
│  
└── src
    ├── my_robot_bringup
    │   ├── launch
    │   ├── rviz
    │   └── worlds
    └── my_robot_description
        ├── launch
        ├── rviz
        └── urdf

```

In order to spawn the robot in gazebo, use the following command:
```console
user@docker-desktop:home/tf1$ ros2 launch my_robot_bringup my_robot_gazebo.launch.xml

```
In order to visualize the robot on RVIZ for debugging purposes, use the following command:
```console
user@docker-desktop:home/tf1$ ros2 launch my_robot_description display.launch.xml

```

## Robot

### Robot TF tree

![image](https://github.com/user-attachments/assets/9f9d5964-cb65-4e65-878f-df18f96774af)

### Control
Gazebo Plugins retrieved from [ros-simulation repo](https://github.com/ros-simulation/gazebo_ros_pkgs/tree/ros2/gazebo_plugins/include/gazebo_plugins) were used to control and publish the joint state.

Once the robot has been spawned, run the following command to control the mobile base:
```console
user@docker-desktop:home/tf1$ ros2 topic pub /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.5}, angular: {z:0.0}} "
```
To control the manipulator use:
```console
user@docker-desktop:home/tf1$ ros2 topic pub -1 /set_joint_trajectory trajectory_msgs/msg/JointTrajectory '{header:{frame_id: arm_base_link}, joint_names: [arm_base_forearm_joint, forearm_hand_joint], points: [ {positions: {0.0, 0.0}} ]}'
```



