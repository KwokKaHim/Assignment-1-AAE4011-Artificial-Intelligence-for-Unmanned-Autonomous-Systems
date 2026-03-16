# AAE4011 Assignment 1 — Q3: ROS-Based Vehicle Detection from Rosbag
> **Student Name:** [Kwok Ka Him] | **Student ID:** [25017452D] | **Date:** [16-3-2026]
## 1. Overview
This project demonstrates a real-time vehicle detection system built on **ROS Noetic** and **Ubuntu 20.04**. It processes compressed image streams from a rosbag and visualizes the results through **Foxglove Studio**.

---

##  2. Detection Method

###  System Architecture
*   **Data Ingestion**: The node subscribes to the `/hikcamera/image_2/compressed` topic. Using compressed streams optimizes bandwidth and prevents buffer overflows.
*   **Deep Learning Inference**: Powered by **YOLOv8n (Nano)** for high-speed object detection.
*   **UI & Visualization**: **Foxglove Studio** is used as the primary interface for real-time playback, detection display, and performance statistics.
*   **Synchronization**: Annotated frames are re-compressed and published to the `/vehicle_detection/image/compressed` topic to ensure low-latency visual feedback.

###  Why YOLOv8n (Nano)?
*   **Efficiency**: It is a powerful and lightweight object detection tool designed for edge devices.
*   **Hardware Compatibility**: Ideal for standard laptops; it maintains a high FPS (Frames Per Second) even with limited GPU/CPU resources, ensuring the detection keeps up with the bag file stream.

## 3. Repository Structure
This package follows the standard ROS directory structure for evaluation:
```text
vehicle_detector/             # ROS Package Root
├── CMakeLists.txt            # Build configuration
├── package.xml               # Package metadata and dependencies
├── scripts/                  # Python executable scripts
│   ├── detect.py             # Main detection node
│   └── extract_images.py     # Image extraction tool
├── launch/                   # Launch files
│   └── detect.launch         # One-click start configuration
└── README.md                 # Project documentation
```

---
## 4. Prerequisites
* OS: Ubuntu 20.04 (LTS)
* ROS Version: ROS Noetic
* Python: 3.8+
---
##  5. How to Run

1.  **Environment**: **ROS 1 (Noetic)** installed on **Ubuntu 20.04** with **Python 3**.
2.  **Workspace**: Create and initialize a catkin workspace:
    ```bash
    mkdir -p ~/catkin_ws/src && cd ~/catkin_ws/src
    catkin_init_workspace
    ```
3.  **Package Setup**: Create your package and add a `scripts` folder:
    ```bash
    catkin_create_pkg vehicle_detector rospy sensor_msgs std_msgs cv_bridge
    mkdir scripts && cd scripts
    ```
4.  **Scripts**: Save your `extract_images.py` and `detect.py` into the `scripts` folder and make them executable:
    ```bash
    chmod +x *.py
    ```
5.  **Execution**: Open **4 terminals** and run the following in order:

    *   **Terminal 1**: Start ROS Master
        ```bash
        roscore
        ```
    *   **Terminal 2**: Start Foxglove Bridge (Adjust buffer for high-res images)
        ```bash
        roslaunch foxglove_bridge foxglove_bridge.launch send_buffer_limit:=100000000
        ```
    *   **Terminal 3**: Start the Detection Node
        ```bash
        python3 detect.py
        ```
    *   **Terminal 4**: Play the Rosbag
        ```bash
        rosbag play /mnt/c/Users/LENOVO/Downloads/ass.bag
        ```

---
## Sample Results
### Image extraction summary
- total frame: 1116
- resolution: 1440x1080
- topic name: /vehicle_detection/image/compressed
###  Detection results (sample screenshot, detection statistics)
  



##  Video Demonstration
https://youtu.be/Xb_POjtcT4s


---

##  Reflection & Critical Analysis
### What did you learn?
After finishing this assignment, I learned how to make commands in the ROS environment. For example, I know how to write the python code in the ROS environment. I need to create a ROS Package. Next, I need to add a scripts folder. Then, create a Python file in scripts with a decided name. Finally, use the ‘nano scripts/detect.py’ command and enter a coding environment. Moreover, I know what is the different between catkin make or colcon build. Catkin make is for ROS 1. colon build is for ROS 2. Also, I learned how to connect the ROS environment to Foxglove. 
### How did you use AI tools?
I use Copilot to help finish this project. I use it to guide me step by step. For example, Copilot provides commands for me to use in ROS environment. Sometimes, there will some errors such as my laptop having no installation of some software. And Copilot will give the new command to fix it. I just repeat the above step until the ROS environment has no errors anymore. The benefit is that AI can immediately identify the problem and save time. Furthermore, I use AI to generate the python code. It helps me a lot since I have no experience in coding using python. I think the limitation is that I need to provide a very detailed prompt for AI, otherwise it will provide the wrong answer again. 
### How to improve accuracy?
Improve the resolution of the videos since YOLO is highly relying on the captured videos or images from the camera, so it is important to improve the quality of the videos and images. Also, Integration of Temporal Tracking can help to Reduces Flickering Detections. It uses algorithms like Kalman Filters to predict where a vehicle should be in the next frame. 
### Real-world challenges
The YOLO is too powerful for drone that it needs the better hardware to run, but it will cause a higher power consumption. It means we need to increase the amount of battery. Also, for real time situations, python-based systems may be slower than C++.
