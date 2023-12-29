# The Safety Filter: A Unified View of Safety-Critical Control in Autonomous Systems

## Key Points

1. introduces a mathematical formalism that brings a broad class of the safety filters reviewed in this paper under a common lens. The exposed modular structure can be used to reconceptualize a range of well-established safety filters, as well as to guide the construction of new ones.

### 思考

1. 如何设置intervention才能更好的保证控制系统的性能表现？

## 1. INTRODUCTION

1. 介绍了为什么要写这篇综述：
   This review is driven by the conviction that connecting these approaches under a common theory will facilitate the transfer of insights between them, reducing the duplication of work and ultimately speeding up the much-needed progress in the field as a whole.
2. 有哪些Safety Filter：
   分为两类，一类是model-based approaches，包括control barrier functions (1), model predictive control (2), and reachability analysis (3)；另一类是data-driven schemes, featuring learned certificates (4), adversarial reinforcement learning (5), and self-supervised safety analysis (6)；
3. 在学习方法和优化方法(Learning and optimization)进步下会出现越来越多的新安全控制方法；
4. 这篇综述的亮点：
   unique in providing a unified conceptual and theoretical framework under which to identify common features and distill key ideas from the plethora of recent research advances.

## 2. SAFE DYNAMIC DECISION-MAKING

**Key:** To discuss and compare the many safety filter approaches, we first establish in this section a common technical language to describe them.

### 2.1 System Model

#### 2.1.1 Dynamic modeling and predictive uncertainty

1. The system is, in general, also subject to a **disturbance input**, denoted by d ∈ D, which captures the model's **predictive uncertainty**, including exogenous factors (e.g., wind), changes in operating conditions (e.g., motor wear), and overall modeling error.

#### 2.1.2 Sensor modeling and perceptual uncertainty

1. 主要是讨论了状态完全可观测和偏可观测这件事。
2. 关键词：perfect state observability, information state, "mixed observability".

### 2.2 Safety Specifications

#### 2.2.1 Failure conditions

1. 概念：failure set, constraint set

#### 2.2.2 All-time safety and controlled-invariant sets

1. 概念：safe set, safety, stability, Robust controlled invariant set, Probabilistic controlled invariant set, maximal safe set, optimal safety policy
2. 找safe set方面的困难：In most cases, finding some safe set Ω is not particularly difficult; however finding onelarge enough to be of practical utility is less straightforward. 引出maximal safe set的概念。
3. 目标：The need to ensure safety without needlessly hindering the robot's operation.

#### 2.2.3 Safety in the face of uncertainty: robust vs. probabilistic guarantees

#### 2.2.4 Operational design domain: qualifying safety

1. 概念：operational design domain

### 2.3 Safety Filters: Reconciling Safety and Performance

1. 概念：safe learning
2. 安全和控制目标解耦(decoupling between safety and performance/safety-performance separation，研究安全的时候不用考虑控制目标；研究控制目标时不用考虑安全，此时安全只是输入约束的一部分):
   The above result means that it is possible to design a safety filter for a robotic system with no knowledge or consideration of the particular task objectives, only requiring the filter to be as permissive as possible while preventing any safety violations. In turn, the taskoriented control policy can then be relieved of the burden of maintaining safety, since it can be viewed as acting on a modified system shielded by the safety filter. From the task policy's perspective, this filtered system is incapable of entering the failure set, regardless of the commanded control actions. Because only unsafe actions are preempted by the filter, the robot is still able to achieve the optimal viable task performance. This decoupling between safety and performance serves as a sort of separation principle, enabling the independent design of safety-agnostic task policies and task-agnostic safety filters (see the Safe Learning aside).

## 3. SAFETY FILTERS

**Key:** The runtime operation of every safety filter can be conceptualized as two complementary functions: monitoring and intervention.
Safety filters can therefore be categorized attending to their safety monitoring methodology, their intervention scheme, the synthesis approach used to obtain the fallback safety strategy, and the safety assurances provided. Figure 3 presents a visual summary of the main safety filter classes reviewed in this paper, organized by these four characteristics.

### 3.1 Computing the Least-Restrictive Safety Filter: Dynamic Programming

1. A desirable safety filter is one that grants the robot as much freedom as possible to carry out its task while allowing no safety violations.
2. 概念：game of kind, game of degree, margin function
3. 方法：
   - 理论基础：
      1. safety analysis can be viewed as a **pursuit-evasion game** between a controller striving to avoid the failure set and an antagonistic disturbance agent aiming to steer the system into it。
      2. The Hamilton-Jacobi (HJ) reachability analysis framework uses level set representations to transform the pursuit-evasion game, conceptually formulated as a game of kind, into a game of degree.
   - 构造dynamic programming Isaacs equation
   - 通过DP求出V(x)，通过V(x)得到maximal safe set and optimal safety policy
   - construct a safety filter with value-based monitoring and switch-type intervention
4. 缺点：
   利用DP求解Isaacs equation时计算复杂且对内存要求高：The computation complexity and memory requirement of numerically solving Equation 9 for general nonlinear dynamics is exponential in the state dimension, which limits its applicability to systems with no more than six continuous state variables.
   目前已提出一些方法解决上述问题。
5. 方法特点：aim to tractably approximate Ω∗

### 3.2 Value-Based Safety Filters: Control Barrier Functions

1. 缺点：
   应用领域受限Unfortunately, existing CBF synthesis approaches tend to only work for restricted dynamical system classes and suffer from scalability issues, especially faced with complex high-dimensional robotic systems in multi-agent environments.
2. 方法特点：However, CBFs no longer encode or approximate the maximal safe set Ω∗.
3. 发展方向：
   Since their debut, CBF-based safety filters have been extended to handle discrete-time problems (51), perceptual uncertainty (52, 53), and, most recently, systems with probabilistic and worst-case uncertainty (54, 55).
4. CBF的难题主要在构造上：
   Contrasting with the efficient, systematic procedure for computing safe control actions given a known CBF, finding a valid CBF for a system of interest is often a nontrivial problem, and the search for computationally tractable and data efficient CBF synthesis methods remains an open research challenge.

### 3.3 Rollout-Based Safety Filters

**Key:** For high-dimensional dynamical systems, computing the optimal value function is prohibitive due to poor scalability, while CBF methods lack general constructive mechanisms. Instead, rollout-based safety filters aim to verify system safety at runtime by forwardsimulating ("rolling out") the dynamics model or solving a trajectory optimization problem.

#### 3.3.1 Model predictive shielding (MPS)

1. 方法：
   - Monitoring is conducted at each control cycle by simply checking if, after executing the candidate task control πtask(x), the fallback policy πè would safely drive the system state into Ω within the prediction horizon (a sufficient condition for all-time safety, although not generally necessary, and therefore typically conservative).
   - Intervention is then a binary policy switch: if the safety monitor's check is successful, the filter lets the task control πtask(x) through; if unsuccessful, it overrides it with the fallback policy πè, whose ability to preserve safety from x was necessarily verified at an earlier control cycle.

#### 3.3.2 Forward-reachable sets

1. 概念：forward-reachable set (FRS), Reachability-based Trajectory Design (RTD)
2. 方法：
   Given an initial state and a control policy, the FRS contains all possible future states, including those reached under the worst-case uncertainty realization. Safety is then determined in terms of whether the FRS under the fallback policy eventually becomes fully contained in the terminal safe set Ω without previously intersecting the failure set F.
3. 方法的优缺点：
   Obtaining the FRS for a predefined fallback policy decouples synthesis from verification, inducing a more tractable computational problem. The downside is that the precomputed policy does not account for the FRS, which can result in conservative filtering and diminished task performance.

#### 3.3.3 Tube MPC

1. 方法的优点：
   Tube-based model predictive control (tube MPC) can be used to compute a local fallback policy via runtime optimization at each control cycle, rather than relying on a precomputed one.
2. 方法的缺点：
   In general, the optimization problem of tube MPC can be computationally intensive, especially for high-dimensional systems and complex constraints.

### 3.4 Data-Driven Safety Filters

1. 应用举例：
   - Recent work has used deep reinforcement learning (RL) with a binary cost c(x, u) := 1{f (x, u, 0) ∈ F}, learning a safety critic that can be seen as a risk monitor (82, 83).
   - Another line of research has pursued approximate solutions to the optimal safety problem encoded in Equation 9 (40, 6, 38, 39, 5).
   - Closely related to approximating the optimal safety value function, recent efforts aim to learn CBFs from data.
   - Data-driven stability analysis can be used to learn controlled-invariant regions of attraction for safety assurance. The recent stabilize-avoid formulation (91) aims to learn policies that safely drive the state to some equilibrium in a region of interest.
2. 方法的特点：
   Although neural network critics have shown practical utility in value-based monitoring, it must be kept in mind that the corresponding safety filters come with no guarantees. Using statistical generalization theory, probabilistic guarantees can be provided under the assumption that training environments and the deployment conditions are drawn from the same (unknown) distribution (84).

### 3.5 Safety Filters for Multi-Agent Systems

1. 多智能体系统交互的难点：
   - Enforcing safety becomes particularly challenging in interactive settings, as the robot and its peer agents may have coupled dynamics, limited communication capabilities, and conflicting interests.
   - Predominant safety methods for multi-agent systems assume worst-case agent behavior (92), which can lead to the overly conservative decision-making known as the freezing robot problem (19), negatively impacting the robot's ability to complete assigned tasks.
2. 目标：
   Several alternatives have been proposed with the aim of "unfreezing" the robot, to improve task performance without compromising on safety.

#### 3.5.1 Adaptive safety filters

**Key:** To prevent overly conservative robot behavior based on an a priori worst-case assumption, adaptive safety filters dynamically constrain the disturbance set D, modulating the range of admissible peer agent actions, based on environmental conditions or observed agent behavior.

#### 3.5.2 Probabilistic safety filters

**Key:** Another commonly adopted safety method that relaxes the worst-case assumption relies on computing a probabilistically safe control policy.

方法的缺陷：
Ultimately, however, under any such probabilistic approaches, safety can be compromised when other agents take actions that are assigned low probability by the robot's prediction algorithm (the "long tail" of unlikely events, 23).

#### 3.5.3 Filter-aware task policies

1. 核心思想：不将安全和控制性能表现解耦，有时候控制过程中为保证安全的干预会影响控制性能表现，这时可以考虑直接在控制性能价值函数的构造中直接加入安全过滤器(safety filter): Seeking a tighter integration between safety and performance, some efforts have investigated endowing task policies with safety filter awareness. These approaches relax the safety-performance separation paradigm, allowing the robot's task-driven decisions to explicitly account for the safety filter's behavior; the goal is to avoid unnecessarily triggering interventions that may negatively impact performance.

### 3.6 Safety Filters for Imperfect Perception

1. 对于Imperfect Perception的问题描述：The methods discussed thus far rely on the common assumption that the robot has reliable access to an accurate estimate of all relevant state variables. This assumption is increasingly challenged by modern robotic applications. Various forms of imperfect perception, ranging from occlusions to sensor failures can significantly endanger the robot's operation.

2. 对其他智能体的不完全观测和不确定行为意图，提出了在同一个框架下对未来其他智能体的状态和意图进行预测的能力：
   To conclude this section, we point out that safety analysis under imperfect state perception and uncertain agent intent (Section 3.5.3) share a common technical bottleneck, namely enabling the robot to strategically account for its future ability to acquire new information. Future research should focus on developing a single safety analysis framework that unifies those two emerging fields.

## 4. UNIFIED SAFETY FILTER THEORY

**Key:** This section introduces a mathematical formalism that brings a broad class of the safety filters reviewed in this paper under a common lens. The exposed modular structure can be used to reconceptualize a range of well-established safety filters, as well as to guide the construction of new ones. The analysis focuses on robust safety filters for uncertainty d ∈ D, while noting that the concepts and results have analogous probabilistic counterparts.

1. 给Safety Monitor, Safety Filter下定义，并给出了safety filter的统一形式（模块化结构），并将第3章中的4中safety filter用统一形式重新描述。

### 4.1 Safety Value Functions as Control Barrier Functions

1. CBF的优势在于控制信号的干预机制很平滑，劣势在于CBF给出的是安全集的子集并且缺乏通用的构造方法。可以考虑用其他safety filter构造安全集，然后利用CBF的控制信号干预机制：
   Control barrier functions (CBFs) provide a smooth intervention mechanism at the cost of settling for suboptimal safe sets and lacking general synthesis methods. Exploiting the modular structure of safety filters, a promising research direction is to combine CBF-type intervention with other safety approaches that enjoy principled constructive mechanisms. Ongoing research efforts explore the use of the HJ safety value function as a control barrier function.

### 4.2 Offline Neural Synthesis with Runtime Certification

1. 涉及神经网络或RL的方法通常lack guarantees（见笔记3.4方法的特点）。

## 5. DISCUSSION

1. In this review, we have provided a unified perspective on a growing family of task-agnostic tools that filter arbitrary control policies into safe ones, exposing their shared structure and comparing their main features.

2. Future Issues:
   - Safety filters that account for runtime learning
   - Safety filters that account for interaction
   - Safety filters with high-dimensional representations
