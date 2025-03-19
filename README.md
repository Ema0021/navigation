## Navigation Stack

We must install and run two Docker "ERF2024/dog_challenge" and "manipulation_task". For the second Docker conteiner you can follow the previously explained (git@github.com:lar-unibo/manipulation_task).

### How to launch the Navigation Stack ###
We must install and run two Docker "ERF2024/dog_challenge" and "manipulation_task". For the second Docker conteiner you can follow the previously explained (git@github.com:lar-unibo/manipulation_task).

For the first conteiner Docker you have to:
- open a terminal-> create a ros workspace ->on the terminal:  mkdir -p NAMEWORKSPACE_ws/src
- enter source directory-> on the terminal: cd NAMEWORKSPACE_ws/src
- check if you have git installed, otherwise -> on the terminal: sudo apt update & sudo apt install git
- clone the simulation package -> on the terminal: git clone https://github.com/ERF2024/dog_challenge.git (also in git@github.com:lar-unibo/dog_challenge)
- enter the simulation directory-> on the terminal: cd dog_challenge
- install docker (skip if already installed)-> on the terminal: ./scripts/install_docker.sh
- download the docker environment for the simulation-> on the terminal: ./start_framework.sh 
!!!!!IF you get an error regarding permissions try: sudo ./start_framework.sh

A ROS_MASTER should be started, alongside it a Gazebo world too.

For the second conteiner Docker you have to:
- In the new terminal create a NEW docker within the manipulation_task folder -> bash manipulation_task/docker/build.sh
- Run the NEW docker -> bash manipulation_task/docker/run.sh
- Access to Docker container using the command -> docker exec -it wolf-unibo-manipulation /bin/bash

Before launching the navigation stack, we need to compile the code and set up our workspace. 
In your Docker shell (BE SURE TO BE IN THE DOCKER SHELL) move to '$HOME/catkin_ws' and then use the following commands:

1) Compile the code:
```
catkin_make
```
2) Set up our workspace
```
source devel/setup.bash
```

Now we are ready to launch the node:

```
roslaunch go1_navigation robot_navigation.launch

```
This will open an RVIZ interface where you have access to the wolf_controller and wolf_navigation.
Where the first allows you to control the robot, while in "wolf_navigation", we have plugins to navigate the robot ("explorer","goto", "homing", "waypoint").

#### Notes:(find this folder in git@github.com:lar-unibo/dog_challenge)

- It could be necessary to restart the computer after running `bash manipulation_task/docker/build.sh` and ''.
- Use the `install_nvidia.sh` script in the `support` folder  if you are experiencing the following problem: `could not select device driver "" with capabilities: [[gpu]]` OR you can prove this erros open the start_framework.sh file, round line 139 you should find : "--gpus all \", completely erase the line (it tells the docker to search for a gpu) save and try again, it should work. 
- If you are experiencing this problem `nvidia-container-cli initialization error nvml error driver not loaded`, it probably means that your computer does not have the latest nvidia-drivers installed, so be sure that they are installed and updated to the last version.
  



