# Control Barrier Function-Based Quadratic Programs Introduce Undesirable Asymptotically Stable Equilibria

## Key Points

**摘要：**

1. 提出问题：In this letter, we show that this framework(QP) can introduce equilibrium points (particularly at the boundary of the safe set) other than the minimum of the Lyapunov function into the closed-loop system. We derive explicit conditions under which these undesired equilibria (which can even appear in the simple case of linear systems with just one convex unsafe set) are asymptotically stable.
2. 分析QP导致的平衡点的存在性和稳定性。
3. 解决办法：To address this issue, we propose an extension to the QP-based controller unifying CLFs and CBFs such that the resulting system trajectories avoid the undesirable equilibria problem on the boundary of the safe set.（仅解决安全集边界平衡点的问题，并且该方法对系统等有一些假设）
![20231204152020](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231204152020.png)
4. The solution is illustrated in the design of a collision-free controller.

## 1. INTRODUCTION

1. CBF-CLF-QP的应用场景：
   collision-free control for multi-robot systems [16], persistent control for teams of mobile robots [10], bipedal robot walking [6], safe learning of system dynamics [17], and adaptive safety using CBFs in the presence of parametric model uncertainty [15].
2. 现有QP框架存在的问题：
   However, the QP-based framework shared across these works suffers from an important limitation. While it guarantees invariance of the system trajectories with respect to the safe set as a hard constraint, it softens the stabilization objective, maintaining the feasibility of the constrained optimization problem everywhere. In this letter, we demonstrate using a simple example that this methodology can introduce equilibria other than the minimum of the CLF into the closed-loop system, and that these undesirable equilibria can even be asymptotically stable.
3. 本文开展的工作：
   This letter adds to the literature in the following important ways. First, it demonstrates, both theoretically and by means of numerical simulations, that the QP-based controller with CLF-CBF constraints proposed by [3] introduces undesired equilibria other than the CLF minimum into the resulting closed-loop system. Secondly, a sufficient condition under which the resulting undesired equilibria are asymptotically stable are explicitly derived for the integrator system. Finally, we propose an extension to the QP-based controller unifying CLFs and CBFs that explicitly bypasses the undesirable equilibria problem on the boundary of the safe set. The solution is illustrated in the design of a collision-free controller.

## 2. QUADRATIC PROGRAMS FOR SAFETY CRITICAL SYSTEMS

## 3. ANALYSIS OF THE CLOSED-LOOP SYSTEM WITH QP-BASED CONTROLLER

### A. Existence of Equilibrium Points

1. 推导了一个QP的平衡点有哪些的（是否通用用的时候需要手推一下，注意是否是在f(0)=0，V(x)平衡点是0等假设下推导的）公式。

### B. Stability of Equilibrium Points

1. It was already shown that, in general, the origin is not an unique equilibrium point of the closed-loop system (3) with u*(x) given by (4). In this section, the objective is to estabilish an example showing that some of these equilibria can be asymptotically stable.
2. 推导了integrator system在安全集边界的平衡点渐进稳定的一个充分条件。

## 4. LYAPUNOV SHAPING FOR QP-BASED CONTROLLERS

1. We now seek to design a stabilizing controller u*(x) such that the resulting closed-loop system (3) does not contain boundary equilibria.
2. Finally, we propose a modification on the QP-based approach by [3] to achieve stabilization and safety for (3) without boundary equilibria, under certain feasibility conditions.（这个方法假设了很多条件，要使用时看看自己的系统是否符合这些条件）

![20231204152020](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231204152020.png)

## 5. SIMULATION RESULTS

## 6. CONCLUTION
