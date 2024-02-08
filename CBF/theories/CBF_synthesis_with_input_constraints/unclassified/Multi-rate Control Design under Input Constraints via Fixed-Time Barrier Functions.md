# Multi-rate Control Design under Input Constraints via Fixed-Time Barrier Functions

## Key Points

**开展的工作：**

- 这篇文章，如果研究periodic safety(where the system trajectories are required to remain in a safe set for all times and visit a subset of this safe set periodically)这个问题的话可以再来读读他是如何设计CBF的，文中的方法没有对CBF中输入约束进行处理，所以存在feasibility的问题。
- 不同更新频率的控制器合成设计值得参考，上层MPC planner用于规划更新频率低，得到一个时间段内的参考控制信号，下层QP controller用于实时控制更新频率高，得到一个实时的修正控制信号，两者合在一起构成最终的输入信号，且MPC使用的模型不是原仿射控制模型，而是在原点处线性化后的LTI model（可能是因为计算效率高？），控制信号是二者控制量的叠加，这个和有参考输入的QP修正不同。
![20240205163350](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240205163350.png)

**future work:**
Future work includes studying the robustness properties of the proposed framework by considering model uncertainties.

**摘要：**

- In this paper, we introduce the notion of periodic safety, which requires that the system trajectories periodically visit a subset of a forward-invariant safe set, and utilize it in a multi-rate framework where a high-level planner generates a reference trajectory that is tracked by a low-level controller under input constraints. We introduce the notion of fixed-time barrier functions which is leveraged by the proposed low-level controller in a quadratic programming framework.

**Key Words：**
无

## 1. INDRODUCTION

1. Constraints requiring the system trajectories to evolve in some safe set at all times while visiting some goal set(s) are common in safety-critical applications.
2. Constraints pertaining to the convergence of the trajectories to certain sets within a fixed time often appear in time-critical applications, e.g., when a task must be completed within a given time interval.
3. Fixed-time stability (FxTS) [6] is a stronger notion of stability, where the time of convergence does not depend on the initial conditions.
4. QP框架有带来短视问题：myopic control synthesis approaches relying solely on QPs are susceptible to infeasibility. 解决办法：To circumvent this issue, combining a high-level planner with a low-level controller has become a popular approach.
5. In this work, we introduce the notion of periodic safety where the system trajectories are required to remain in a safe set for all times and visit a subset of this safe set periodically.
6. 对multi-rate control framework的解释：the low-level controller and the high-level planner operate at different frequencies
7. 本论文的两大贡献：
   - First, we combine the concepts of fixed-time stable Lyapunov functions [5] and control barrier functions [1] to define the notion of fixed-time barrier functions.
   - Second, we design the constraints of the MPC problem to consider this region of attraction of the lowlevel controller in the high-level planner.

## 2. PROBLEM FORMULATION

1. Periodic safety的概念
2. Fixed-Time Domain of Attraction (FxT-DoA)的概念
3. fixed-time barrier functions(FxT barrier function)的概念
4. In particular, existence of a FxT barrier function h implies: 1) forward invariance of the set DS and 2) convergence to the set S within time TS .

## 3. MULTI-RATE CONTROL

这一章节没有提到如何处理CBF的输入控制约束，会带来是否可行的问题
![20240205152811](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240205152811.png)

1. In this section, we present a hierarchical strategy where we first design a high-level planner that generates a reference trajectory z(t), and then, a low-level controller that tracks this reference trajectory to guarantee that the closed-loop trajectoryx(t) satisfies (3).

### A. High-level planning

设计MPC上层规划控制器，每隔T时间计算一次

1. The matrices (A, B) are known and, in practice, may be computed by linearizing the system dynamics (1) about the equilibrium point, i.e., the origin.
2. The MPC problem is solved at 1/T Hertz and therefore the reference high-level input is piecewise constant.

### B. Low-level control synthesis

设计QP下层控制器，每个仿真时间步计算一次

## 4. CLOSED-LOOP PROPERTIES

1. In this section we show the properties of the proposed multirate control architecture.
   - A. First, we show in Lemma 1 that under the low-level controller ul, the set Di is FxT-DoA for the set Ci, so that starting from any x((i − 1)T ) ∈ Di, the closed-loop trajectories reach the set Ci within time T.
   - B. Next, in Theorem 1 we show recursive feasibility of the MPC so that the closed-loop trajectories satisfy x((i −1)T ) ∈ Di for all i ∈ N, which along with item A, implies that the closed-loop trajectories satisfy (3).

### A. Fixed Time Domain of Attraction

1. In this section, we show that under the low-level controller defined as the optimal solution of the QP (19), the set Di is a FxT-DoA for the set Ci.
2. 这一句就说明了该文没有对输入约束进行处理，可能会有可行性的问题：
   To this end, it is essential that the QP (19) is feasible for all x so that the low-level controller is well-defined. The slack term δ ensures the feasibility of the 4QP (19) for all x /∈ ∂Ci.

### B. MPC Recursive Feasibility and Closed-Loop Constraint Satisfaction

## 5. SIMULATIONS

## 6. CONCLUSIONS
