
<h1 align="center"> Robotics Project </h1> <br>
<h3 align="center"> Planning, Developing, Learning ROS </h3> <br>
<p align="center">
University Of Burgundy (VIBOT)
  <p align="center">
      <img src = "vibot.png" width=60>
  </p>
</p>

<h3 align="center">                       
</h3>
<h4 align="center">                       
By: <br>  
 Mahmoud Badran,  Arsalan Khawaja
</h4>
<p align="center">
  <p align = "center">
     <img  src = "https://www.ros.org/news/2016/05/23/kinetic.png" width=400>
     <img  src = "resources/turtlebot3.jpg" width=400>
    
  </p>
</p>

[![Generic badge](https://img.shields.io/badge/Report-100-green.svg)](https://shields.io/)
[![Generic badge](https://img.shields.io/badge/Development-30-red.svg)](https://shields.io/)
[![Generic badge](https://img.shields.io/badge/Ros-kinetic-green.svg)](http://wiki.ros.org/kinetic/Installation)
[![Generic badge](https://img.shields.io/badge/Platform-IgniteAcademy-blue.svg)](https://www.theconstructsim.com/)





## Project Management (Technical Report)

- [Introduction](#introduction)
- [Project Tasks](#Project-Tasks)
- [Analysis OF Studied Techniques](#Analysis-OF-Studied-Techniques)
- [Work Plan](#Work-Plan)
- [Conclusion](#Conclusion)
- [References](#References)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Introduction
Robotics Operating System (ROS), is a middleware, low level framework, to write robotic softwares. It can be cosidered as an API to make the process of developing a robotic related projects more flexible, and simplified. There will be no need for an extensive knowledge of the hardware in which it saves much effort and time in the development phase. It includes many libraries and tools which connects and control the robot manipulators, handle the communication between multiple devices in a a working space. <br>
ROS is supported by many operating systems like ubunto, windows. Ubunto is the more stable operating system working with ROS. However, for the development of this project we are using the construct web plaform, which is an online robotics working environmant. The platform uses ubunto as the main operating system with ROS kinetic and uses the **Gazebo** as real world simulator with many robot model simulations like turtlebot 3. The platform will enable us to learn some of ROS basic techniques to be able to apply Robot Control, Mapping, Robot Localization, Path planning and setting up some goals to navigate through the environment.  

## Project Tasks 
The project goal is to apply the learned **ROS** techniques and pakages to apply the navigation task on Turtlebot3:  
- Moving the robot around the environment using **/cmd_vel** topic. <br>
- Construct a map of the whole environment. We need to fully occupy the whole environment, then we need to localize the Robot. <br>
- Path planning, we need to publish a goal to move base navigation system in which Turtlebot3 can reach
that goal without colliding with any obstacles. <br> 
- Create waypoints that allows Turtlebot3 to navigate within the environment. 

## Analysis OF Studied Techniques

- Important concepts that have been studied and will be important in developing the project : <br><br>
   - **Nodes**: One of the most important concepts in ROS. We can describe nodes as a program (python, c++) to enable ROS to make communication tasks. A node can subscribe or publish to a topic, which will be explained. <br><br>
   - **Topic**: The process of transmitting data between nodes. Some nodes are responsible for publishing some data to a specific topic where other nodes (subscribers) will be able to request these data ( messages ) from the topic.<br><br>
   - **Messages** : Data structure which describes the data that ROS nodes publish or recieve. the nodes communicate, send messages, receive messages through topics.<br><br>
   - **Services** : another way to transmit the data between nodes. it is a synchronous operation where the robot has to stop processing while waiting for a service response.<br><br>

  <p align="center">
    <p align = "center">
       <img  src = "XCndTVvlwmaG.png" width=700>
    </p>
  </p>
  
- ROS Packages & Basic Commands : <br>
   - A package in ROS is a working directory which contains all the necessary ROS files like executable python and cpp files, configuration and combilation files and launch files. 
   - The structure of the package directory:<br> 
      - **src** folder which contains all the executable files 
      - **launch** folder which contains all the launch files
      - **package.xml** file which contains other packages dependencies and url paths. In case we want to be able to call other packages from this package. 
      - **CMakeLists.txt** file which contains some cpp compilations and building commands. 
    - The main working space in ROS is called **catkin_ws**. It is a directory where all our ROS packages are installed.  
    - We can move to any package using **roscd** <br> 
     ```roscd <package_name>```
    - ROS programs(nodes) can be executed using launch files, with launch files we can run multiple nodes in one file. A launch file can be run using **roslaunch**  command: <br> 
    ```roslaunch <package_name> <launch_file>```
    - If we want to create a package in the working space **catkin_ws**, we use this command: <br>
      ``` catkin_create_pkg <package_name> <package_dependecies> ```
    - If we want to know some information about a specific node, we use this **rosnode** command: <br> 
      ``` rosnode info <node_name>``` 
    - If we want to know some information about a specific topic, we use this **rostopic** command: <br> 
      ``` rostopic info <topic_name>```  
    - If we want to know some information about a specific message, we use this **rosmsg** command: <br> 
    ``` rosmsg show info <msg_name>```  <br> 
    - An important command needed to be running before start working with any ROS project called **roscore**. It contains all the necessary files for any ROS system.
      

## Work Plan

```
Task 1: Robot Control
```
We use TurtleBot3, which is a mobile robot with small size and low price but still have the same quality that other mobile robots have.
- First of all, it is necesseary to start and launch our turtlebot3. It is done using the **turtlebot3_bringup** package and starting **turtlebot3_remote.launch**. file. <br> 
 ```<include file="$(find turtlebot3_bringup)/launch/turtlebot3_remote.launch" />``` <br> 
- One important command we can use to know what are the topics that got published by the environment. <br> 
```rostopic list``` <br> 
By executing this command, we can see all the topics provide by the environment. One of the topics that should be provided to move the robot is **/cmd_vel**:   

- With this topic we can publish velocity information to the robot. if we want to know more information about this topic we can execute this command: <br> 
   - ```rostopic info /cmd_vel ``` <br> 
       After running the command we can see that this topic uses **Twist** type messages. So, this topic recieves data of type Twist (angular and linear         velocities ,(x,y,z)). To know more information about the message we execute this command: <br> 
       ```rosmsg show geometry_msgs/Twist``` <br> 
       See the Figure below : <br> 
       <p align="center">
          <p align = "center">
             <img  src = "resources/twistmsg.png" width=200>
          </p>
        </p>
         
- TurtleBot3 receives the velocity information by subscribing to this topic. The topic will provide the robot translation and rotation data. 
- We can publish to this topic by running this command: 
  ```rostopic pub /cmd_vel  TAB TAB```
  And then in the terminal we can edit the values of the two vectors. 
- Otherwise, we can create a launch file to run a node responsible for publishing velocity information to the robot. see the code below: <br> 
   ```self.pubNode = rospy.Publisher('/cmd_vel', Twist, queue_size=1)``` <br> 
   ```self.msgTwistObj = Twist()``` <br> 
   ```self.msgTwistObj.linear.x = 0.2 ```<br> 
   ```self.pubNode.publish(self.msgTwistObj)``` <br> 
   Here, we create a vairable called **pubNode** that is responsible for publishing Twist information to **cmd_vel** topic. And another variable called **msgTwistObj** that holds Twist message values. As you can see in the last command , we added 0.2 value to the x linear position of the robot.The last command, we used 'publish()' function to publish the new updated message values. <br> 
- Another topic we use is **/scan** topic, we use this topic to get the laser information, readings from the robot. For example, the distance between the robot and a wall in the environment. The message used is of type **LaserScan**. See the commands below:<br> 
```self.subNode = rospy.Subscriber('/scan', LaserScan, self.callback)```<br> 
```self.laserMsg = LaserScan()```<br> 
    In our node, we create another variable called **subNode** to subsicribe to **/scan** topic. And another variable called **laserMsg** which holds a laser information and readings.  The **callback** parameter in the Subscriber function is a function that have the updated laser information. see command bellow:<br> 
    ```def callback(self, msg):```<br>
        ```self.laserMsg = msg```<br>   
    ```self.laserMsg.ranges```   <br> 
   So, whenever the robot moves, the variable **laserMasg** will be updated. One of the useful information we can obtain from **laserMsg** is the **ranges** parameter. we use **ranges** parameter to know the distance between the robot and an object in the environment. <br> 
   See the Figure below. It shows different frames of the robot after launching the node that is responsible for moving the robot. **Explain More About Ranges**

<p align="center">
  <p align = "center">
     <img  src = "resources/r1.png" width=350>
    <img  src = "resources/r2.png" width=350>
    <img  src = "resources/r3.png" width=350>
    <img  src = "resources/r4.png" width=350>
  </p>
</p>
<br><br><br>

``` 
Task 2: Mapping & localization 
```
<br>
<h4 align="center"> <ins> Mapping </ins> </h4>

To start the autonomus navigation process, the robot must have a map of the environment to be able to recognize objects, walls where it will allow the robot to plann trajectories through environment. <br> 
In order to construct a map : <br> <br>


- Launch TurtleBot3 (Explained in Task1) 
- To start of the mapping process we need to use **gmapping** package that provides **slam_gmapping** node. 
    This node is implementing the gmapping **SLAM** algorithm. It creates a 2D map of the environment using the data the Robot is providing during movement like       laser data, in which it will be transformed to an Occumaoncy Grid Map (OGM) data format (**nav_msgs/OccupancyGrid.msg**) where it represents a 2-D grid map and each cell of the grid represents the occupancy ( if the cell is completely occupied or completely free). <br>
    Start the mapping process by adding this command to the launch file: <br>
    ```   <node pkg="gmapping" type="slam_gmapping" name="turtlebot3_slam_gmapping" output="screen">``` <br><br>
    
- In the mapping process, an important tool is used called **RViz**. It will help us in visulising th map creation process, it will allow us to see what the robot is covoring from the environment. <br>   
To launch Rviz. Execute this command: ``` rosrun rviz rviz ```
    <p align="center">
    <p align = "center">
       <img  src = "resources/screen.png" width=600>
    </p>
    </p>
- You can see in the figure above **Rviz**. In the left, we can see the displays which can be addded by us. we are interested in three displays which are:
    - **Map**: visulize the map. Topic is **/map** where it has message of type Occupancy Grid Map **OGM**, ```nav_msgs/OccupancyGrid.msg ```  <br> 
    - **LaserScreen**:  visualze what the Lazer on the robot is detecting. Topic is **/scan**<br>
    - **RobotModel**:  localize the Robot on the map.<br><br>
- After launnching **slam_gmapping** and **RViz**, we can start moving the robot by executing Kerbord control command:<br> 
  ```roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch ```.<br> After moving the robot around all the places needed we should see the map fully occupied in **Rvis**<br>
    <p align="center">
    <p align = "center">
       <img  src = "resources/screen2.png" width=600>
    </p>
    </p> 
- The map can be saved using **map_server** package, it includes **map_savor** node  which will allow us to access the map data. 
    Execute this command : <br> 
    - ``` rosrun map_server map_savor -f <file_name> ```
 After executing it will generate two files: <br><br>
       - **file_name.pgm:** PGM stands for Prtable Gray Map where it contains the Occupancy Grid Map(OGM) data. If we download the file and open it, it will look like this: 
      <p align="center">
      <p align = "center">
         <img  src = "resources/mahmap.png" width=350> <br>
        <em>Each cell ranges from 0 to 100 integer value where 0 means completely free and not occupied, 100 is completely occupied</em>
      </p>
      </p>
      
       - **file_name.yaml:** This file contains the meta data of the generated map which contains these parametrs, image,resoulution, origin, occupied_thresh, free_thresh,negate. 
 
--- 
 
<h4 align="center">  <ins> Localization </ins> </h4>

After creating the map, the next step is to locate the robot in the environment (created map). We can define localization as the process of finding the location of the robot in respect with the environment. For now, we have the map of the environment created, and we have sensors located on the robot which will observe the environment then we do localization to estimate the coordinates and angles of where the robot is located in the environment. 

- To apply localization, we use **AMCL (Adaptive Monte Carlo Localization)** package which provides **amcl** node. It is a localization system that implements Kullback-Leibler(Monte Carlo) algorithm which uses an adaptive practicale filters to track the position of the robot in repect with the environment. <bR> 
  
    **What is Monte Carlo Algorithm ?** <br>
    An algorithm which is responsible for generating many future guesses (Particles) of the robot expected movements in the environment. When the robot starts moving, the algorithm starts generating Particles and then uses the obtained sensor information (**/scan**) to create an optimised robot movement ( make all the created Particles head to the right direction). See below Table which describes the topics subscribed and published by AMCL.<br><br> 
    Subscribed Topics (message type) | published Topics (message type) 
    ------------ | -------------
    **map** (``` nav_msgs/OccupancyGrid```) | **amcl_pose** (```geometry_msgs/PoseWithCovarianceStamped```)
    **scan** (```sensor_msgs/LaserScan```) | **particlecloud** (```geometry_msgs/PoseArray```)
    **tf** (```tf/tfMessage```) | **tf** (```tf/tfMessage```)
    
     <br>
     
    - **map:** amcl subscribe to map topic to get the map data (OGM), to used it for localization. 
    - **scan:** To have the updated scan readings. 
    - **tf:** Transform topic which is necessery to provide the relationship between different reference frames. For example, translate from the base_laser (reference frame of the laser) coordinate frame to base_link(reference frame for the center of the robot) coordinate frame. 
    - **amcl_pose:** amcl node publishes the position of the robot in the environment to the amcl_pose topic.
    - **particlecloud:** amcl publishes the particle cloud of arrows created by the system to measure the uncertainty of the robot current position. see the figure below (red arrows displayed using Rviz,add **PoseArray** display which subscribe to **PointCloud** topic). <br>
- To launch amcl and start the localization process, we create a launch file which includes:

    - Launch TurtleBot3 applications: <br> ```<include file="$(find turtlebot3_bringup)/launch/turtlebot3_remote.launch" />```
    - Call our generated map file:<br> ```<arg name="map_file" default="$(find pkg_name)/maps/map.yaml"/>```
    - Run map server node with our generated map:<br> ```<node name="map_server" pkg="map_server" type="map_server" args="$(arg map_file)" />```
    - Launch amcl node:<br> ```<node pkg="amcl" type="amcl" name="amcl">``` <br>
    - AMCL node depends on some parameters like **min_particles**, **max_particles**. These parameters decide the number of particles used in the localization   process. We add the parameters in the launch file: <br>
       ```<param name="min_particles" value="500"/>``` <br>
       ```<param name="max_particles" value="3000"/>```

        <p align="center">
        <p align = "center">
        <img  src = "resources/particles.png" width=500> <br>
        <em> Generated Particles</em>

        </p>
        </p>
        
     - We use Rviz **2D Pose Estimate** button to send the navigation system an initial pose of the robot. The last thing is to start moving the robot around the environment by using **turtlebot3_teleop** package. <br><br>  
      
``` 
Task 3: Path Planning
```
<br> 

- After creating a map, localize the robot, we need to plan a path, trajectory for the robot to follow to reach a specific goal while avoiding obstacles along the way. To achieve this, we need to use **move_base** package which provides **move_base** node. This package is the base of the navigation task where it connects all the navigation components. See the figure below: 
  <p align="center">
  <p align = "center">
     <img  src = "resources/navtask.png" width=900> <br>
     <em>Navigation Task</em>
  </p>
  </p>
  
 - The figure shows how the **move_base** node interact with other system compnents. The node implements **SimpleActionServer** from **actionlib** package with message of type **gemetry_msgs/PoseStamped**. Tha Action server provides **/goal** topic that will provide the **move_base** node with goal position. See table below to see description of some topics move_base node subscribe to and publishes. <br><br>

  
     Topics | Message |Description  
    ------------ | ------------ | -------------
    **move_base/goal** (``` subscribed```)|  ```move_base_msgs/MoveBaseActionGoal ``` |  Provide goal position using **SimpleActionServer** which will allow us to track the current goal position status. 
    **move_base_simple/goal** (``` subscribed```) |   ``` gemetry_msgs/PoseStamped```  | Provide goal position to **/move_base** node directly without using **SimpleActionServer**.
    **/cmd_vel** (```published```) | ``` geometry_msgs/Twist```  |  Publish velocity information to the robot (base controller to make transformation). 
    <br> 
- **SimpleActionServer** provides topics like goal(**move_base_simple/goal**), Feedback (**/move_base/feedback**), Result(**/move_base/result**). 
    - **FeedBack**: Keeps updating the server about the current information of the robot along the path (current position, laser information).For example, if we create a goal and the robot start to move toward the goal. If we display the message from the FeedBack topic we will see real time updated information in the teminal. Execute this command. <br> 
      ```rostopic echo move_base/feedback```
    - **Result**: It is sent only once, a final pose of the robot is sent by the server to the move_base node When the robot reaches the goal.
       
   
- As you can see in the Navigation Task Figure above, there are parameters required to be loaded to the **/move_base** node: 
   - **Global Planner:** The new goal, when recieved by move_base node, will be sent to the Global Planner. It will be responsible for building a safe plan for the robot to avoid collisions, obstacles along the way to the goal. It is called global because it starts planing the path from the begining for the whole map and it doesn't depend on the current laser information provided by the robot. <br> 
   - **Local Planner:** The local planner uses only the information currently prvided by the robot sensor reaings and plans a path within a small area surrounding the robot position. When the next set of information come in it plans a new piece of the path. 
   - **Costmap paremeters (local & global):** the costmap parameters are responsible for storing the information related to obstacles in the environment(map). The global costmap is a static map used to store information about the whole map to be used for global planning where local costmap is used to store local information (the small area surrounding the robot position) to be used for local planning. 
     <p align="center">
    <p align = "center">
       <img  src = "resources/globalcostmap.png" width=400> 
       <img  src = "resources/localcostmap.png" width=400> <br>
       <em>Global Costmap - Local Costmap</em>
  </p>
  </p>
  
 - To implement path planning with obstacle avoidance, we create a launch file where it includes the map_server package to get the map data, amcl package to localize the robot , and move_base package with its parameter configuration. As explained, move base node requires some parameters to be loaded. To configure and add move base node, we execute the following commands:  
   -  To launch the node:<br>
   ```  <node pkg="move_base" type="move_base" respawn="false" name="move_base" output="screen">" ```
   - Load the required files (local & global costmaps | local & global planners). All the required parameters are included in these yaml files: 
     ``` 
     <!-- rosparam is used to load parameters from yaml file-->
          <rosparam file="$(find t3_navigation)/param/costmap_common_params_$(arg model).yaml" command="load" ns="global_costmap" />
          <rosparam file="$(find t3_navigation)/param/costmap_common_params_$(arg model).yaml" command="load" ns="local_costmap" />
          <rosparam file="$(find t3_navigation)/param/local_costmap_params.yaml" command="load" />
          <rosparam file="$(find t3_navigation)/param/global_costmap_params.yaml" command="load" />
          <rosparam file="$(find t3_navigation)/param/move_base_params.yaml" command="load" />
          <rosparam file="$(find t3_navigation)/param/dwa_local_planner_params.yaml" command="load" />
       ```
        
- To create a goal, we can use Rviz. <br> 
   - Launch move_base node. The map should be created and the robot localized. (Turtlebot3)  
   - Run Rviz and add add all necessary displays to visualize the navigation process. 
   - To visualize the **local costmap**, **global costmap**, we add two **Map** display elements and attach them to **/move_base/local_costmap/costmap** and      **/move_base/global_costmap/costmap**  topics respectively. 
   - To visualize the **local plan**, **global plan**, we add two **Path** display elements and attach them to **/move_base/DWAPlannerROS/local_plan** and **/move_base/NavfnROS/plan** topics respectively.  
   - In Rviz, we choose **2D Pose Estimate** button to initialize the robot pose. Then we choose the **2D Nav Goal** button and click on the position where we want our turtlebot3 robot to move (goal). 
   - After creating a goal, a goal message (**gemetry_msgs/PoseStamped**) will be published to **/move_base/goal** topic. 
   - The goal message we published to **/move_base/goal** topic will be recieved by **SimpleActionServer** which is implemented in the move-base node. So, the      goal information will be recieved by the move_base node with goal topic provided by **SimpleActionServer** with message type **move_base_msgs/MoveBaseActionGoal** 
   - We can run this command to see what has been published to goal topic: <br> 
     ```rostopic echo /move-base/goal```
     <p align="center">
        <p align = "center">
           <img  src = "resources/1.png" width=350>
          <img  src = "resources/2.png" width=350><br>
           <em>Initialize Robot Pose Using 2D Pose Estimate </em>
        </p>
      </p>
       <p align="center">
        <p align = "center">
           <img  src = "resources/3.png" width=350>
          <img  src = "resources/4.png" width=350><br>
          <em>Set A Goal Using 2D Nav Goal And Start Moving Toward The Goal </em>
        </p>
      </p>
     
- We can create a goal by directly publishing to the goal topic. By executing this command: 
   -  ```rostopic pub /move_base/goal/ move_base_msgs/MoveBaseActionGoal```
   
- Another way we can create our goal is by creating an action client program(node) that send a goal to move_base. 
   - Initalize the node and create Publisher to publish the goal to **move_base** node. 
      ```
        rospy.init_node("GoalSender")
        pub = rospy.Publisher("move_base/goal", MoveBaseActionGoal)
        ```
          
    - Import all the move base package messages. Execute the following: <br> 
      ```from move_base_msgs.msg import ``` 
      
    - Create a function to send the goals. Inside the function we initalize a goal object from **MoveBaseActionGoal** and then we configure the goal parameters (position). Finally, we call the function to publish the goal. See below: 
      ``` 
          def GoalSender(publisher):
            goal = MoveBaseActionGoal()
            goal.goal.target_pose.header.frame_id = "map"
            goal.goal.target_pose.pose.orientation.w = 1.0
            goal.goal.target_pose.pose.position.x = 0
            goal.goal.target_pose.pose.position.y = -5
            publisher.publish(goal)
          GoalSender(pub)
        ``` 

      The **MoveBaseActionGoal** has a **goal** parameter of type **MoveBaseGoal.msg** which has the **target_pose** parameter of type **geometry_msgs/PoseStamped.msg** that will allow us to create a goal.
      
- To send goals using **SimpleActionServer**. 
   - We create a node and import the necessary packages like actionlib. 
      ``` 
          import actionlib
          from move_base_msgs.msg import MoveBaseAction, MoveBaseGoal
       ```   
   - Initialize an action server. So we create a move_base action client (**SimpleActionClient**). <br> 
      ```
      client = actionlib.SimpleActionClient('move_base',MoveBaseAction) 
      # this command to wait for the server to start listening for goals.
      client.wait_for_server()
      ```
   - Create a goal to send to the server. <br> 
      ```
          # Create a goal with the MoveBaseGoal directly
          goal = MoveBaseGoal()

          # Configure the parameters 
          goal.target_pose.header.frame_id = "map"

          goal.target_pose.header.stamp = rospy.Time.now()

          # Translate 0.8 meters along the x axis w.r.t. map reference frame 
          goal.target_pose.pose.position.x = 0.8

          # No rotation of the mobile base frame w.r.t. map reference frame
          goal.target_pose.pose.orientation.w = 1.0
        ```
      
   - Send the goal to the action server we created.  
     ```
        # Sends the goal to our action server.
        client.send_goal(goal)
        # Waits for the server till the end of the process.
        wait = client.wait_for_result()
       ```
  
   

- Now Turtlebot3 is able to navigate through the environment and follow a safe path without any obstacle collisions.<br><br>

``` 
Task 4 : Create WayPoints  
```
<br>
<h4 align="center"> <ins> WayPoints  </ins> </h4>

If we want the robot to pass through multiple waypoints(goals) before reaching its destination, we can use a package called **follow_waypoints** where it will be responsible for storing these waypoints. This package will publish the stored waypoints to **move_base** node as a sequence and then the robot will reach the goal by navigating through all the waypoints.

- To install this package, we need to clone its [GITHUB](https://github.com/danielsnider/follow_waypoints) repository into our catkin src folder : <br> 
   ```git clone https://github.com/danielsnider/follow_waypoints.git``` <br>
   After installing the package we need to be build our catkin_ws working space again, so we change the current directory to catkin_ws and then we execute: 
   ```catkin_make```
   ```source /devel/setup.bash``` <br> 
   Now, we have **follow_waypoints** package ready. 
- To start the waypoint server, we first start the navigation task process we implemented before: <br> 
  ```roslaunch <our navigation package> <our launch file.launch>```
- Now we launch **follow_waypoints**: <br> 
  ```roslaunch follow_waypoints follow_waypoints.launch```  <br> 
- The waypoint server listen to **initialpose** (**amcl** and **follow_waypoints** subscribe to this topic) that is used to initialize the robot with message type    ```geometry_msgs/PoseWithCovarianceStamped```. The server will store all the waypoints and then will provide it to **move_base** node to start navigating through all the specified waypoints. 
- After launching all the necessary packages, we can start creating waypoints using **Rviz** and we add **PoseArray** display element(see Figure below) and we add **waypoints** topic to this display. We run **Rviz** tool with already implemented configuration this time .<br> 
   ```rosrun rviz rviz -d `rospack find turtlebot3_navigation`/rviz/turtlebot3_nav.rviz```. <br> 
    <p align="center">
        <p align = "center">
           <img  src = "resources/posearray.png" width=250> <br> 
           <em> PoseArray Display Element</em>
        </p>
      </p>
   
    
   - Use **2D pose Estimate** to localize the Robot. 
   - Use **2D Nav Goal** to add goals (waypoints). 
       <br> 
       <p align="center">
        <p align = "center">
           <img  src = "resources/initRobotPose_WayPoint1.png" width=250>
          <img  src = "resources/waypoint2.png" width=250><br>
           <em> Initial Pose Of the Robot | WayPoint 1</em>
        </p>
      </p>
       <p align="center">
        <p align = "center">
           <img  src = "resources/waypoint3.png" width=250>
          <img  src = "resources/waypoint5.png" width=250><br>
          <em> WayPoint 2 | WayPoint 3(The last waypoint we choose should be in the same position as the initial Robot pose) </em>
        </p>
      </p>
      
       
      
 - Now that we added our waypoints . We should start the **path_ready** topic (**follow_waypoints** subscribes to this topic to initaize the process to follow our waypoint), then it will start sending the waypoints we created to move_base node. This topic has message of type ```std_msgs/Empty```. To start the **path_ready topic**, we execute: <br> 
 ```rostopic pub /path_ready std_msgs/Empty -1```    
  After that, our Robot will start following the created waypoints. 
  
- If we want to create our own custom sequence of waypoints and implement the navigation through all the points autonomously, let's execute the following: 
   - First, we set up waypoints locations. So, what we need is a coordinates of the waypoints with respect to map reference frame. To implement that, we create a list or a dictionary of our waypoint coordinates.
      ```
      # Create the dictionary 
      locations = Dict() 
      # add our waypoint names and values. 
      locations['waypoint1'] = Pose(Point(0.5, 4.0, 0.000), Quaternion(0.000, 0.000, 0.223, 0.975))
      locations['waypoint2'] = Pose(Point(-1.3, 2.382, 0.000),Quaternion(0.000, 0.000, -0.670, 0.743))
      locations['waypoint13'] = Pose(Point(-3.756, 6.401, 0.100), Quaternion(0.000, 0.000, 0.733, 0.680))
      ```
      We can get these coordinates by using Rviz tool. Press the 2D Nav Goal button and click on the location of the waypoint we want. The coorinates will be displayed on the terminal. 
      
      
   - Subscribe to move_base action server. <br> 
      ```
      import actionlib, rospy
      from move_base_msgs.msg import MoveBaseAction, MoveBaseGoal
      from geometry_msgs.msg import PoseWithCovarianceStamped, PoseArray,Pose,Quaternion,,Twist
      # subscribe to action server 
      client = actionlib.SimpleActionClient('move_base',MoveBaseAction) 
      # this command to wait for the server to start listening for goals.
      client.wait_for_server()   
      ```
   - Create a variable to hold the initial position of the robot w.r.t the map.<br> 
     ```
      # With msg type PoseWithCovarianceStamped. 
      initial_pose = PoseWithCovarianceStamped()
      ```
     
     ```
      # This line of code is used when to get the initial position using RViz (The user needs to click on the map) 
      rospy.wait_for_message('initialpose', PoseWithCovarianceStamped)
     ```
   - Subscribe to **initialpose** topic with callback function called **update_initialpose_callback** to update the initial_pose variable with the current initial pose. 
        ```
        # Subscribe to initialpose topic 
        rospy.Subscriber('initialpose', PoseWithCovarianceStamped,update_initialpose_callback)
        # callback function to update the initial_pose vaule to the current initial pose. 
        def update_initialpose_callback(initial_pose):
          initial_pose = initial_pose
        ```  
   - Start the process of sending goals(waypoints) to move_base action server. We take a sequence of waypoint locations from the dictionary we created and then we iterate over the sequence to navigate through all waypoints. 
     ```
       # Set up a goal location
       goal = MoveBaseGoal()
       #location = ['waypoint1', 'waypoint2', 'waypoint3']
       goal.target_pose.pose = locations[location]
       goal.target_pose.header.frame_id = 'map'
      
       # For the user, to know where the robot is moving (to which waypoint)
        rospy.loginfo("Going to: " + str(location))

        # Send the goal(current waypoint) to move_base action server 
        client.send_goal(goal)
        ```  
   

  - The custom waypoints program is not a fully complete code, or a correct program. but a sample of how we could implement the process. See reference [3]. 

  

## Conclusion

## References
  - [WIKI ROS](http://wiki.ros.org/)
  - [The Construct Platform](http://theconstructsim.com)
  - ROS By Example, A Do-It-Yourself Guide to the Robot Operating System, VOLUME 1, A PI ROBOT PRODUCTION, R. PATRICK GOEBEL. Section 8.5.3 [Book](https://drive.google.com/file/d/1aZ8jmMl6UAiN0Qi_xSbD2nOgiCnx72y3/view)

