# Enhancing Feasibility and Safety of Nonlinear Model Predictive Control with Discrete-Time Control Barrier Functions

## Key Points

**safety filter:**

- safety monitor: 论文主要讲理论，怎么合成CBF没有涉及

- intervention scheme和task policy合二为一了: MPC framework
有两个：
NMPC-DCBF:
![20240108205614](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240108205614.png)
NMPC-DCLF-DCBF:
![20240108214330](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240108214330.png)

- fallback policy

**开展的工作：**

本文创新的思想：
MPC-CBF因为要预测多步且受不可调参的CBF的约束，可能求解不可行（求解可行的标志就在于每一步的reachable set和safe region有没有交集），因而MPC-GCBF对此进行改进，在MPC中只在第1步有CBF约束，改善了feasibility的情况，但是因为CBF约束的参数不可调，第1步就有可能不可行，于是本文就在CBF约束上加一个可调的参数，参数的函数作为损失加在优化求解的目标函数中。同时为了克服MPC-GCBF求解只有one-step CBF约束可能不能充分约束系统的安全性导致在后面时间步的优化问题中不可解（多步CBF约束有解表示未来几个时间步是能有保证安全的解的，1步约束只能保证该步有解不管后面的时间步），于是增加了CBF约束的horizon.

可行性其实是CBF约束与输入/状态限制、系统动力学约束之间的矛盾（reachable set与safe region）。
![20240108224229](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240108224229.png)

The contributions of this paper are as follows:

- We propose two control frameworks for guaranteeing stability and safety using nonlinear MPC (NMPC), where the safety criteria are considered as discrete-time CBF constraints, and stability criteria appear as CLFs formulated either as a terminal cost or discrete-time constraints.
- The decay rates of the discrete-time control barrier function constraints are relaxed in the optimization problem, which allow the proposed formulations to enhance the feasibility and the safety at the same time for both onestep and multi-step input optimization.
- -The proposed formulations are shown theoretically to enhance the feasibility and safety performance compared with existing approaches, and also validated with numerical examples.

**future work:**

Our future work will focus on how to implement the proposed formulations either as a mid-level planner or a real-time controller on mobile robots, where modelling uncertainty, system disturbance and noise are required to be considered for real-time deployment. From the theoretical perspective, a formal discussion about recursive feasibility and stability will be carried out to summarize the technique of nonlinear MPC with control barrier function.

**对象：**
无

**仿真工具：**
MATLAB

**使用或开源的数据集：**
无

**是否开源：**
是，网址：<https://github.com/HybridRobotics/NMPC-DCLF-DCBF>

**摘要：**

1. 现有方法的不足：
   The limitations of these existing approaches are mainly about feasibility and safety. In the existing approaches, the feasibility of the optimization and the system safety cannot be enhanced at the same time theoretically.
2. 本文开展的工作和方法的优势：
   In this paper, we propose two formulations that unifies CLFs and CBFs under the framework of nonlinear model predictive control (NMPC). In the proposed formulations, safety criteria is commonly formulated as CBF constraints and stability performance is ensured with either a terminal cost function or CLF constraints. Slack variables with relaxing technique are introduced on the CBF constraints to resolve the tradeoff between feasibility and safety so that they can be enhanced at the same.

**Key Words：**
无

## 1. INTRODUCTION

### A. Motivation

### B. Related Work

1. 对可行性问题的描述：
    The feasibility issues arise due to the potential empty intersection between the reachable set and the safe region confined by CBF constraints at each time step.
2. 现有方法的问题及对问题的阐述：
   Moreover, with current approaches, there exists a tradeoff between safety performance and feasibility and they cannot be enhanced at the same time, as discussed in [4]. In other words, reducing the decay rate of CBF constraints increases the system safety, but comes at the possibility of infeasibility.
3. A potential way to partly handle the feasibility issue is to adopt the CBF constraint only on the first time step as a one-step constraint, as presented in the formulation MPC-GCBF in [18]. This approach is shown to enhance the feasibility, however, we are still under the restriction between choosing feasibility and safety, as the intersection between the reachable set and the safe region at the first step could still potentially be empty.
4. 对feasibility问题的介绍非常好：
   Similarly, feasibility is challenging to be guaranteed in the continuous domain. Many existing approaches relax the CLF constraint to resolve the conflict between CLF and CBF constraints, as summarized in [5]. However, the QPbased problem could become infeasible as the CBF constraint might violate the input constraint even when we relax the CLF constraint. In [2], a valid CBF is specifically designed for the adaptive cruise control scenario based on the system dynamics under input constraints, which could ensure the feasibility in the optimization. This approach solves the problem specifically for this system but not for general nonlinear systems. Recently in [20], the decay rates of CBF constraints are relaxed with optimization variables, which generally resolves the conflict between the CBF constraint and the input constraint and guarantees point-wise feasibility.
5. 本文方法的特点：
   In this paper, the proposed formulations draw inspiration from the decay-rate relaxing technique for the CBF constraint in the continuous-time domain, and will be shown to be able to enhance the feasibility and the safety at the same time. The proposed formulations are generalized for both one-step or multi-step constraints, and don't specifically require only an one-step constraint to increase the feasibility as done with MPC-GCBF [18].
6. 提出一项技术：decay-rate relaxing technique for CBF constraint

### C. Contributions

### D. Paper Structure

## 2. BACKGROUND

### A. CLFs and CBFs

### B. Existing Approaches Revisited

1. DCLF-DCBF
2. MPC-DCBF
   However, MPC-DCBF has a smaller region of feasibility than the DCLF-DCBF controller as more constraints are used to confine the optimal control input.
3. MPC-GCBF
   MPC-GCBF [18]: In the formulation (7), the CBF constraints are imposed on multi-steps along the horizon. This increases the computational complexity with a large horizon and the possibility of infeasibility also increases with more constraints. One way to suppress the computational complexity and enhance the feasibility is to apply a one-step CBF constraint.
   高阶DCBF：
   This approach is also generalized with consideration over the high relative-degree constraint, where constraints in (7e) are modified as constraints posed on two nonadjacent steps, where m represents the relative degree of the high-order safety constraint.
   ![20240108204744](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240108204744.png)
4. CLF-NMPC

## 3. CLFS AND CBFS UNIFIED WITH NMPC

In this section, we are going to present two proposed formulations: NMPC-DCBF and NMPC-DCLF-DCBF unifying discrete-time CLFs and CBFs with NMPC.

### A. Formulations

1. NMPC-DCBF
![20240108205614](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240108205614.png)
   - The control Lyapunov function V (xt+N |t) is used as a terminal cost scaled up with the parameter β.
   - The terminal cost as CLF adopts the fashion of work from the field of MPC, as noted in [21], where stability usually can be achieved without the need to specify a terminal state constraint if β is selected large enough.
   - Different from the formulation in (7), the decay rates of control barrier functions are relaxed from the fixed value1 − γk into optimization variables ωk(1 − γk) and an additional cost about the relaxing rate variables ψ(ωk) ≥ 0is included in the optimization. This function ψ can be tuned for different performance.
   - MCBF ≤ N is applied for CBF constraints, which allows us to choose the appropriate value of MCBF to reduce the computational complexity.
   - NMPC-DCBF represents a generalized form of MPC-DCBF and MPC-GCBF with the relaxing technique of decay rates of safety constraints.
   - MPC-GCBF的缺点：However, one-step constraint might not confine the system sufficiently and the optimization problem may become infeasible after a while in the closed-trajectory. 因而 In our proposed approach, we continue to use the multi-step constraints, which guarantee stronger set invariance with less assumptions.
   - To apply NMPC-DCBF on a high-relative degree system, we just simply need MCBF ≥ m, where m represents the relative-degree defined in (10).
2. NMPC-DCLF-DCBF
![20240108214330](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240108214330.png)
   - Alternatively, the stability criteria with CLF could be posed as constraints instead of as a terminal cost
   - where MCLF and MCBF are the horizon length for CLF and CBF constraints respectively, which can be chosen to be less than the prediction horizon N .
   - NMPC-DCLF-DCBF represents a generalized form for DCLF-DCBF with horizon lengths for cost and constraints. When the horizon lengths for CLF and CBF constraints equal to one, i.e., MCLF = MCBF = 1, the NMPCDCLF-DCBF becomes exactly as DCLF-DCBF except the decay rate of CBF constraint is relaxed.

## 4. THEORETICAL ANALYSIS

In this section, we are going to illustrate theoretically the advantages about feasibility and safety of the proposed approaches.

### A. Theoretical Analysis of Feasibility

1. reachable set和safe region（CBF约束得到的下一个时间步状态的范围）的概念
![20240108224229](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240108224229.png)
2. The optimization of MPC-DCBF is feasible when the intersections between the reachable set RMPC-DCBFk and safe setSMPC-DCBFk at time t + k are non-empty for all k.
3. To sum up, as the relaxing technique for decay rates is applied in NMPC-DCBF and NMPC-DCLF-DCBF, we can state they outperform MPC-DCBF / MPC-GCBF / DCLF-DCBF from the perspective of feasibility.
4. In (19), it shows that SNMPC-DCBFk = C, which is the same as the region enforced by the distance constraint (3). This reveals the NMPC-DCBF holds the same feasible region as MPC-DC

### B. Theoretical Analysis of Safety

1. γk参数对MPC-DCBF/MPC-GCBF/DCLF-DCBF的两面性
   By reducing γk for MPC-DCBF / MPC-GCBF / DCLFDCBF, the system safety will increase as the smaller γk represents a slower decay rate of lower bound of control barrier function, see (4). However, from (17), we can see that reducing γk for MPC-DCBF makes SMPC-DCBFk smaller, which leads the optimization more likely to be infeasible along the trajectory as the intersection between the reachable set and the region constrained by safety constraint decreases. This leads to a tradeoff between feasibility and safety. This tradeoff also happens among DCLF-DCBF and MPC-GCBF with similar reasons and forces us to choose either feasibility or safety for performance.
2. ψ(ωk)函数设计
   可以参考，感觉有很多可以改变、优化之处，比如不需要γk参数，只用ωk进行调节安全性与可行性之间的关系。
3. When ωk = 0, the relaxed CBF constraint becomes equivalent to a simple distance constraint and MPC with distance constraints (MPC-DC [4]) needs longer horizon to generate an expected obstacle avoidance performance in a closed-loop trajectory. Therefore, it's not recommended to set a relatively too small value for Pω , which would overrelax the CBF constraint, i.e., the optimized value of ωkcould be too small.
4. 论文中说的相比于其他论文同时提高可行性与安全性：
   To sum up, by reducing γk and utilizing an appropriate form of the additional cost function for decay-rate slack variable ωk, the proposed approach would outperform the existing formulations in term of safety while not harming feasibility performance.
   However, in the case of our proposed NMPC-DCBF, the region confined by safety constraint won't be affected by changing the value of γk, as shown in (19). Hence, the intersection between the reachable set and the region constrained by safety constraint is independent ofγ. This allows us to enhance the safety by reducing γk while not harming feasibility, which resolves the tradeoff between feasibility and safety.

## 5. NUMERICAL EXAMPLES & RESULTS

### A. Numerical Results for Feasibility

1. To sum up, the proposed formulations outperform the state-of-the-art in terms of feasibility.

### B. Safety

1. MPC-GCBF becomes infeasible after around 5 seconds in a closed-loop trajectory starting from the initial condition. This arises from the fact that the one-step constraint doesn't sufficiently confine the system for safety and leads the system into an infeasible state after a while.

## 6. CONCLUSION & FUTURE WORK
