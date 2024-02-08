# Robust Control Barrier Functions under High Relative Degree and Input Constraints for Satellite Trajectories

## Key Points

**开展的工作：**

- 在不同条件的假设和设定下，提出了3种满足输入约束条件的RCBF合成公式，3种合成公式分别对应着不同的假设：We have presented three forms for RCBFs for relative degree 2 systems that constructively consider input constraints and disturbance bounds to ensure the RCBF condition is always feasible in the presence of input constraints.结果是Thus, systems meeting the theorem requirements are guaranteed to have safe closed-loop trajectories despite the input constraints and disturbances.
- 提出了一种磁滞开关方法来使RCBF减少对安全集内部很里面的状态对输入量的限制与约束（方法效果介于CBF和CBC之间），对应着讲了一种class-K func和开关界限的设计方法：We also introduced a switching approach for enforcing the RCBF condition only near the boundary of the inner safe set, and a class-K-like function that allows us to predict how close the state will approach the boundary of this set as a function of the disturbance.（可以从这一节参考下class-K func的设计，和磁滞开关的设计相匹配）
- 仿真验证

**future work:**
In the future, we are interested in how these RCBFs may be used as constraints in path planning methods for potentially more fuel-efficient trajectories or underactuated systems, and as constraints for scalable multi-agent safe trajectory design.

**摘要：**

- This paper presents methodologies for constructing Control Barrier Functions (CBFs) for nonlinear, control-affine systems, in the presence of input constraints and bounded disturbances.
- More specifically, given a constraint function with high-relativedegree with respect to the system dynamics, the paper considers three methodologies, two for relative-degree 2 and one for higher relative-degrees, for creating CBFs whose zero sublevel sets are subsets of the constraint function's zero sublevel set. Three special forms of Robust CBFs (RCBFs) are developed as functions of the input constraints, system dynamics, and disturbance bounds, such that the resultant RCBF condition on the control input is always feasible for states in the RCBF zero sublevel set.
- The RCBF condition is then enforced in a switched fashion, which allows the system to operate safely without enforcing the RCBF condition when far from the safe set boundary and allows tuning of how closely trajectories approach the safe set boundary.

**Key Words：**
Control barrier function, Constrained control, Quadratic programming, Aerospace

## 1. INDRODUCTION

1. While our focus is on spacecraft, the following results are broadly applicable to systems with constraints of high-relative-degree.
2. Thus, **the main questions of this paper are**: given a constraint function with relative-degree 2 (or higher in Section 3.3) and specified input constraints, 1) how to determine a CBF whose inner safe set is a subset of the safe set and which is valid with respect to the input constraints, and 2) how to ensure invariance of the inner safe set in the presence of bounded disturbances.
3. 现有方法的问题：However, the aforementioned papers all require that the set of allowable control inputs is Rm. Since the constraint function is of high-relative-degree, there may exist states in the safe set from which arbitrarily large control inputs are needed to render the system trajectories within the safe set. Therefore, if the set of allowable control inputs is bounded, there may be no admissible control input that keeps the system trajectories within the safe set, and hence the system could become unsafe.
4. 本文的方法：The results of this paper will similarly specify a subset of the safe set that is controlled forward invariant but, unlike [35], here we use first-order CBFs [2] and we provide three principled methodologies to select the analogue of the parameters in [35] for certain classes of systems (namely, systems satisfying the theorem assumptions in Section 3). These methodologies are based on feedback linearization (distinct from [20]), potential energy functions, and model-predictive safety, respectively.
5. 很多论文它的CBF合成方法是根据应用场景的特点来做的，方法可能不具有通用性。
6. 本文讨论的在扰动环境中的安全性问题的一个设定：Safety under a bounded worst-case disturbance, as is considered in this paper.
7. 现有论文对扰动处理的问题：In all of these papers, it is assumed that the system has sufficient control authority to counteract these disturbances. However, satisfying this assumption is nontrivial, and is a requirement of the methods in Section 3.
8. 本文的一个目标————减少对闭环轨迹的约束，只在安全集边界附近施加安全约束：Finally, one objective of this paper is to place fewer restrictions on closed-loop trajectories by applying safety criteria only near the boundary of the inner safe set. This was accomplished in [28] by designating strict subsets of the safe set termed "performance-critical regions" where safety was guaranteed without enforcing the CBF condition.
9. For systems subject to many CBFs simultaneously, the work in [5,33] simplifies control input calculation in a similar manner by breaking the state space into regions where only a few CBFs are actively applied, though this introduces potential issues with non-uniqueness of system solutions. These issues are fixed in [10] by relaxing the system to a differential inclusion.
10. 本文提出了一种磁滞开关法来relaxes the CBF condition in the interior of the inner safe set while still provably guaranteeing safety in the presence of input constraints：
    Expanding upon these approaches, this paper introduces a hysteresis-switching approach inspired by [10] and [34] that relaxes the CBF condition in the interior of the inner safe set while still provably guaranteeing safety in the presence of input constraints. Such hysteresis-switching removes the need for differential inclusions, and thus prevents chattering control inputs that may not be feasible on real actuators. This switching approach also motivates a special choice for the class-K function that is left as a free tuning parameter in all of the theorems in Section 3. We show in simulation how the proposed choice allows one to directly tune how closely trajectories approach the boundary of the safe set.
11. 这篇文章的主要贡献：
    (1) three strategies for generating CBFs from highrelative-degree constraint functions in the presence of input constraints and bounded matched and unmatched disturbances simultaneously (Section 3); (2) a switching method for relaxing the CBF condition in the interior of the inner safe set and tuning how closely trajectories approach the boundary of the inner safe set (Section 4); and (3) specializations of the above CBFs to deep-space trajectory applications (Section 5).

## 2. Preliminaries

### 2.1 Notation

### 2.2 Model and Problem

### 2.3 Mathematical Background

1. 讲时变CBF的论文（不知道是不是原始论文）：
   [1] LINDEMANN L, DIMAROGONAS D V. Control Barrier Functions for Signal Temporal Logic Tasks[J/OL]. IEEE Control Systems Letters, 2019, 3(1): 96-101.

## 3. Control Barrier Functions for Input Constraints

本章讲了在三种不同状态约束的情况下的CBF合成方法，详见下面两条：

1. the goal of this section is to develop a RCBF H and associated sets SH in (3) and SresH in (4) for dynamics relevant to spacecraft, namely relative-degree 2 dynamics. The primary challenge addressed by all the subsequent methods is that for constraint functions with high-relative degree, the input constraints and disturbances must also be incorporated into the form of the RCBF.
2. The following subsections identify three forms of RCBFs, presented in order of increasing complexity and decreasing conservatism. Each form is developed as a function of h and is applicable under different conditions on the input constraints and disturbances.

### 3.1 Constant Control Authority

1. In this subsection, suppose the constraint function h is of relative-degree r = 2, and has the special property that  ̈h can always be made less than some negative constant. Intuitively, this means that the controller can add/remove "energy" from the system at a constant rate. Then, assuming no disturbances, [6] provides the following form for a CBF.
2. However, even if an amax > 0 does exist, this method can be overly conservative.
3. The following section describes an alternative to Theorem 9 that aims at reducing conservatism, and which further treats certain cases where no amax exists.

### 3.2 Variable Control Authority

1. 3.1节在设定上的局限性：Using the methodology in the prior section, the set SresHonly includes states that can be rendered always insideS by setting  ̈hw equal to a negative constant −amax. For agents with a wide operating range, such as a spacecraft operating at various altitudes, this restriction may result in an overly conservative set SresH , or no such amaxmay exist.
2. 本文的设定：Thus, instead of assuming that  ̈hw is upper bounded by a constant as in (15), suppose it is upper bounded by a known function, denoted φ.
3. Intuitively, the function Φ in (20) is usually a potential field, in which states below a certain potential value are unsafe. One can think of the argument of Φ−1 in (21) as analogous to the sum of potential energy −Φ(h) and kinetic energy1 2  ̇h2w; the inverse of this quantity provides an "effective constraint value" H in the same units as the original constraint h. Using this analogy, Theorem 10 gives a condition for ensuring an agent moving in this potential field never falls below the minimum safe potential threshold.
4. We note that assumptions (15) and (20) may appear to be restrictive assumptions, but are reasonable for many systems.

### 3.3 General Case Control Authority

1. The core idea of this subsection is to propagate the state forward in time using the nominal evading maneuver, and analyze the resultant trajectory for safety.

## 4. Hysteresis-Switched Control Barrier Functions

感觉磁滞开关法介于传统的CBF和CBC之间，通过设定两个开关界限，既保证了在安全集内部不会受Class-K func的过多约束，在靠近安全边界时又可以借助Class-K func的约束让控制量更加平滑，作者也给出了class-K func和磁滞开关界限的参考。

1. This section develops a condition on the control input that establishes set forward invariance similar to Lemma 4, but which places fewer constraints on the system trajectories. The core idea of this section is that, as we will show, the RCBF condition u ∈ μrcbf(t, x) in (8) does not need to be enforced everywhere in SresH to ensure forward invariance of SresH , and we will develop a systematic way to relax the conditions in Lemma 4.
2. Class-K function在安全集边界起作用可以阻止系统进入不安全状态，在安全集内部起作用会带来一定的保守性（可以看作是一个unnecessary constraint）。
3. CBC的安全有效性的证明可以参考Theorem 20：
![20240131185026](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240131185026.png)
4. 目前有对控制量约束平滑切换的研究：
   A related approach for smooth switching based on the value of h rather than H is presented in [28], but this approach requires U = Rm.
5. For practical implementation, it is often desirable to tune a controller to reduce the number of switches of the discrete state, which could cause jumps in the control input that wear out the actuators. 因而作者提出了一种合理选择class-K func的方法（能够预测系统状态将与安全集边界的距离来减少切换）及磁滞切换界限ε1, ε2，并解释说明了为什么这么选择。
![20240131192600](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240131192600.png)
6. Thus, we have proposed a method of regulating safety that allows for switched controllers that mitigate the potentially undesirable constraints following from high relative-degree constraint functions.

## 5. Spacecraft Simulation and Discussion

### 5.1 Spacecraft Dynamics

1. In this section, we apply the previously presented RCBFs and hysteresis-switching strategy to satellite dynamics and demonstrate these approaches in simulation.

### 5.2 Setup for Safety

1. 根据前文推导的4种RCBF合成方法合成了4种RCBF
![20240131200735](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240131200735.png)

### 5.3 Simulations: Ceres

### 5.4 Simulations: Eros

1. 仿真环境是时变的：
   Note that Eros spins with angular velocityω = [3.101(10)−4, 6.232(10)−5, 9.810(10)−5] rad/s [19], so each point is moving and thus the time varying component ∂tH is important in this scenario.

## 6. Conclusions
