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

flowchart:

```mermaid
flowchart TD

A[Start generate_launch_description()] --> B[Define package names<br>asiza_docking, asiza_gazebo,<br>asiza_localization, asiza_navigation]

B --> C[Define file paths<br>gazebo launch, EKF, map, RVIZ, Nav2 params]

C --> D[FindPackageShare for all packages]

D --> E[Build default file paths using PathJoinSubstitution]

E --> F[Define LaunchConfiguration variables<br>(autostart, slam, namespace, map, use_sim_time, etc.)]

F --> G[Declare Launch Arguments<br> - Configs<br> - Robot settings<br> - Position/orientation<br> - Flags]

G --> H[Create ld = LaunchDescription()]

H --> I[Add all declared launch arguments to ld]

I --> J[Include AprilTag Docking Launch]

J --> K[Start Assisted Teleoperation Node]

K --> L[Start cmd_vel_relay Node]

L --> M[Include EKF Launch]

M --> N[Include Gazebo Launch<br>spawn robot + RVIZ flags]

N --> O[Start nav_to_pose node]

O --> P[Include Nav2 bringup_launch.py]

P --> Q[Return LaunchDescription]

Q --> R[END]
```



