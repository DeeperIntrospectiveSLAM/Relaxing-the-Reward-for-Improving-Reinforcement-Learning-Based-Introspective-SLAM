# Relaxing-the-Reward-for-Improving-Reinforcement-Learning-Based-Introspective-SLAM

In this groundbreaking work, we reveal that the rewards used in current deep RL methods are overly rigid, stifling the agent's learning and resulting in inefficient routes. Our innovative, simpler reward system demands less exploration time, cultivates a tracking policy 2.5 times more robust, and achieves routes that are three times more efficient. We surpass numerous baselines across demanding routes that traverse multiple rooms, barren corridors, and sharp turns, setting a new standard in navigation.


[![Watch the video]]([https://youtu.be/VQ5cSm4JBDY](https://drive.google.com/drive/u/0/folders/1Akn_OD9mNORnfO2MPfNUQBmn6D-bD9V-))


Furthermore, we launched our training files for the research community to test our agent and reuse it for further improvements. 


## 1. Pre-requisites for training and testing

* Ubuntu 16.04, 18.04 or 20.04
* C++ 11 Compiler
* Pangolin 
https://github.com/stevenlovegrove/Pangolin.
* OpenCV 3.4 or higher
* Eigen3
Required by g2o (see below). Download and install instructions can be found at: http://eigen.tuxfamily.org. Required at least 3.1.0.
* MINOS simulator or any preferred simulator
https://github.com/minosworld/minos
* ORB-SLAM3
https://github.com/UZ-SLAMLab/ORB_SLAM3
* ROS

## 3. Environment Setup

For agent training and testing, we are using MINOS as a simulator. Localization and mapping are done with the help of ORB-SLAM3, and environment control is achieved via ROS topics. After successfully installing all prerequisites, follow these simple steps to set up the complete environment. 

### Camera Calibration

Copy the MINOS camera calibration file (MINOS.yaml) into the folder ORBSLAM3/Examples. 

### ROS NODE: 

This ROS node is important. Simply paste the attached ROS node (merger) in catkin_ws/src and make necessary changes to CmakeList.txt by Uncommenting the following:

*add_compile_options(-std=c++11)*

*add_executable(${PROJECT_NAME}_node src/merger.cpp)*

*target_link_libraries(${PROJECT_NAME}_node*
  
  *${catkin_LIBRARIES})*

*Add find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
image_transport
std_msgs
cv_bridge
)*


Later, catkin_make and test by running the following command:
 
*rosrun merger merger_node*

### Changes in MINOS simulator:

replace lines 98-102 with

if 'logdir' in params:

            self._logdir = '/home/frames'
            
        else:
            
            self._logdir = '/home/frames'


and replace line 422-428 with

*if self.params.get(‘save_png’):*

  *if image is None:*

  *image = Image.frombytes(mode,(data.shape[0], data.shape[1]),data)*

  *time.sleep(0.06)*

  *image.save(‘/home/frames/color_.jpg’)*

and save Simulator.py

### Bash File

Simply download the given bash file and from terminal run *bash start.sh*

This will start the SLAM3 and MINOS simulator. A rostopic will also be initiated in parallel by this file which is responsible for publishing images over SLAM3. 


## 4. Train and Test the agent

* Download the agent_dqn.py 
* Change the parameters as per your system and requirements.
  

*python3 agent.py --dqn_test*

*python3 agent.py --dqn_train*





