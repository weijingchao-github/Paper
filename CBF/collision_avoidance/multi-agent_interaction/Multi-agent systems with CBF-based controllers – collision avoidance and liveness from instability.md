# Multi-agent systems with CBF-based controllers – collision avoidance and liveness from instability

## Key Points

本文研究多智能体互相躲避(如two agents negotiating the passing order through an intersection)的liveness, collisions, and feasibility，以及平衡点的结构、稳定性与死锁(gridlock)的关系等问题，涉及Centralized, DF, DR, CCS and PCCA这5种算法。
**比较深奥，暂时看不懂**

给出的一个研究展望：it is not known to the authors how to design a control policy that creates unstable equilibria or modify an existing one to have this property.

## 1. Introduction

1. 本文研究多智能体互相躲避的liveness, collisions, and feasibility，以及平衡点的结构、稳定性与死锁的关系等问题。
2. CBF与MPC的对比：
   A few noteworthy differences between CBF and MPC include (i) MPC generally relies on a set of linearized dynamic systems to cover the nonlinear model range, whereas CBF deals with the nonlinear (but control affine) model directly, (ii) for nonconvex constraints, MPC requires convexification, sequential convex programming, or mixed integer programming, while CBFs do not see them as such, and (iii) MPC takes advantage of future state prediction whereas CBF does not.
3. One contribution of this paper is a proof that the centralized, distance-CBF based QP problem is always feasible.
4. 多智能体交互的环境分为controlled environment和less controlled scenarios
    In a controlled environment with all agents having the ability to communicate.
    In less controlled scenarios such as vehicles operating on roadways, or multi-brand robots operating without common communication protocols.
5. 提到并介绍了很多less controlled scenarios情况下多智能体交互的算法。
6. 提到通过仿真实验，对比了不同算法的liveness, collisions, and feasibility性质：We then proceed to compare algorithm metrics on liveness, collisions, and feasibility through a randomized five-agent Monte-Carlo simulation trials for each method.
7. 提到了多智能体交互会产生死锁问题。
8. 推断各算法得到的平衡点结构与稳定性与死锁倾向相关：We conjectured that the equilibrium structures and their stability play a decisive role in determining propensity to gridlock.
9. 介绍了不同算法在实际控制中在出不出现死锁问题的表现。
10. 介绍了论文的架构。

## 2. ROBUST CONTROL BARRIER FUNCTIONS REVIEWED

## 3. HOLONOMIC AGENT MODEL

1. 智能体数学模型的构建
2. CBF的设计(handmake)

## 4. CBF-BASED COLLISION AVOIDANCE ALGORITHMS

1. 多智能体交互时：假设其他物体静止（The problem, of course, is that the host does not know other agents' preferred accelerations, so zeros are used instead of unknown u0j 's.），不能对其他物体一起控制，只能对每个agent进行单独CBF控制不能保证安全
![20231208153711](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231208153711.png)
多智能体协同CBF控制能保证安全
![20231208154158](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231208154158.png)
2. 后面介绍了Decentralized Reciprocal QP, CCS QP, PCCA QP方法，感觉有些方法可能只适用于论文中设定的场景。

## 5. 5-AGENT SIMULATION RESULTS

1. 对Centralized, DF, DR, CCS and PCCA这几种算法进行仿真，To assess the algorithms, a set of metrics was devised to compare liveness, collisions, and feasibility.

## 6. EQUILIBRIUM INSTABILITY AND LIVENESS

1. 探讨gridlock，平衡点和平衡点稳定性问题：
   It turns out that the policies that exhibited gridlocks (DF, DR, CCS) create a set of stable equilibrium (gridlock) points, while for those that did not (Centralized, PCCA) there is a single unstable equilibrium point in the physical space. In other words, the liveness in these multiagent systems comes from instability.

### A. DF and DR equilibria and their stability

### B. Centralized controller equilibrium analysis

### C. CCS equilibrium analysis

### D. PCCA equilibrium analysis

### E. Summary of the equilibrium analysis and simulations

1. While one distinction between decentralized, host-only-control policies and co-optimization policies is related to feasibility, it is not correlated to liveness and absence of gridlocks. The actual mechanism for gridlock avoidance is the presence of unstable equilibria in the joint agent space. The policies that have unstable equilibria (Centralized and PCCA) produced no gridlocks in the 5-agent Monte Carlo simulations. In contrast, the policies with stable equilibria had gridlocks observed.

## 7. CONCLUSIONS

This paper compared several CBF-based control policies for their performance in multi-agent scenarios. The results show that algorithms that take all the constraints into account and have or pretend to have control over all the agents, have lower convergence times and, as proven in this paper, are always feasible. The Centralized and PCCA policies showed minimal violations while the Decentralized Follower and Reciprocal methods had a few larger violations due to infeasibility. The CCS algorithm, structurally close to PCCA, showed liveness behavior more similar to Decentralized policies – lower mean convergence time, but about the same number of gridlocks. To explain the observed behavior, we analyzed the policies applied to a simpler 2-agent problem. It turned out that the policies exhibiting good liveness and lack of gridlock in simulation have unstable equilibria in the joint agent space, while policies with observed gridlock have stable equilibria. Beyond the retroactive analysis provided in this paper, it is not known to the authors how to design a control policy that creates unstable equilibria or modify an existing one to have this property.
