# Safety-Critical Control and Planning for Obstacle Avoidance between Polytopes with Control Barrier Functions

## Key Points

**safety filter:**

- safety monitor: handmake->duality-based optimization->directly use multiple CBFs
![20240102211057](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240102211057.png)
![20240102211145](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240102211145.png)

- intervention scheme: intervention scheme和task policy合二为一了: NMPC-DCBF framework
![20240102164712](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240102164712.png)
- task policy
- fallback policy

**开展的工作：**

1. NMPC-DCBF
2. 各种提升求解速度的方法（文章后半部分都是这个），主要通过将约束通过数学方法转变成计算效率高的形式、设置好的初始值以及调参
3. 仿真多边形智能体通过多边形障碍物的情况

- We formulate the dual form of the obstacle avoidance constraint between polytopes as DCBF constraints for safety. These proposed DCBF constraints are incorporated into an NMPC formulation which enables fast online computation for control and planning for general nonlinear dynamical systems.
- The proposed NMPC-DCBF formulation for polytopes is validated numerically. Different convex and nonconvex shaped robots are shown to be able to navigate with tight maneuvers through maze environments with polytopic obstacles using fast real-time control and trajectory generation.

**future work:**
无

**对象：**
多边形车辆（运动学模型）

**仿真工具：**
Python，非线性求解器CasADi+ipopt

**使用或开源的数据集：**
无

**是否开源：**
是，网址：<https://github.com/HybridRobotics/cbf>

**摘要：**

1. 现有方法的问题：In either case, the solution can only be applied as an offline planning algorithm.
2. 本文方法的优势：The proposed optimization formulation has lower computational complexity compared to existing work and can be used as a fast online algorithm for control and planning for general nonlinear dynamical systems.

**Key Words：**
无

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
2. 该场景下的safe set
   To ensure safe motion of the robot, we enforce DCBF constraints (3) pairwise between each robot-obstacle pair. Then, the safe set corresponding to the pair (Oi, R) is defined as:
![20240102112759](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240102112759.png)
3. However, (3) requires computation of hi(f (x, u)) via (8), which can only be solved numerically. This results in an optimization formulation with non-differentiable implicit constraints, which results in a significant increase in computation time. In the following section we derive explicit differentiable constraints which guarantee that the DCBF constraint is satisfied without affecting the feasible set of safe inputs K(x) ∀ x ∈ X .

## 3. OPTIMIZATION WITH DUAL DCBF CONSTRAINTS

还是NMPC-DCBF的框架，但是因为根据几何构造的DCBF(8)带入约束(3)中是不可微的隐式约束，计算效率低，所以利用duality-based optimization将约束转变为可微的显式约束，能够在不影响可行输入集范围大小的前提下提升计算效率。

### A. Dual Optimization Problem

### B. Obstacle Avoidance with Dual Variables

1. In order to remove the implicit dependence of hi(x) on xvia (8), we enforce a constraint stronger than (3) which does not require explicit computation of hi(x) via (8). The dual formulation of (8), (10), can be used to achieve this.
2. This means that for any fixed x ∈ X , the input u satisfies the DCBF constraint (3) with the implicit definition of hiif and only if the tuple (u, λOi∗, λR∗) satisfies (13). So, the feasible set of inputs is not reduced at any x ∈ X .

### C. Optimization Formulation

1. 最终的NMPC-DCBF优化公式
![20240102164712](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240102164712.png)
2. This NMPC-DCBF formulation (20) corresponds to enforcing safety constraints only between the pair (Oi, R) of polytopes. To enforce DCBF constraints between every pair of robot and obstacle, we introduce corresponding dual and primal variables and enforce the constraints (20e)-(20h) for each pair.
3. The mathematical intuition behind (20) is different from the previous work in [31] that focuses on duality in the continuous domain. Moreover, the system dynamics is not required to be control affine in our proposed (20). Furthermore, differentiability of dual variables is required in [31] and not needed in this work.

### D. Complexity and Performance

1. 通过进一步改写DCBF约束来提升计算效率Exponential DCBF Constraint
2. 选择MPC和DCBF的窗口长度
   Our NMPCDCBF formulation does not require the obstacle avoidance horizon length NCBF be equal to N , which additionally reduces the complexity [33].
3. To sum up, DCBF constraints with dual variables enable fast optimization for obstacle avoidance between polytopes.

### 4. NUMERICAL RESULTS

1. 仿真主题：an autonomous navigation problem
2. 仿真任务：We model the controlled robot with different shapes, including triangle, rectangle, pentagon and L-shape. The proposed optimization-based planning algorithm allows us to successfully generate dynamically-feasible collisionfree trajectories even in tight maze environments.
3. 仿真环境(Environment)
4. 系统动力学模型(System Dynamics)：The controlled robot is described by the kinematic bicycle model, which is typical for testing trajectory planning algorithms in tight environments.
5. 全局规划方法(Global Planning)
6. 局部轨迹生成方法(Local Trajectory Generation)
7. 初始值设置(Warm Start)
8. 参数设置与仿真结果

## 5. CONCLUSION

1. We proposed a nonlinear optimization formulation using discrete-time control barrier function based constraints for polytopes. The proposed formulation has been shown to be applied as a fast optimization for control and planning for general nonlinear dynamical systems. We validated our approach on navigation problems with various robot shapes in maze environments with polytopic obstacles.
