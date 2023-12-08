# Safety-Critical Model Predictive Control with Discrete-Time Control Barrier Function

## Key Points

**safety filter:**

- safety monitor: handmake(consider just one)
![20231202182219](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231202182219.png)
![20231202182250](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231202182250.png)

- intervention scheme和task policy合二为一了: MPC framework
![20231202182333](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231202182333.png)

- fallback policy

**开展的工作：**
A safety-critical model predictive control design is proposed in this paper, where discrete-time control barrier function constraints are used in a receding horizon fashion to ensure safety. We present an analysis of its stability and feasibility, and describe its relation with MPC-DC and DCLF-DCBF. To verify our analysis, we use a 2D double integrator for obstacle avoidance, where we can see that MPC-CBF outperforms both MPC-DC and DCLF-DCBF. The proposed control logic is also applied to a more complex scenario: competitive car racing, where our ego car can race and safely overtake other racing cars.

缝合但是推断和分析的很好，分析并比较了这三种安全控制策略

1. MPC-DC
![20231202191952](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231202191952.png)
2. DCLF-DCBF
![20231202192039](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231202192039.png)
3. MPC-CBF
![20231202192129](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231202192129.png)

这篇文章揭示了在一些CBF避障的论文中，为什么智能体都是直挺挺的朝着前方障碍物走去，基本撞上前方障碍物，然后绕着障碍物走，即CBF起作用时刻的问题，并通过MPC这种多预测几个时间步的方法实现CBF的提前作用。
![20231202160014](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231202160014.png)

在避障中，CBF的作用就是让智能体转向避障。

**future work:**

1. tradeoff between safety and feasibility in terms of the choice of γ. However, it still remains an open challenge for how to automatically choose the γ.
   Given xt, X , U, we could pick a value of γto find a tradeoff between safety and feasibility. However, when the system evolves, this γ might no longer satisfy our safety demand or guarantee the optimization feasibility. Therefore, for a given fixed γ, we generally only have pointwise feasibility and a persistently feasible formulation is still an open problem and is part of future work.
   随着系统状态的变化，如果固定γ为一个不变量，可能这一个时间点γ可行了，下一个时间点γ不可行了，所以可自适应的γ是未来的一个研究方向。

**对象：**
两个：1）2D一个点绕大球
![20231202182943](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231202182943.png)
   2）多车在跑道上追逐
![20231202183033](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231202183033.png)

**仿真工具：**
MATLAB

**使用或开源的数据集：**
无

**是否开源：**
是，网址：<https://github.com/HybridRobotics/MPC-CBF>

**摘要：**
In order to obtain safe optimal performance in the context of set invariance, we present a safety-critical model predictive control strategy utilizing discrete-time control barrier functions (CBFs), which guarantees system safety and accomplishes optimal performance via model predictive control.

**Key Words：**
无

## 1. INTRODUCTION

### A. Motivation

1. 现有研究方法(CLF-CBF)存在的缺点（暂时认为与nominal controller没有预测功能有关）：
   Some recent work formulates this problem using control barrier functions, but only using current state information without prediction, see [1], [2], which yields a greedy control policy. Model predictive control can give a less greedy policy, as it takes future state information into account.
2. 现有研究(MPC-DC)的问题：与障碍物距离太近要出现碰撞时CBF才会发挥作用进行避障
   This distance constraint will not confine the optimization until the reachable set along the horizon intersects with the obstacles. In other words, the robot will not take actions to avoid the obstacles until it is close to them.
3. 本文针对2.中的问题采取的解决方法：
   We address this challenge above by directly unifying model predictive control with discrete-time control barrier functions together into one optimization problem.
4. 解决方法的效果（暂时认为是MPC方法预测功能解决了2.中的问题）：
   In this formulation, the CBF constraints could enforce the system to avoid obstacles even when the reachable set along the horizon is far away from the obstacles.

### B. Related Work

1. 除了连续时间系统，CBF也被推广到了离散时间系统：
   Besides the continuous-time domain, the formulation of CBFs was generalized into discrete-time systems (DCLF-DCBF) in [2].

2. MPC-DC方法存在的缺陷：
   However, these obstacle avoidance constraints under Euclidean norms will not confine the robot's movement unless the robot is relatively close to the obstacles. To make the robot take actions to avoid obstacles even far away from it, we usually need a larger horizon which increases the computational time in the optimization.

3. MPC-CBF相比于CLF-CBF方法的优势：
   Inspired by the previous work of model predictive control and control barrier functions, DCLF-DCBF can be improved by **taking future state prediction into account**, yielding a better control policy.

### C. Contribution

We analyze the stability of our control design, and qualitatively discuss the feasibility in terms of set intersections between reachable sets of MPC and safe sets enforced by CBF constraints along the horizon.

## 2. BACKGROUND

### A. Model Predictive Contro

1. 介绍了open-loop trajectory和closed-loop trajectory的概念。

### Control Barrier Functions

1. 介绍了discrete-time control barrier functions的概念
![20231201222141](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231201222141.png)
2. 介绍了discrete-time control Lyapunov function的概念
![20231201222824](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231201222824.png)
![20231201222844](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231201222844.png)

## 3. CONTROL DESIGN

### A. Formulation

1. 提出了本文的控制算法：MPC-CBF.

### B. Stability

### C. Feasibility

1. 求解的可行性：根据每一时间步输入和状态定义域得到的reachable set和CBF公式得到的subset间是否有交集来判断能否求出解。
2. When γ becomes relatively small, the MPCCBF controller makes a smaller subset of the safe set C in (4) invariant, and thus is more safer, but this might also make the optimization infeasible. A larger γ will make the optimization more likely to be feasible, but the CBF constraints might not be active during the optimization. We expect thatγ is chosen appropriately, such that the intersection between these two sets will not be empty and becomes a proper subset of Rk. This leads to a tradeoff between safety and feasibility in terms of the choice of γ. However, it still remains an open challenge for how to automatically choose the γ.

### D. Relation with DCLF-DCBF

1. The stage cost q(xk, uk) minimizes the system input, similar as uT k H(x)uk in (9a). The terminal cost minimizes the control Lyapunov function p(f (xk, uk)) in (14a), instead of using CLF constraints as (9b).
2. To sum up, our MPC-CBF formulation operates in a similar manner of DCLFDCBF with prediction N = 1.

### E. Relation with MPC-DC

1. Moreover, the feasible set at each horizon step k in MPC-DC formulation becomes Rk ∩ C. While, as we have seen previously, the feasible set in MPC-CBF formulation at each horizon step k is Rk ∩ Scbf,k. Note that Scbf,k is a subset of C. Therefore, the MPC-CBF formulation in (10) has a smaller safe set than MPC-DC. 所以MPC-CBF相比于MPC-DC在相对于障碍物比较远时就会进行避障。运行过程中并不是CBF得到的安全集越大越好，有时候根据性能要求小一点，这样如在避障场景下，机器人就不会离得障碍物太近才会采取避障而是早采取行动。Our MPC-CBF formulation is safer than MPC-DC in the context of smaller set invariance.

## 4. EXAMPLES

### A. 2D Double Integrator for Obstacle Avoidance

1. 对仿真结果的分析很全面透彻，值得效仿，同时验证了第3章中的猜测（可以和第3章呼应着看）。

### B. Competitive Car Racing

1. 障碍物（其他车）是动态的：
   In some previous car racing control work [24], [25], they only consider static obstacles on the track while we deal with dynamic obstacles such as other cars using MPC-CBF.
   假设自车位置和其他车的位置每时每刻都是可知的，这样瞬时静态的计算CBF来完成动态避障的过程。

## 5. CONCLUTION

## APPENDIX

### A. Car Racing Implementation

介绍如何推导及处理得到系统的状态空间表达式。
