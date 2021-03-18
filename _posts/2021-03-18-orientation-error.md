---
layout: post
title: Orientation Error
date: '2021-03-18T19:00:00.002-04:00'
author: Mahyar
tags:
- Robotics
- Python
---
# Robot Control
The job of the robot controller is to convert the task specification to forces and torques at the actuators. Control strategies include motion control, force control, hybrid motion/force control, or impedance control. Which of these behaviors is appropriate depends on both the task and the environment. For carrying out any task in any environment, we need to control force or motion in the required direction. Please remember that this "or" is exclusive. In other words, if the robot imposes a motion then the environment will determine the force, and if the robot imposes a force then the environment will determine the motion. The following is the use cases according to the demands of typical robotic applications: 
1) Standard industrial application: 
• pre-programmed task 
• external interface (if any) only necessary for synchronization
2) Advanced industrial application with non-continuous feedback control: 
• pre-programmed task 
• external sensors, but only discrete measurements 
• no continuous feedback control (“look-then-move”) 
• industrial controller does path planning, interpolation, inverse kinematics, etc.
• simple interface sufficient (exchange of data without real-time requirements)
• real-time / non-real-time vs. (non-)continuous are two different issues
3) Advanced industrial application with continuous feedback control: 
• pre-programmed task 
• external sensors used for feedback control 
• examples: cameras, FT sensor, … 
• major part of the application is programmed on an industrial controller
• sensor data processing is programmed outside robot controller
• low cycle time and minimal dead time of feedback control are important for sensor-based control? real-time interface: exchange of data in fixed time intervals (e.g., interpolation cycle time)
4) Research outside the robotics field: 
• robot is used for research outside the field of robotics, e.g., the robot is used to automate measurements 
• use cases 1-3 are applicable
5) Robotics research – system/application level: 
• robot is used as part of a larger system to realize and evaluate new applications in the area of cognitive systems, service robotics, etc.
• integration of robot controller in other systems should be easy
• functionality of robot controller should be controllable from outside
6) Robotics research – control level: 
• robot is used to implement and evaluate new robotics algorithms in the area of control, e.g., inverse kinematics, dynamics, force control, …
• robot control at the low level (real-time constraints)
7) Robotics research – haptics: 
• robot is used as a haptic input device (e.g., for virtual reality) or slave for telepresence systems; high sensitivity for force control (< 10 N)
• control of robot systems at the lowest level possible (real-time constraints)

It is typically assumed in the robotics literature that there is direct control of the forces or torques at robot joints, and the robot's dynamics transforms those controls into joint accelerations. In some cases, however, we can assume that there is direct control of the joint velocities, for example when the actuators are stepper motors.  Also, robot-control engineers are usually supposed not to rely on the velocity-control modes of off-the-shelf amplifier for electric motors, because these velocity-control algorithms do not make use of a dynamic model of the robot. This allows the robot-control engineer to use a dynamic model of the robot in the design of the control law. It is important however that users educate themselves about the features of the system they have at hand so that they do not re-invent the wheel. One example of a very capable robot is the FrankaEmika robot which by using the open-source C++ interface, you can send real-time control values at 1 kHz with 5 different interfaces:
Gravity & friction compensated joint level torque commands.
Joint position or velocity commands.
Cartesian pose or velocity commands.

The research/automation groups that are concerned with use cases 5-7 are the ones who want to control the robot at the lowest level possible. It is interesting to see that some users intend to improve or research algorithms that are already quite mature and integrated into the robot controllers, such as standard motion control algorithms or more advanced ones, such as vibration damping. Nevertheless, traditional industrial robots which are good sources of velocities due to their high gear ratios. They are no able to read the forces of the environment and are only able to be controlled by joint positions. Since the robotics market is still dominated by traditional robots, it is important to consider use case implementation for traditional ones.

One of the fundamental requirements for the success of a contact-rich task (use case 5-7) is the capacity to handle the interaction between manipulator and environment. The quantity that describes the state of interaction more effectively is the contact force at the manipulator’s end-effector. As mentioned before, most common industrial robots are joint-position-controlled. For this type of robot, compliance control is necessary to safely attempt contact-rich tasks, or the robot is prone to causing large unsafe assembly forces even with tiny pose (position and orientation) errors.

# Orientation Error