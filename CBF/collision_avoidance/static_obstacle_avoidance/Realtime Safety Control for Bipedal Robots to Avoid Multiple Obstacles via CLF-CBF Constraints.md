# Realtime Safety Control for Bipedal Robots to Avoid Multiple Obstacles via CLF-CBF Constraints

## Key Points

**safety filter:**

- safety monitor: handmake->saturate->combine multiple to one: product of smoothly saturated valid CBFs
![20231130151122](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231130151122.png)
![20231130151841](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231130151841.png)
![20231130151911](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231130151911.png)

- intervention scheme: QP
![20231130151227](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231130151227.png)
![20231130151254](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231130151254.png)
![20231130151320](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231130151320.png)
![20231130151352](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231130151352.png)
- task policy
- fallback policy

**开展的工作：**
给定确定的双足机器人状态空间表达式，针对一个目标位置和一个障碍物的情况根据经验构造一个确定的CLF和CBF公式,构造CBF-CLF-QP；对该系统、单障碍物情况下的CLF-CBF-QP出现平衡点的情况进行分析（平衡点的数量、位置），对停止到障碍物轮廓的平衡点给出了一个解决方法;考虑多障碍物的情况，将针对单个障碍物构造的CBF先饱和处理之后利用乘法合成一个CBF；双足机器人在到达最终目标点时会经过许多中途设立的目标点，不同目标点切换时控制信号会不连续，采用平滑参考控制信号的方法使控制信号的运动轨迹连续。

**future work:**
无

**对象：**
Bipedal Robot

**仿真工具：**
MATLAB单障碍物仿真，ROS1(C++)多障碍物仿真

**使用或开源的数据集：**
无

**是否开源：**
是，网址：<https://github.com/UMich-BipedLab/multi_object_avoidance_via_clf_cbf>

**摘要：**
we propose a means to design and compose control barrier functions (CBFs) for multiple non-overlapping obstacles and evaluate the system on a 20-degree-of-freedom (DoF) bipedal robot.

**Key Words：**
Motion Planning, Autonomous Navigation, Obstacle Avoidance, Control Barrier Function, Control Lyapunov Function

## 1. Introduction and Contributions

1. 提出了避障领域存在的技术难题：
   This raises a concern when obstacles either move into the planned path but the map has not been updated or a robot's new pose allows the detection of previously unseen obstacles. The slow update rate of the map leads to either collision or abrupt maneuvers to avoid collisions.
2. 综述避障方法：
   1) 经典方法：
        probabilistic roadmap approaches (PRM) and cell decomposition
      存在的问题：
        the omission of robot dynamics and the extra computation for map discretization make these methods hard to use in real-time applications
   2) Artificial potential fields
      优点：
        stand out for their simplicity, extendability, and efficiency, leading to their wide adoption for real-time obstacle avoidance planning problems
      存在的问题：
        A drawback of potential field methods is that they require the entire map of an environment to be available when designing a potential function that will render attractive one or more goal points in the map. Moreover, unwanted local minima and oscillations in the potential field have limited their deployment in the field.
   3) CBF
      优点：
        enables realtime controller synthesis with provable safety for mobile robots operating in a continuous (non-discretized) space and can work with a partial (or incomplete) map.
3. 提出CBF-CLF-QP平衡点的问题：
   Specifically, the inequality constraints (of the QP) associated with the derivatives of the control Lyapunov and control barrier functions can induce equilibria in the closed-loop system that are distinct from the equilibrium of the CLF. Reference [19] characterizes these equilibria via the KKT conditions associated with the QP, while reference [20] emphasizes that if an induced equilibrium is unstable, then "natural noise" in the environment will avoid the robot being deadlocked at an unstable equilibrium.
4. new proposed CLF-CBF system的贡献
5. 提到了CLF-CBF-QP虚假平衡点的概念：
   spurious equilibrium points induced by the CLF-CBF constraints on the QP.

## 2. Related Work on Control with Safety

### 2.1 Artificial Potential Fields and Navigation Functions

1. Artificial Potential Fields方法的缺点：
   It has been recognized that superimposed attracting and repelling fields can create undesired spurious equilibria, which prevent a robot from reaching its goal state [30]. In addition, potential fields have been observed to introduce trajectory oscillations as a robot passes near obstacles.
2. Navigation Functions方法的缺点：
   Because the design of a navigation function takes into account the global topology of the method of navigation functions is not appropriate for problems requiring the online identification and avoidance of obstacles; in addition, there are topological restrictions to the existence of navigation functions.

### 2.2 Control Barrier Functions and Control Lyapunov Functions

1. CBF和artificial potential functions的关系：
   The recent paper [44] shows that CBFs are a strict generalization of artificial potential functions and that in a practical example, a CLF-CBF-QP has reduced issues with oscillations as a robot passes near obstacles and improved liveness, meaning the ability to reach the goal state.

### 2.3 Combining Multiple CBFs

1. Reference [47] combines multiple CBFs for disjoint unsafe sets with a single CLF to produce a new CLF that simultaneously provides asymptotic stability and obstacle avoidance.

### 2.4 CLF-CBF-QPs and Unwanted Equilibrium Points

### 2.5 Summary

1. The presence of multiple obstacles is common in practice. While existing works can treat disjoint obstacles, they are not appropriate for use where obstacles are identified in real-time via an onboard perception system.

## 3. Construction of Control Lyapunov Function and Control Barrier Function

### 3.1 State Representation

### 3.2 Design of CLF and CBF for Bipedal Robots

### 3.3 Proof of CBF Validity

### 3.4 Quadratic Program of the Proposed CLF-CBF System

### 3.5 Analysis for Unwanted Equilibria

1. Paper [19] points out very clearly that the CLF-CBF-QP formulation of Sec. 3.4 can introduce unwanted equilibria that may prevent the robot from reaching a goal state. The paper [20] also considered this problem and noted that if the equilibria are unstable, then liveness is preserved for almost all initial conditions.

## 4. Combining CBFs for Multiple Obstacles

1. A key innovation with respect to [46] is that we will compose the associated CBFs in a smooth (C1) manner. A potential drawback with respect to [46] is that we will assume the obstacles giving rise to the CBFs are a positive distance apart. Similar to [47], we saturate standard quadratic CBFs before seeking to combine them. Distinct from [47], we multiply the saturated CBFs instead of creating a weighted sum.

### 4.1 Smooth Saturation Function

1. 将CBF变成平滑的饱和CBF

### 4.2 Multiplication Property of Smooth Saturated CBFs

## 5. Smoothing Reference Control Variables

1. 当机器人运动过程中需要途径多个目标点时，控制变量会出现不连续，这一节提出平滑和连续控制信号的方法。
   We have created a continuous vector field for a single target position surrounded by multiple obstacles. However, discontinuities are introduced when we switch from one target to another. The jumps appear in two ways: when the attraction points used in the CLF are updated and when the associated reference control variable uref is updated.

## 6. Simulation Results with single and multiple obstacles

### 6.1 Robot Model in Simulation

### 6.2 Behavior Study with Single Obstacle in MATLAB

### 6.3 Liveness Analysis in MATLAB

### 6.4 Multi-Obstacle Simulation with ROS in C++

## 7. Experimental Results on a Bipedal Robot

### 7.1 Autonomy System Integration

### 7.2 Autonomy Experiment on Cassie Blue

## 8. Conclusion

## Appendix A

1. 对单障碍物CLF-CBF-QP平衡点数量的分析，讨论了whether each CLF or CBF constraint is active or inactive四种情况对应的平衡点数量。
