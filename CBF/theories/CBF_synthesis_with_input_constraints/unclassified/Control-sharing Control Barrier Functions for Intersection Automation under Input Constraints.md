# Control-sharing Control Barrier Functions for Intersection Automation under Input Constraints

## Key Points

**开展的工作：**

- 这篇文章在考虑输入限制CBF和多CBF直接作为约束求解可行性是根据应用场景设计的，难以推广到其他应用场景，方法不具有通用性。
- 有几点可以学习的：第一章中的CBF两大挑战；第三章多个CBF的control-sharing property；第四章用四次超椭圆定义不规则智能体边界的方法；第四章给了状态约束后，通常的两类解决带有input constraints的方法；第四章在CBF或状态约束带有max-operator时，导致CBF不再是一个连续可微方程，这里提出一种平滑近似max{c, x}的方法；第五章在需要时可以扩充状态向量的方法（文中用的是线性系统，也可能可以推广到非线性系统）；第七章提到的CBF方法的两个缺陷（不具有预测能力，在geometric symmetry in the initial condition时容易出现dead-lock）

**future work:**
we envision to investigate a combination of MPC- and CBFbased control schemes. Additionally, we intend to study a distributed numerical solution of CBF-QP (25).

**摘要：**

This contribution introduces a centralized input constrained optimal control framework based on multiple control barrier functions (CBFs) to coordinate connected and automated agents at intersections.

**Key Words：**
无

## 1. INDRODUCTION

1. 这两篇文献里讲了CBF方法的限制与不足
   Given that CBFs have also their limitations and drawbacks [5], [7]
2. The utilization of CBFs, though, gets challenging when input constraints are present [5], [13] or multiple CBFs [14] are applied simultaneously. Then, it may happen that the resulting QP gets infeasible. To maintain safety guarantees, though, the CBFs have to be designed such that they are jointly feasible subject to input constraints [5], [8], [13].

### A. Contribution

1. In the remainder, we convey a centralized input constrained optimal control framework which relies on multiple CBFs to satisfy state and safety constraints, subject to bounded control inputs.
2. 提出了CBF研究中的两大主要挑战：
   - 多CBF同时可行For such setup, we prove that these CBFs are jointly feasible — referred to as control-sharing property [14].
   - CBF满足输入限制the utilized CBFs are provably compatible with input constraints.

## 2. INTERSECTION COORDINATION PROBLEM

### A. Problem Description

### B. Modeling

### C. Local and Global Coordinates

## 3. CBFS FOR CONSTRAINED CONTROL

### A. Background on CBFs

1. 多个CBF的control-sharing property：
![20240128163915](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240128163915.png)
   没有说状态的子集满足就拥有control-sharing property，还是所有状态满足才拥有control-sharing property.

### B. CBFs for Constrained Agent Velocity

### C. Control-sharing Property

## 4. COLLISION AVOIDANCE

### A. Geometric Formulation

1. 用四次超椭圆定义智能体的边界
![20240128193305](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240128193305.png)

### B. CBF Formulation

原始状态约束经验证不是一个真正的CBF，文章根据应用场景的特点（两车的安全距离是采用最大制动力刹车的刹车距离）来设计valid CBF，因为最大制动力的计算包含最大加速度a_max，所以构造的CBF满足输入约束。文章里也提到了这一点：CBF (20) is tailored to the straight crossing scenario. 方法难以推广到其他应用场景，不具有通用性。

1. 给了状态约束后，通常的两类解决带有input constraints的方法
![20240128173701](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240128173701.png)
   文章根据场景的特点使用了第一种方法构造CBF：
   we define the CBF such that the distance dij between the superellipse and Agent j's geometric center is lower bounded by a safety distance dsafe,ij which allows both agents to stop without a collision when exploiting their maximum braking capability along the vector Pj − Pi.
2. CBF方法容易造成死锁的现象：
   CBFs are generally known to be prone to deadlock-like situations, which can however be circumvented [7].
3. 在d_safe推导过程中有max-operator，从而导致CBF不再是一个连续可微方程，这里提出一种平滑近似max{c, x}的方法
![20240128195801](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240128195801.png)
    平滑近似的时候，需要over-approximate d_safe才能确保安全。

### C. Control-sharing Property

1. For every agent i and every two conflicting agents j, l ∈ Ac(i), the CBFs hc,ij (x) and hc,il(x) exhibit a control-sharing property, i.e., Kc,ij (x) ∩ Kc,il(x) 6 = ∅.
2. Collision avoidance CBFs (20) exhibit a control-sharing property with velocity CBFs (7a) and (7b).

## 5. CONTROLLER SYNTHESIS

1. 这种处理方法可以学习一下:有时候可以根据需要扩充系统状态向量
![20240128211818](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240128211818.png)
   这里因为是线性系统，打算用线性控制中的状态反馈控制-LQR-Riccati公式，通过让系统稳定让速度与参考速度差值逐渐减到零，所以扩充系统状态向量。

## 6. SIMULATION RESULTS

### A. Simulation Setup

### B. Discussion of Results

1. Due to the slightly conservative max-operator approximation in Section IV-B, the acceleration stays marginally above the minimum.
2. 求解速度挺快的：
   The centralized CBF-QP (25) has been solved in real-time, i.e., within 0.7 ms on average and 3.0 ms in the worst case.

## 7. CONCLUSION

1. CBF方法的几点缺陷：A limitation of CBFs, though, is their limited ability to exploit predictions (e.g. when other non-controllable road users come into play). Moreover, CBFs may be prone to deadlock-like situations, e.g., due to geometric symmetry in the initial condition.
2. 未来展望：Therefore, we envision to investigate a combination of MPC- and CBFbased control schemes. Additionally, we intend to study a distributed numerical solution of CBF-QP (25).
