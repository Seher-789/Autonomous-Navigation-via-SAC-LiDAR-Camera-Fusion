# Autonomous Navigation using Soft Actor-Critic with LiDAR-Camera Fusion Data

This project implements a deep reinforcement learning (DRL) pipeline for **autonomous robot navigation** in simulation, using **LiDAR-Camera sensor fusion** as the primary perception method. It utilizes the **Soft Actor-Critic (SAC)** algorithm enhanced with vision and point cloud data for real-time decision-making.

---

## Key Features

- **LiDAR-Camera Fusion**: Combines VLP-16 3D LiDAR and RGB camera data for rich environment perception.
- **Soft Actor-Critic (SAC)**: A robust, off-policy DRL algorithm for continuous control in complex environments.
- **Goal-driven Navigation**: The agent learns to reach the goal while avoiding obstacles using fused sensory inputs.
- **Sim-to-Real Transfer Potential**: Designed with modularity for future real-world deployment.
- **Visualization Support**: Real-time plotting of reward and loss via Spyder or external tools.

---


---

## ⚙️ Setup Instructions

### 1. Create a Conda Environment
```bash
conda create -n gtrl python=3.7
conda activate gtrl
```
## 2. Install Python Dependencies
```bash
pip install numpy tqdm natsort cpprb matplotlib einops squaternion opencv-python rospkg rosnumpy pyyaml
```
## 3. Install ROS Dependencies
```bash
sudo apt install python3-catkin-tools python3-osrf-pycommon
sudo apt-get install ros-noetic-cv-bridge
```
## 5. Clone the Repository
```bash
cd ~/your_workspace/
git clone https://github.com/Seher-789/Autonomous-Navigation-via-SAC-LiDAR-Camera-Fusion.git
```
## Build and Configure
## 6. Compile the Catkin Workspace
```bash
cd Autonomous-Navigation-via-SAC-LiDAR-Camera-Fusion/DRL-Transformer-SimtoReal-Navigation/catkin_ws
catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python3
```
## 7. Set Environment Variables
```bash
export GAZEBO_RESOURCE_PATH=~/Autonomous-Navigation-via-SAC-LiDAR-Camera-Fusion/DRL-Transformer-SimtoReal-Navigation/catkin_ws/src/gtrl/launch
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/ros/noetic/lib
```
(Optional) Add to ~/.bashrc to persist:
```bash
echo 'export GAZEBO_RESOURCE_PATH=~/.../gtrl/launch' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/ros/noetic/lib' >> ~/.bashrc
source ~/.bashrc
```
## 8. Source the Workspace
```bash
source devel/setup.bash
```
## 9. Copy Gazebo Models
```bash
cp -a ~/.../gtrl/models/. ~/.gazebo/models
```
## Modify Code Paths
Edit main.py
```bash
sys.path.append('/home/your_workspace/.../gtrl/scripts')
```
## Edit env_lab.py (line ~129)
```bash
fullpath = os.path.join('/home/your_workspace/.../drl_navigation/launch', launchfile)
```
## Run the Training
```bash
cd .../gtrl/scripts/SAC
python main.py
or
python3 main.py
```
## Launch LiDAR-Camera Fusion Node
```bash
roslaunch lidar_camera_fusion vlp16OnImg.launch 
```
## Kill ROS and Gazebo Processes
```bash
killall -9 rosout roslaunch rosmaster gzserver nodelet robot_state_publisher gzclient python python3
```
(Optional) Add an alias:
```bash
echo "alias k9='killall -9 rosout roslaunch rosmaster gzserver nodelet robot_state_publisher gzclient python python3'" >> ~/.bashrc
source ~/.bashrc
```
##Training Output
**Reward Graphs**
**Collision and Success Rate Logs**
<img width="2560" height="1600" alt="Screenshot from 2025-07-15 20-10-50" src="https://github.com/user-attachments/assets/eb8657dc-a73d-47b2-95de-b26accfe6456" />
<img width="1654" height="929" alt="Screenshot from 2025-07-15 20-10-45" src="https://github.com/user-attachments/assets/98fda9ef-a29b-401a-b4f3-47d3ef629a3e" />

