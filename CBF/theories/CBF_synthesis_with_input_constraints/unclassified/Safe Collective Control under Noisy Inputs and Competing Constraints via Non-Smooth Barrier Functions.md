# Safe Collective Control under Noisy Inputs and Competing Constraints via Non-Smooth Barrier Functions

## Key Points

**开展的工作：**

- 这篇文章将多个同种智能体的安全控制，将多智能体看作统一的一个智能体，将所有智能体的状态组合成一个状态向量，将所有智能体的控制输入组合成一个控制向量，将每个智能体的状态约束一起组合，合成一个CBF，然后做安全控制。（个人认为这种多个智能体状态和控制量的直接叠加计算效率堪忧）。
- 主要涉及两方面的技术：多状态约束的平滑近似——polynomial smoothing technique，仿真中比log-sum-exp平滑近似效果好；带有概率CBF约束的stochastic model-predictive control (SMPC)（可能是因为考虑了输入有扰动，所以这里是有概率的约束）.
- 本文并没有考虑输入约束怎么特殊处理，只是在SMPC框架中作为硬约束，虽然对可行性进行了一些条件设定有所缓解，但感觉依然存在可行性问题。

**future work:**
safe controls can be synthesized (locally) for collectives by considering the ensemble as one agent, computing controls, and propagating the resulting optimal values (component-wise) to individual agents

**摘要：**

- 任务：We consider the problem of safely coordinating ensembles of identical autonomous agents to conduct complex missions with conflicting safety requirements and under noisy control inputs.
- 方法：Using non-smooth control barrier functions (CBFs) and stochastic model-predictive control as springboards and by adopting an extrinsic approach where **the ensemble is treated as a unified dynamic entity**, we devise a method to synthesize safety-aware control inputs for uncertain collectives, drawing upon recent developments in Boolean CBF composition and extensions of CBFs to stochastic systems.
- 对方法的进一步说明：Specifically, we approximate the combined CBF by a smooth function and solve a stochastic optimization problem, with agent-level forcing terms restricted to the resulting affine subspace of safe control inputs.
- 对平滑近似步骤的说明：For the smoothing step, we employ a polynomial approximation scheme, providing evidence for its advantage in generating more conservative（这里的保守不是指安全集的大小，而是对nominal controller的改变量很小，9.B的仿真讨论中有提到） yet sufficiently-filtered control signals than the smoother but more aggressive equivalents realized via an approximation technique based on the log-sum-exp function（log-sum-exp近似对nominal controller的改变比较激进）.

**Key Words：**
control barrier functions, multi-agent systems, safety-critical control, stochastic model-predictive control

## 1. INDRODUCTION

1. 前面两段主要讲问题的背景，就是在实际中多智能体协同运行的安全很重要，但是它们之间的目标可能会出现冲突；系统模型和输入存在潜在不确定性；讲讲CBF在不确定环境中的应用及将多个安全限制条件进行组合。
2. 已经有很多对多状态约束组成一个CBF进行研究：In the deterministic case, a number of studies have presented CBF composition techniques for capturing diverse safety requirements (see [ 1], [2]).
3. 随机系统的CBF

### A. Scientific Contributions

1. 本文用的两个方法：polynomial smoothing function和stochastic quadratic program
   Leveraging new-found ideas on Boolean composition of CBFs with smooth approximation, we report results on synthesizing safe controllers for ensembles under complex tasking and noisy inputs. In contrast to similar work [2], however, we apply a polynomial smoothing function in the smoothing step and synthesize control inputs via a stochastic quadratic program.
2. non-smooth CBF (NCBF)
3. stochastic model-predictive control (SMPC)

### B. Outline

## 2. NON-SMOOTH CONTROL BARRIER FUNCTIONS

介绍了带有扰动输入的动力学系统、这种系统的CBF形式和stochastic quadratic programming的公式。

## 3. COMPOSING CBFS VIA BOOLEAN LOGIC

介绍了ensemble-level safe set的概念
![20240207095943](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240207095943.png)

## 4. APPROXIMATING NCBFS VIA POLYNOMIALSMOOTHING

1. Since hΣ is non-smooth and, thus, unfit for quadratic optimization, in this section, we discuss a parametric polynomial smoothing technique for finding an approximation of hΣ.
2. 这一章介绍了parametric polynomial smoothing technique，方法参考的文献[7]。

## 5. SMPC WITH POLYNOMIAL-APPROXIMATED NCBFS

1. 介绍了随机MPC/随机二次规划，没有对输入约束进行额外处理，而是将其直接作为SMPC的约束，这样其实就存在求解可行性的问题
![20240207193949](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240207193949.png)
2. 文中也提到了可能存在求解可行性问题Due to the hard input constraints and chance constraints, SMPC problems of the form (14) are generally intractable [8]，也提出了一些设定来提升求解可行性。

## 6. THEORETICAL RESULTS

1. 平滑近似需要量化近似的精度：To quantify the accuracy of the CBF approximation with respect to the choice of parameter
2. 综合了Polynomial Smoothed NCBFs and Stochastic Quadratic Programming的整套控制算法
![20240207200157](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240207200157.png)

## 7. MULTI-AGENT SAFETY NOTIONS

1. 对多智能体安全的描述

## 8. NUMERICAL EXAMPLES

1. 感觉这里的设计可以优化：Assuming identical agents, we can then write the ensemblelevel dynamics for the single-integrator collective as  ̇x = u + (kw ⊗ IN )w, with x = [x1, y1, x2, y2, . . . , xN , yN ]T and u = [u1, u2, . . . , uN ]T。因为这样每多一个智能体状态向量就要增加维度，求解效率低下.

## 9. RESULTS & DISCUSSIONS

这一节主要是多项式平滑近似与log-sum-exp近似在仿真中表现的对比分析。

### A. Safety-Critical Control under Varied Safety Specifications

1. 在仿真中本文的多项式平滑近似比log-sum-exp近似表现更好
   we notice that ˆhΣ admits a zero value for the LSE approximation scheme, which may cause the controller to revert to its nominal value, hence violating the safety constraints and effectively invalidating such CBF. ˆhΣ is also less sensitive to the smoothing parameter for the polynomial approximation scheme than for the LSE technique.

### B. Effect of β on Safety-Critical Control

1. 继续将多项式平滑近似与log-sum-exp近似进行对比
   we observe that the polynomial smoothing technique tends to generate more conservative control actions that are adequate for the task and closely track the nominal CBF controller, modifying it only minimally, while that of the log-sum-exp function is more aggressive, exhibiting larger deviations from the nominal CBF-based controller, for unsafe control actions.

### C. Control Input Computation Time

1. 作者这里用的并行程序，所以计算的很快：
   Simulations were conducted using a workstation equipped with an AMD 7950x 16-core processor and 128 GB of RAM, with software programs optimized for parallel processing.

## 10. CONCLUSIONS

1. 作者在这篇文章里将多智能体看作统一的一个智能体，将所有智能体的状态组合成一个状态向量，将所有智能体的控制输入组合成一个控制向量，将每个智能体的状态约束一起组合，合成一个CBF，然后做安全控制。
   safe controls can be synthesized (locally) for collectives by considering the ensemble as one agent, computing controls, and propagating the resulting optimal values (component-wise) to individual agents
