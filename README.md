# Masters Project: Autonomous 6-DoF Robotic Arm Control on a Space Rover
A self-contained framework combining analytical inverse kinematics and ArUco-marker vision to drive a 6-DOF robotic arm on a mobile rover.


**Inverse Kinematics + Vision-Based Feedback**

---

## Project Overview

This repository implements a **vision-guided robotic control pipeline** for a 6-degree-of-freedom (6-DoF) robotic arm mounted on a rover. It integrates:

* **Analytical inverse kinematics solver** (closed-form DH + geometric methods)
* **Vision subsystem** using OpenCV ArUco markers for 6-DoF pose feedback
* **Real-time GUI** (Matplotlib + PyQt5) for visualization and testing

Together, these modules enable the robotic arm to detect targets, estimate pose, compute joint angles, and actuate in real-time with high precision.

---

## Motivation & Objectives

### Why this matters

*  **Space robotics**: Autonomous arms are essential for lunar/planetary rovers where human input is limited.
*  **Industrial automation**: Vision-guided arms adapt to unstructured environments without manual reprogramming.

### Project Objectives

1. Build a closed-form IK model for a custom 6-DoF robotic arm.
2. Calibrate a camera for distortion-free, accurate 3D perception.
3. Implement ArUco-based detection and pose estimation with `cv2.solvePnP`.
4. Develop a real-time visualization and feedback loop.

---

## System Architecture

```text
   +------------------------+              
   |   Camera (Mono/Stereo) |              
   +-----------┬------------+              
               │ video frames             
               ▼                          
   +------------------------+     joint angles  
   |   ArUco Detection &    | ─────────────▶   
   |  Pose Estimation (PnP) |                    
   +-----------┬------------+                    
               │ 6-DoF pose                        
               ▼                               
   +------------------------+                    
   |  Inverse Kinematics    |                    
   |  (DH + Geometric)      |                    
   +-----------┬------------+                    
               │ motor commands                   
               ▼                               
   +------------------------+                    
   |    6-DoF Robotic Arm   |                    
   +------------------------+                    
```

---

## Technical Details

### 4.1 Kinematic Model & Inverse Kinematics

* Modeled using **Denavit–Hartenberg (DH) parameters**.
* **Closed-form IK** computes joint angles from end-effector targets.
* Ensures **fast computation (<1 ms)** for real-time use.


---

### 4.2 Camera Calibration

* Performed with a **9×6 checkerboard pattern**.
* Corrects **radial and tangential distortions**.
* Achieved **mean reprojection error: 0.06 px**.


---

### 4.3 ArUco Marker Detection

* Dictionary: **DICT\_5X5\_1000**
* Detection works reliably at ±60° tilt and low light (50 lux).


### 4.4 Pose Estimation (solvePnP)

* Uses `cv2.solvePnP` with **IPPE\_SQUARE** algorithm.
* Achieves **±2 mm translation accuracy** and **±0.5° orientation accuracy**.


---

### 4.5 3D Visualization & GUI

* Real-time 3D plotting with **Matplotlib**.
* "U-shaped gripper" marker for camera orientation.

---

## Acknowledgements

* **A/Prof. Chi-Tsun (Ben) Cheng** – Supervisor
* **RMIT Rover Team 2024** – Technical support & testing
* **OpenCV & ROS2 communities** – Tools & libraries


