Asiza — ROS2 Mecanum Mobile Robot Platform

A fully modular and extensible **ROS2-based mobile robot** designed for indoor navigation, mapping, autonomous behaviors, and academic research.

Asiza integrates a custom mecanum drive system, multi-sensor perception, a clean URDF/Xacro description, and a full Nav2 navigation pipeline for both simulation and real-world deployment.

---

Overview

Asiza is a **high-performance mobile robot** built on a four-wheel mecanum drivetrain, equipped with modern perception sensors, and powered by ROS2.  
The system is designed to be:

- Easy to customize  
- Simple to extend with new sensors or behaviors  
- Suitable for real robot deployment and Gazebo simulation  
- Fully compatible with SLAM, localization, and autonomous navigation pipelines  

---

Key Features

  Mecanum Drive
  - Custom controller, adjustable wheels, accurate odometry.

  Robot Description
  - Modular URDF with accurate visuals and sensor mounts.
  
  Navigation
  - Nav2, SLAM, AMCL, and autonomous path planning.
    
  Sensors
  - LiDAR, RGB-D camera, IMU, easily expandable.
    
  Simulation
  - Gazebo-ready with realistic physics.
    
  Bringup
  - Unified launch files for simulation and hardware.
    
  Packages
  - Description, Bringup, Control, Navigation, Simulation.
  
  Extras
  - AprilTag docking, diagnostics, RViz setup.

---

Robot Images & tf Diagram:

<img width="1004" height="887" alt="image" src="https://github.com/user-attachments/assets/2b889178-e65e-4354-806f-81c5c3f8e8eb" />

---

<img width="1231" height="644" alt="image" src="https://github.com/user-attachments/assets/3e495f1b-30cb-4beb-b931-1d62506a71fb" />

---
Flowchart for mecanum controller :

flowchart TD

A["update() called"] --> B{"Controller ACTIVE?"}
B -- No --> C["halt wheels if not halted"] --> D["return OK"]
B -- Yes --> E["Get last cmd_vel message"]

E --> F{"cmd_vel nullptr?"}
F -- Yes --> G["Warn + return ERROR"]
F -- No --> H["Check age of cmd_vel"]

H --> I{"Timed out?"}
I -- Yes --> J["Set vx, vy, wz = 0"]
I -- No --> K["Use received command"]

J --> K

K --> L["Apply wheel multipliers and compute L, W"]

L --> M{"Open-loop mode?"}
M -- Yes --> N["odometry.updateOpenLoop()"]
M -- No --> O["Use wheel feedback to update odometry"]

O --> P["Compute yaw (Quaternion)"]
N --> P

P --> Q{"Should publish now?"}
Q -- Yes --> R["Publish odometry + tf if enabled"]
Q -- No --> S["Skip publishing"]

R --> S

S --> T["Apply speed limiters (x, y, z)"]

T --> U["Update previous_commands queue"]

U --> V{"publish_limited_velocity?"}
V -- Yes --> W["Publish limited velocity"]
V -- No --> X["Skip limited cmd publication"]

W --> X

X --> Y["Compute wheel velocities using IK"]
Y --> Z["Set wheel velocities on hardware interfaces"]

Z --> AA["return OK"]
