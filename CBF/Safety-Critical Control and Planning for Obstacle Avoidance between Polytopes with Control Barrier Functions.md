# Safety-Critical Control and Planning for Obstacle Avoidance between Polytopes with Control Barrier Functions

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

1. NMPC-CBF
2. 考虑多边形智能体通过多边形障碍物的情况。

- We formulate the dual form of the obstacle avoidance constraint between polytopes as DCBF constraints for safety. These proposed DCBF constraints are incorporated into an NMPC formulation which enables fast online computation for control and planning for general nonlinear dynamical systems.
- The proposed NMPC-DCBF formulation for polytopes is validated numerically. Different convex and nonconvex shaped robots are shown to be able to navigate with tight maneuvers through maze environments with polytopic obstacles using fast real-time control and trajectory generation.

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

1. 现有方法的问题：In either case, the solution can only be applied as an offline planning algorithm.
2. 本文方法的优势：The proposed optimization formulation has lower computational complexity compared to existing work and can be used as a fast online algorithm for control and planning for general nonlinear dynamical systems.

**Key Words：**
Motion Planning, Autonomous Navigation, Obstacle Avoidance, Control Barrier Function, Control Lyapunov Function

## 1. Introduction

1. When a tight-fitting obstacle avoidance motion is expected, the robot and the obstacles need to be considered as polyhedral.
2. In this paper, we propose an optimization formulation to consider obstacle avoidance between polytopes using discrete-time control barrier function (DCBF) constraints with dual variables.

### A. Related Work

1. 现有的针对collision avoidance between two polytopes场景的方法存在的缺陷：
   - cannot be deployed as a real-time controller or trajectory planner for general nonlinear systems
   - However, obstacle avoidance behavior with this method can only be achieved with a relatively long horizon and needs to be solved offline for nonlinear systems.
2. 使用DCBF约束代替与障碍物距离的约束(distance constraints)在减少MPC的horizon方面的优势
Recently, it has been shown that considering discrete-time control barrier function (DCBF) constraints instead of distance constraints can handle this challenge, where the DCBF constraints can regulate the obstacle avoidance behavior with a smaller horizon and prevent local deadlock in trajectory generation.
3. 现有研究对场景过于简化
   In the work mentioned above, the robots and the obstacles are only considered as points or hyper-spheres, while obstacle avoidance constraint between polytopes is still an unsolved problem in all previous work by using discrete-time control barrier functions.

### B. Contributions

- We formulate the dual form of the obstacle avoidance constraint between polytopes as DCBF constraints for safety. These proposed DCBF constraints are incorporated into an NMPC formulation which enables fast online computation for control and planning for general nonlinear dynamical systems.
- The proposed NMPC-DCBF formulation for polytopes is validated numerically. Different convex and nonconvex shaped robots are shown to be able to navigate with tight maneuvers through maze environments with polytopic obstacles using fast real-time control and trajectory generation.

## 2. BACKGROUND

### A. Optimization Formulation using DCBFs

1. DCBF在可行性与安全性方面的改良
   改良原因：If γ(x) is close to 1, the system converges to ∂S slowly but can easily become infeasible. On the other hand, if γ(x) is close to 0, the constraint (3) is feasible in a larger domain but can approach ∂S quickly and become unsafe.
   改良方法：加一个松弛函数
   ![20231226221312](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231226221312.png)
2. MPC结合CBF的方法还能够克服单步CBF控制带来的deadlock问题
   When one-step control input is optimized [34], it could lead to a deadlock situation such that the robot is safe but unable to track the reference command. A nonlinear model predictive control formulation [17] can overcome these problems.
3. NMPC-CBF公式
![20231229094544](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231229094544.png)
   N and NCBF ≤ Ndenote the prediction and safety horizons respectively, which allows us to control the optimization computation complexity.

### B. Obstacle Avoidance between Polytopic Sets

1. 对obstacle和agent形状的假设
   In this work, we assume that there are NO static obstacles together with a single controlled robot. We further assume that the geometry of all the obstacles and the robot can be over-approximated with a union of convex polytopes, which is defined as a bounded polyhedron.
2. 
