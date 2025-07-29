---
layout: project
permalink: /:title/
category: class_projects

meta:
  keywords: "ROS2, MoveIt, Computer Vision"

project:
  title: "Balloon Volleyball with a 7-DOF Robot Arm"
  type: "ROS2 | MoveIt | Computer Vision"
  url: "https://github.com/Dilan-Wijesinghe/AirTrafficControl"
  logo: "/assets/images/projects/balloon_volleyball/balloon_move.gif"
  date: Dec. 8th, 2022

---
<br>
<div class="h2">Worked With:</div>
<p>Dilan Wijesinghe, Rintaroh Shima, Muye Jia, Hanbing Wu</p>
<br>
<span class="h2">Skills:</span>
<p> ROS 2, Computer Vision, MoveIt</p>

<span class="h2">Description</span>
<p>The objective of this project is to play the game 'Don't let the balloon drop to the ground' with a Franka Emika Panda arm. With the help of a RealSense D435i camera, our robot tracks a falling balloon in real time, predicts where the balloon will land, and moves to the location before the balloon falls. The robot then taps the balloon back up into the air, and waits for the balloon to start falling before intercepting it again. A person can also play alongside the robot, tapping the balloon back into the robot's workspace.
</p>
<br>

<img src="/assets/images/projects/balloon_volleyball/balloon_move.gif" alt="balloon volleyball">


The project can be split into three main categories: motion planning, perception, and dynamics predictions.
<p style="margin-left: 5%;" markdown="1">

`motion_planning`: My main role in the project was creating asynchronous calls to plan a trajectory to goal cartesian position in (x, y, z) space given the robot's current position. As of 2022, ROS2 Humble did not have a MoveIt2 interface yet, and so my role was to communicate with topics and message types to execute trajectories. All motion seen in the video is done with our "custom MoveIt2" package.
</p>
<br>
<p style="margin-left: 5%;" markdown="1">
`perception`: The perception pipeline was built using open source computer vision packages and a RealSense RGB-D camera, with the goal of tracking the red balloon in 3D space in real time. 
</p>

<br>
  <img src="https://dilan-wijesinghe.github.io/assets/img/gifs/balloon_tracking.gif" alt="perception">
<p style="margin-left: 5%;" markdown="1">
`dynamics predictions`: The two main dynamics to consider were the motion of the balloon and the "jerking" upward motion for the robot to intercept the balloon. Initially, we were using an EKF to predict the trajectory of the balloon, but it wasn't quick enough to predict in real time. Instead, we switched to basic, first-order integration to track the balloon. The upward motion of the robot was achieved by executing a trajectory 0.1m above the target with a 5.0x velocity scaling.

</p>