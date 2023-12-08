# Dynamic Control Barrier Function-based Model Predictive Control to Safety-Critical Obstacle-Avoidance of Mobile Robot

## Key Points

**safety filter:**

- safety monitor: handmake(论文中没有提到多个CBF的组合方式，需要看代码，CBF里的参数是动态的)
![20231205104016](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231205104016.png)

- intervention scheme和task policy合二为一了: MPC framework
![20231205104152](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231205104152.png)

- fallback policy

**开展的工作：**
This paper proposes a safety-critical method for static and dynamic obstacles avoidance based on LiDAR sensor. Firstly, we adopt a robust local perception module, which perceives and parameterizes obstacles to MBEs, and predicts obstacles trajectory considering uncertainty based on Kalman filter. Then, we combine Dynamic Control Barrier Function and Model Predictive Control framework to generate a safe collision-free trajectory for robot navigation in dynamic environment.

![20231205103833](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231205103833.png)

亮点：

1. 应用于动态障碍物避障；
2. 在状态向量的选择上，不光考虑了机器人的状态，还考虑了障碍物的状态，用这样考虑因素更全面的状态向量构造CBF->从而实现了动态避障。

**future work:**
无

**对象：**
小车

**仿真工具：**
ROS1 Melodic Gazebo 动态障碍物仿真
![20231205102334](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231205102334.png)

**使用或开源的数据集：**
无

**是否开源：**
是，网址：<https://github.com/jianzhuozhuTHU/MPC-D-CBF>

**摘要：**
This paper presents an efficient and safe method to avoid static and dynamic obstacles based on LiDAR. First, point cloud is used to generate a real-time local grid map for obstacle detection. Then, obstacles are clustered by DBSCAN algorithm and enclosed with minimum bounding ellipses (MBEs). In addition, data association is conducted to match each MBE with the obstacle in the current frame. Considering MBE as an observation, Kalman filter (KF) is used to estimate and predict the motion state of the obstacle. We extend the traditional Control Barrier Function (CBF) and propose Dynamic Control Barrier Function (D-CBF). We combine D-CBF with Model Predictive Control (MPC) to implement safety-critical **dynamic obstacle avoidance**.

## 1. Introduction and Contributions

1. this paper presents an onboard lidar-based approach for safe navigation of vehicles in a dynamic environment.
2. For motion planning in a dynamic environment, we propose D-CBFbased MPC to obtain a safe collision-free trajectory.
3. 与之前看的一篇文章呼应：Zeng et al. [22] proposed a model predictive control design and [23] analysed its feasibility and safety, where discrete-time CBF constraints are used in a receding horizon fashion to ensure safety. However, this algorithm doesn't perform well in dynamic environment. Our approach extends CBF to achieve dynamic obstacle avoidance.
4. 这篇文章主要针对动态障碍物避障。
5. 这篇文章的主要贡献：
   - Dynamic Control Barrier Function-based Model Predictive Control framework is proposed to generate a safe collision-free trajectory in a dynamic environment.
   - We propose a method for detection and prediction of obstacles based on minimum bounding ellipse and Kalman filter, in which uncertainty is considered to enhance safety.
   - Experiments in gazebo and real scenarios are carried out to verify the real-time performance, effectiveness and stability of the safe-critical obstacles avoidance algorithm.

## OVERVIEW OF THE FRAMEWORK

1. 论文方法的框架

## IMPLEMENTATION

### A. Local Planning

#### 1. Dynamic Control Barrier Function

1. D-CBF在状态向量的选择上，不光考虑了机器人的状态，还考虑了障碍物的状态
![20231204221905](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231204221905.png)
    用这样考虑因素更全面的状态向量构造CBF
![20231204222138](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231204222138.png)
    然后套进去CBF的公式
![20231204222204](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231204222204.png)
    从而得到比只考虑机器人状态的CBF约束式更严格的输入
![20231204222402](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231204222402.png)
2. 采用离散时间CBF

#### 2. Model Predictive Control

1. 使用《Safety-Critical Model Predictive Control with Discrete-Time Control Barrier Function》这篇论文中描述的常用MPC-CBF框架
![20231204223156](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231204223156.png)

### B. Local Perception

1. The local perception maintains and estimates the safety space and obstacle regions and predicts trajectory of obstacle while considering the uncertainty of observation.

#### 1. Local map

#### 2. Obstacle parameterization

1. Considering obstacle avoidance in navigation tasks, it is meaningful to consider the minimum bounding volume of the obstacle.
2. If the robot finds a feasible motion in the environment after the obstacle simplification, then this motion must also be feasible in the original space [30]. Therefore, the obstacles are clustered and enclosed with minimal bounding ellipses (MBE) in this module.
3. 点云聚类+minimum bounding ellipse algorithm

#### 3. Uncertainty analysis

1. 障碍物的位置不确定性和形状不确定性->为后面卡尔曼滤波做准备

#### 4. Trajectory prediction

1. 用卡尔曼滤波进行轨迹预测，预测步数与MPC窗口数可能一致（猜测的，后面有需要再看原文或代码）。

## 4. EXPERIMENTS

### 1. Real-world scenarios

### 2. Simulation scenario

## 5. CONCLUSIONS
