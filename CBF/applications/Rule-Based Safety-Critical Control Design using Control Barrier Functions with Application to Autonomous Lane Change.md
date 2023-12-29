# Rule-Based Safety-Critical Control Design using Control Barrier Functions with Application to Autonomous Lane Change

## Key Points

**safety filter:**

- safety monitor: handmake->多个CBF、CLF、输入/状态限制直接作为约束
  使用了有限状态机，每个状态均handmake多个CBF
![20231211170845](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231211170845.png)

- intervention scheme: QP
![20231211170921](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231211170921.png)
- task policy
  由CLF来确保控制性能。
- fallback policy

**开展的工作：**

In this paper, we presented a safety-critical lane change control design using rule-based CLF-CBF-QP formulation. Utilizing a FSM, we divide a lane change maneuver into different states, which allows the proposed strategy to function as both a planner and a controller. A quadratic program based safety-critical control is applied to achieve optimal lane change motion while guaranteeing safety. We tested the proposed control design using three pre-designed typical driving scenarios and 5000 randomly generated tests in different scenarios to show the effectiveness and robustness.

**future work:**

1. 利用车辆动力学模型替换车辆运动学模型it is desirable to explore the use of a nonlinear nonaffine dynamic bicycle model in the future work.
2. Besides, in this work, we assume the perception system is able to sense surrounding environment accurately and the controller can receive the sensors' measurements without time delay. To enhance the performance of our safety-critical controller, we need to incorporate a state estimator and introduce a safety margin for the noisy data from distance estimation between the ego vehicle and surrounding ones. The communication time cost between sensors and controller should also be considered in the future work.

**对象：**
车辆自动变道

**使用或开源的数据集：**
无

**是否开源：**
是，网址<https://github.com/HybridRobotics/Lane-Change-CBF>

**摘要：**
This paper develops a new control design for guaranteeing a vehicle's safety during lane change maneuvers in a complex traffic environment. The proposed method uses a finite state machine (FSM), where a quadratic program based optimization problem using control Lyapunov functions and control barrier functions (CLF-CBF-QP) is used to calculate the system's optimal inputs via rule-based control strategies. The FSM can make switches between different states automatically according to the command of driver and traffic environment, which makes the ego vehicle find a safe opportunity to do a collision-free lane change maneuver. By using a convex quadratic program, the controller can guarantee the system's safety at a high update frequency.

**Key Words：**
无

## 1. INTRODUCTION

1. mid-level path planner+mid-level path planner方案存在的的缺陷：
   （不从这篇论文的角度讲，这也是可以看做使用CBF做底层安全保护的原因）
   However, the mid-level path planner usually can not be updated at a high frequency and may not respond to a sudden threat immediately, which means its planned trajectory may not always meet safety-critical requirements in a fast changing environment. Furthermore, there are always notable tracking errors in the low-level controller, which means tracking a collisionfree trajectory could still be potentially unsafe. Therefore, in a safety-critical autonomous lane change strategy, safety relevant constraints should be considered in the low-level controller directly and the controller must work at a high update frequency.
2. CBF-CLF的计算复杂度很低：
   Due to its low computational complexity, this quadratic program allows the low-level controller to work at a high update frequency, which motivates us to investigate the safety-critical lane change control design through the CLFCBF-QP formulation.
3. 标题中的rule-based strategy指的是有限状态机FSM.
4. FSM的优势：
   Since its computational complexity is lower than that of a traditional path planner, **the FSM can be used in a low-level controller and work at a high update frequency**, which inspires us to use a well-designed FSM to replace the mid-level path planner in traditional lane change strategies.
5. 因而用FSM+CBF代替mid-level path planner+mid-level path planner
   本文提出的方法及作用效果：
   we propose a rule-based safety-critical lane change control design. A FSM works as the basic structure, where a quadratic program based optimization problem using CLF and CBF constraints (CLFCBF-QP) is formulated to achieve control objectives and guarantee the system's safety. The FSM can unify the midlevel path planner and low-level controller in traditional lane change strategy as one: a low-level safety-critical controller, see Fig. 1. The FSM is used to make the decision if the ego vehicle can do a collision-free lane change maneuver or not. If the current traffic environment isn't suitable for a lane change maneuver, the ego vehicle will keep the current lane until a safe situation occurs. Additionally, if a threat arises during a lane change maneuver, the FSM will enter another state to drive the ego vehicle back to its current lane. Since the safety relevant constraints are considered in the lowlevel controller directly and a quadratic program allows the controller to run with high update frequency, our proposed strategy can guarantee the ego vehicle's safety in complex environments.
6. 有限状态机的作用：
   The FSM helps the proposed strategy do switches between multiple CBF constraints in a complicated environment.

## 2. BACKGROUND

### A. Vehicle Model

1. From [20], authors show that the kinematic bicycle model works under small lateral acceleration and also recommend 0.5μg as a limitation for the validity of the kinematic bicycle model (μ is friction coefficient and g is gravitational acceleration).

### B. Safety-Critical Control

## 3. CONTROL DESIGN

### A. Finite State Machine

FSM状态和输入的设计

### B. Safety-Based Conditions for Switches of CBFs

1. 要确保the continuity of the system's safety under different CBF constraints
   This asks the controller to guarantee the continuity of system's safety.
2. 文章使用的保证连续安全的方法：
   As shown in Fig. 3, system's CBF constraints before and after a switch can be described as safe sets C1 and C2, respectively. When h2(x, t) replaces h1(x, t) as the new CBF constraint, if the system's state x is in the intersection of C1and C2, the new barrier function h2(x, t) will make the new safe set C2 invariant after the switch, which will guarantee the system's safety. This condition is used to design switches between different CBF constraints in this paper.

### C. Rule-Based CLF-CBF-QP Formulation

1. Through CLF constraints, it is possible to track a desired position without a reference trajectory.
2. CLF和CBF都是根据作者设定的规则handmake，即在不同状态下有哪些控制目标和安全限制。
3. 通过合理设计状态转换，确保the continuity of the system's safety under different CBF constraints.
4. 通过多约束的直接组合，构建CBF-CLF-Qp
![20231211162317](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231211162317.png)

## 4. RESULTS

### A. Simulation with Pre-designed Typical Scenarios

### B. Simulations with Randomly Generated Tests

## 5. DISCUSSION

1. 未来的改进方向：
   it is desirable to explore the use of a nonlinear nonaffine dynamic bicycle model in the future work.
   Besides, in this work, we assume the perception system is able to sense surrounding environment accurately and the controller can receive the sensors' measurements without time delay. To enhance the performance of our safety-critical controller, we need to incorporate a state estimator and introduce a safety margin for the noisy data from distance estimation between the ego vehicle and surrounding ones. The communication time cost between sensors and controller should also be considered in the future work.

## 6. CONCLUSION
