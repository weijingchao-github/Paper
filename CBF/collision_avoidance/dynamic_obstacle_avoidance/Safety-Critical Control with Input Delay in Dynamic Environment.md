# Safety-Critical Control with Input Delay in Dynamic Environment

## Key Points

**开展的工作：**

- 考虑动态环境的CBF：We establish the notion of environmental control barrier functions (ECBFs) for delay-free systems to explicitly address scenarios in which safety is affected by a dynamic environment.
  ![20231206113643](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231206113643.png)
  考虑环境状态有扰动保证安全的CBF：ECBFs rely on the environment's state e and its derivative ̇e. In practice, these quantities are typically estimated with uncertainty. Thus, now we robustify safety-critical controllers against uncertainties in the environment. We provide robustness based on worst-case uncertainty bounds (i.e., in a deterministic fashion).
  ![20231206114001](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231206114001.png)
- 考虑输入延迟的CBF：We connect the theories of CBFs and predictor feedback by developing the notions of CBFs and ECBFs for systems with input delay and synthesizing safety-critical controllers via predictor feedback. Predictors require special care in dynamic environments as the environment's future cannot be predicted accurately. Thus, we make controllers robust against prediction errors.
![20231206114320](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231206114320.png)
- We demonstrate the efficacy of this framework on reallife engineering systems where time delays and dynamic environments both occur, through the examples of adaptive cruise control and obstacle avoidance with a Segway.

We have discussed safety-critical control for systems with input delay that operate in dynamically evolving environment. We have provided formal safety guarantees and proofs thereof. We have established a method for safe control synthesis by proposing environmental control barrier functions and integrating them with predictor feedback. We have strengthened the underlying safety condition to provide robustness against uncertain environments, in which the future of the environment cannot be predicted accurately but bounds on the related prediction error are known. The resulting control design uses worst-case uncertainty bounds and is provably safe.

**future work:**

1. input-to-state safety
2. Our future work includes the analysis of prediction errors, control of systems with both state and input delays, and use of control barrier functionals acting on delayed states.

**对象：**
两个：1）ACC 2）Segway避障
We have demonstrated the method by an adaptive cruise control problem where the motion of another vehicle creates an uncertain environment, and by a Segway controller that avoids moving obstacles.

**使用或开源的数据集：**
无

**是否开源：**
否

**摘要：**
This paper develops a framework for safety-critical control in dynamic environments, by establishing the notion of environmental control barrier functions (ECBFs). Importantly, the framework is able to guarantee safety even in the presence of input delay, by accounting for the evolution of the environment during the delayed response of the system. The underlying control synthesis relies on predicting the future state of the system and the environment over the delay interval, with robust safety guarantees against prediction errors.

**Key Words：**
Delay systems, Dynamic environment, Predictive control, Robust control, Safety-critical control

## 1. INTRODUCTION

为什么要将环境考虑进CBF：safety is often affected by a dynamic environment that surrounds the control system.

1. 动态环境下对安全性的要求：
   Strict safety requirements call for theoretical safety guarantees and provably safe controllers. Thus, control synthesis must take into account how the control system interacts with its environment, and it must ensure that environment's evolution does not lead to safety violations. As such, dynamic environments pose a major challenge for safety-critical control.
2. 本论文开展的工作：
   In this paper, we explicitly involve dynamically changing environments into the framework for safety-critical control, in order to handle uncertain environments with worst-case safety guarantees in a deterministic fashion. Importantly, our framework also allows us to compensate the effect of input delay, which was not addressed in the literature.

## 2. PRELIMINARIES TO SAFETY-CRITICAL CONTROL

1. However, verifying that a given h is indeed a CBF is nontrivial when there are input constraints (U ⊂ Rm). An approach to overcome input constraints is the backup set method [17], that relies on the forward integration of the dynamics similar to predictor feedback presented in Section IV.

## 3. SAFETY IN DYNAMIC ENVIRONMENT

1. 提到了环境安全集的概念
2. 解决了在具有不确定状态的动态环境下如何用CBF保证安全

### A. Environmental Control Barrier Functions

1. environmental control barrier functions (ECBFs)，除了智能体的状态，还考虑环境的状态，来构建ECBF.

### B. Robust Safety in Uncertain Environment

1. ECBFs rely on the environment's state e and its derivative ̇e. In practice, these quantities are typically estimated with uncertainty.
2. 考虑的是一个非常保守的情景(waorst-case scenario)，即不确定性的上限
![20231205222733](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231205222733.png)
论文中假设不确定性的上限已知。
然后将不确定性问题变成一个确定的形式（也是在很多假设的前提下建立的）we provide robustness based on worst-case uncertainty bounds (i.e., in a deterministic fashion)
![20231205222926](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231205222926.png)
满足上面这个很保守的条件，就确保了在不确定状态的动态环境下的安全。

## 4. SAFETY OF SYSTEMS WITH INPUT DELAY

有输入延迟，就要对未来状态进行预测。
有输入延迟的系统
![20231206114830](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231206114830.png)

### A. Solution of the System and Predictors

1. 介绍了predicted state和predictor的概念。
2. 后文只讨论constant delay，可以拓展到time-varying and state-dependent delay的情况。

### B. Control Barrier Functions with Input Delay

1. 建立了具有输入延迟的CBF和QP的理论，以保证在输入延迟情况下的安全。

### C. Safety with Input Delay in Dynamic Environment

1. 将3.A与4.A综合起来，建立了具有输入延迟的ECBF和QP的理论，以保证在考虑环境状态、输入延迟情况下的安全。

## 5. CASE-STUDY: CONTROL OF A SEGWAY

### A. Safety-Critical Control in Dynamic Environment

### B. Safety-Critical Control with Input Delay

## 6. CONCLUSIONS
