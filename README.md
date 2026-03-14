# ROS-Based Vehicle Detection from Rosbag
## Method description
### Architecture
Data collection: The node subscribes to the /hikcamera/image_2/compressed topic. I use Foxglove as a UI for playback and detection display with statistics.

Deep Learning Inference: YOLOv8n (Nano)

Synchronization & Visualization: The final annotated frame is re-compressed and published to the /vehicle_detection/image/compressed topic in Foxglove
### The reason why using YOLOv8n (Nano)
Is is a powerful object detection tool

Good for laptop: low requirement of hardware
### How to run
1. Make sure download the ROS and Python 3
2. Create a catkin workspace
3. Go into src and create the package
4. Add a scripts folder for Python nodes
5. Write a Python code of extract_images.py
6. Write a Python code of detect.py
7. Open 4 terminal
8. In the first terminal, Start ROS Master by using 'roscore'
9. In the second terminal, Start Foxglove Bridge by using 'roslaunch foxglove_bridge foxglove_bridge.launch send_buffer_limit:=100000000'
10. In the third terminal, Start the Detection Node by using 'python3 detect.py'
11. In the forth terminal, Play the Rosbag by using 'rosbag play "/path/to/your/.bag"' (The path format is Linux) 


