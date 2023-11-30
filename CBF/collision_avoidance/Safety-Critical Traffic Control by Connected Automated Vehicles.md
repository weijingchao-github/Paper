# Safety-Critical Traffic Control by Connected Automated Vehicles

## Key Points

**safety filter:**
![20231130111453](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231130111453.png)

- safety monitor: handmake -> multiple
![20231130111414](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231130111414.png)
- intervention scheme: QP
![20231130111553](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231130111553.png)
- task policy
- fallback policy

**开展的工作：**
In this paper, we propose a safety-critical traffic control (STC) strategy for mixed-autonomy traffic systems, in which a single CAV leads several HDVs such that it both guarantees safety and achieves string stability.
In this paper, we proposed a safety-critical traffic control (STC) framework, in which the **longitudinal motions** of connected automated vehicles (CAVs) are regulated amongst connected human-driven vehicles (HDVs) in mixed-autonomy traffic flows.
Moreover, we employed **state observer-based CBFs** to establish STC when the CAV does not have access to all the states of the following HDVs.

**future work:**
In our future work, we plan to investigate the effects of partial connectivity and address feedback, communication and actuation delays for the safety-critical control of mixed-autonomy traffic.

**对象：**
single-lane mixed traffic including a head HDV, a CAV and several following HDVs
(human-driven vehicles (HDVs)、connected automated vehicles (CAVs))

**仿真工具：**
未提

**使用或开源的数据集：**
We leverage the Next Generation Simulation (NGSIM) dataset that is widely used in transportation research.

**是否开源：**
否

**摘要：**
This paper proposes safety-critical traffic control (STC) by CAVs—a strategy that allows a CAV to stabilize the traffic behind it, while maintaining safety relative to both the preceding vehicle and the following connected human-driven vehicles (HDVs). Specifically, we utilize control barrier functions (CBFs) to impart collision-free behavior with formal safety guarantees to the closed-loop system. The safety of both the CAV and HDVs is incorporated into the framework through a quadratic program-based controller, that minimizes deviation from a nominal stabilizing traffic controller subject to CBF-based safety constraints. Considering that some state information of the following HDVs may be unavailable to the CAV, we employ state observer-based CBFs for STC. Finally, we conduct extensive numerical simulations—that include vehicle trajectories from real data—to demonstrate the efficacy of the proposed approach in achieving string stable and, at the same time, provably safe traffic.

**Key Words：**
Connected Automated Vehicle, Mixed Traffic, Traffic Control, Safety-Critical Control, Control Barrier Function, State Observer

## 1. INTRODUCTION

### 1.1 Traffic Control by Connected Automated Vehicles

1. Traffic Control方法可以分为road-based traffic control和vehicle-based traffic control两类，目前vehicle-based traffic control是CVA的主流；

2. 综述了现有vehicle-based traffic control的方法（主要是纵向控制的），指出这些方法的不足在于只保证string stable但无法保证安全。

### 1.2 Safety of Mixed-autonomy Traffic

### 1.3 Contributions

- A quadratic program-based controller is constructed for CAVs, that incorporates a nominal stabilizing traffic controller and safety-constraints derived from control barrier functions—the end result being safety and string stability simultaneously.
- Safety guarantees are provided both for the CAV as hard constraint and for the following HDVs as soft constraints. These guarantees are based on various safety measures (TH, TTC and SDH) that are analyzed and compared.
- STC is extended to the case of output feedback by the help of state observers to address scenarios in which the CAV does not have access to all the states of the HDVs. To this end, a state observer-based CBF approach is formulated.
- Extensive numerical simulations are conducted to show the benefits of the proposed STC, identify its limitations, and analyze the effect of parameters. The simulations also incorporate real trajectory data for the head HDV.

![20231130095408](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231130095408.png)

...
