# Homework 3

In this repository, we demonstrate teleoperation and obstacle avoidance behavior with a simulated ROBOTIS TurtleBot3 using Ubuntu 20.04 and ROS Noetic. The teleoperation is done using the keyboard and the obstacle avoidance is done using a LiDAR sensor.

## Setup

### Docker (Recommended)
First, install Docker and Docker Compose using the official install guide.

To run Docker containers with NVIDIA GPU support, you can optionally install the NVIDIA Container Toolkit.

First, clone this repository and go into the top-level folder:
```bash
git clone https://github.com/abhijaysingh/enpm690_hw3.git
cd enpm690_hw3
```

Build the Docker image:
```bash
docker build -t nvidia_ros ./docker/
```

### Local Setup
If you do not want to use Docker, you can directly clone this package to a Catkin workspace and build it provided you have the necessary dependencies. As long as you can run the examples in the TurtleBot3 manual, you should be in good shape.

First, make a Catkin workspace and clone this repository:
```bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
git clone https://github.com/abhijaysingh/enpm690_hw3.git
rm -rf enpm690_hw3/docker/obstacle-avoidance-turtlebot/
```

Then, build the package:
```bash
cd ~/catkin_ws
catkin_make
```

## Usage

### Docker
To run the Docker container, use the following command:
```bash
docker run -it --net=host --gpus all \
    --env="NVIDIA_DRIVER_CAPABILITIES=all" \
    --env="DISPLAY" \
    --env="QT_X11_NO_MITSHM=1" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    nvidia_ros \
    bash
```

Once inside the container, launch Gazebo with the TurtleBot3:
```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

#### Teleoperation
To run the teleoperation demo, open a new terminal and run the following command in the container:
```bash
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```

#### Obstacle Avoidance
To run the obstacle avoidance demo, open a new terminal and run the following command in the container:
```bash
roslaunch obstacle-avoidance-turtlebot naive_obs_avoid.launch
```

### Local
To run the package, first source the setup file:
```bash
source ~/catkin_ws/devel/setup.bash
```

Then, launch Gazebo with the TurtleBot3:
```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

#### Teleoperation
To run the teleoperation demo, open a new terminal and run the following command:
```bash
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```

#### Obstacle Avoidance
To run the obstacle avoidance demo, open a new terminal and run the following command:
```bash
roslaunch obstacle-avoidance-turtlebot naive_obs_avoid.launch
```



