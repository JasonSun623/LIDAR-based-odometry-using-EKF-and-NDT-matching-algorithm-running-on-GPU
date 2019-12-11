# ndt_mapping_localization
C++ Implementation of the NDT mapping and localization algorithm for ADV on ROS.  

Two packages available in this implementation :

- **vehicle_mapping** : Pointcloud registration using the 3D NDT algorithm assisted by an EKF.
- **vehicle_localization** : 6-DoF Localization using the 3D NDT algorithm assisted by an EKF.

![NDT Results](/image.png)

**Dependecies :**

- **ROS** (http://wiki.ros.org/ROS/Installation)
- **robot_localization** (https://github.com/cra-ros-pkg/robot_localization)
- **PCL** (https://github.com/PointCloudLibrary/pcl)

**How to use :**
  
- **vehicle_mapping** :  
  
  1. Set up the topic names for GPS and IMU data in the vehicle_state/launch/ekf.launch and vehicle_state/param.ekf.yaml. For more information of how to use the robot_localization package, please see : http://docs.ros.org/lunar/api/robot_localization/html/index.html  
  2. Set up the topic names for Pointcloud and EKF Odom data in vehicle_mapping/launch/ndt_mapping.launch  
  3. Set up the path to save the final pointcloud in vehicle_mapping/launch/ndt_mapping.launch  
  4. Use *roslaunch vehicle_mapping ndt_mapping.launch* to launch the mapping package and play the rosbag that you want to use as input in an other terminal.
  
- **vehicle_localization** :  
  
    1. Set up the topic names for Pointcloud and EKF Odom data in vehicle_localization/launch/map_localization.launch 
    2. Set up the path to load the pointcloud map in vehicle_localization/launch/map_localization.launch 
    3. Choose which method to use to find the initial position. (RVIZ or GPS)  
    If you choose RVIZ, you will have to give a guess to the localization package on where to start using the "2D Pose Estimate" button in RVIZ  
    If you choose GPS, you will have to give the coordinates of the origin of your pointcloud map and set them up in vehicle_localization/launch/map_localization.launch.  
    *At the moment, the method based on RVIZ is more stable than the GPS one*
    4. Launch a rosbag throught another terminal, or launch live data streaming from the sensors.
    
**Demo**

We provide a pointcloud map built using the mapping package, and a rosbag recorded on a different day to test the localization package, which you can download from here : https://drive.google.com/open?id=1mqBURRoouFT1HYkWjkjENcotXf75Tz0u
  
If you still have problem running the packages, you can check the following videos demonstration how to use both the RVIZ and GPS approchaes : 
- RVIZ : https://www.youtube.com/watch?v=uujf0hiHXEE
- GPS : https://www.youtube.com/watch?v=1BxHPAaOFik
 
**Notes**  
- Sometimes, slowing down the rosbag playing speed (using -r) can improve the results of the localization package
- Tweaking the scoreThreshold parameter can also improve results

Please do not hesitate to report any problems or bugs you may encounter, either throught the issues page of this repo, or by sending an email to melhousni@wpi.edu and askulkarni2@wpi.edu.
