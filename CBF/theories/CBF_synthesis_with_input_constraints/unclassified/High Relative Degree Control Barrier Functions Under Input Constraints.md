# High Relative Degree Control Barrier Functions Under Input Constraints

## Key Points

**开展的工作：**

- 设计了两种考虑输入约束的CBF合成方法，都是针对high-relative-degree的情况，第一种有点类似于仿真的方法，第二种是先定义了一个假设，然后通过仿真得到一个valid CBF（在r=2时不用仿真可以得到一个解析解）。
- 这篇文章有研究两方面内容时可以参考：一方面是high-relative-degree CBF合成，另一方面是通过仿真方法得到CBF。

**future work:**
Future work includes extending this formulation to guarantee feasibility of more complex objectives and unsafe sets, in particular, environments with strong central gravity, and comparing the efficiency of online approaches to optimal planned paths.

**摘要：**

- This paper presents methodologies for ensuring forward invariance of sublevel sets of constraint functions with high-relative-degree with respect to the system dynamics and in the presence of input constraints.
- We show that such constraint functions can be converted into special Zeroing Control Barrier Functions (ZCBFs), which, by construction, generate sufficient conditions for rendering the state always inside a sublevel set of the constraint function in the presence of input constraints.

**Key Words：**
Control barrier function, Constrained control, Quadratic programming, Aerospace

## 1. INDRODUCTION

1. 提出问题：However, the problem of designing CBFs for high-relative-degree (r ≥ 2) constraint functions under control input constraints remains an open question except for specific systems [1]–[4]. In this paper, we seek to generalize these results, and in particular the methods in [4]–[6], to a wider class of systems.
2. 这段话可以好好体会下：
   If the constraint function is of relativedegree r = 1 with respect to the system dynamics, then the set can be rendered forward invariant if the constraint function is also a CBF [2]. For control-affine dynamics, this leads to an affine condition on the control input, which can be applied pointwise to yield either explicit control laws [1], or optimization-based control laws [2], [7]–[9] that render the safe set forward invariant. However, if the constraint function is of relative-degree r ≥ 2 and the uncontrolled dynamics allow trajectories to leave the safe set, then the constraint function alone cannot be a CBF. To recover such a control-affine condition, we seek to construct CBFs that are composed of the constraint function and its derivatives, and whose sublevel sets are subsets of the safe set.
3. 目前将high-relative-degree constraint functions变成CBF的方法与其对应的文献：
   Several papers develop methods to convert high-relativedegree constraint functions (r ≥ 2) into CBFs, including using compositions with bounded monotonic functions [2], backstepping [7], feedback linearization and pole placement [8], [10], or by defining safe sets for every order of derivative of the constraint function [9]. The approach in [5] bypasses the creation of a new CBF, but develops a condition on the first controllable derivative that fills the same role as the conditions in [7], [8].
   这些方法存在的问题：没有考虑输入约束
   All these approaches lead to conditions on the control input that are potentially infeasible if the set of valid control inputs is bounded.
4. 目前已有很多针对特定系统构建满足输入约束的CBF的方法，也有研究更平常系统的文献：
   Conditions for safety under input constraints for the nintegrator system are introduced in [4]. For certain other systems, a second CBF that guarantees satisfaction of control input constraints for all future times can also be introduced [2], [3]. For more general systems, [6], [11] recently developed an approach (not specific to high-relative-degree) wherein a small known backup set is expanded to the set of states which can reach the backup set in a finite time horizon under input constraints. The work in [12] is similar to [6], [11], but generalizes the approach to infinite time horizon.
5. 本篇论文主要开展的工作：
   - This paper addresses the problem of designing CBFs for high-relative-degree constraint functions with guaranteed safety under input constraints for a broader class of systems than in [1]–[4], [6], [11] using extensions to the approach in [12].
   - We introduce two strategies for generating CBFs that by construction can be rendered nonpositive in the presence of input constraints.
   - The first strategy uses a predefined nominal control law similar to [6], [11], [12], but does not require a predefined backup set (as in [6], [11]), and does not require the searched time horizon to contain a unique maximizer of the constraint function (as in [12]).
   - The second strategy simplifies the first and generalizes [4] to any system for which there exists a minimum control authority over the rth derivative of the constraint function everywhere in the safe set.
   - Similar to [9], the resultant controlled forward invariant sets are subsets of the safe set, and could be smaller or larger than the corresponding sets obtained in [9]. However, unlike [9], these methods by construction respect input constraints without tuning other parameters of the CBF.

## 2. PRELIMINARIES

### A. Notation

### B. Model and Problem Formulation

1. 对relative-degree r的定义：Definition 1.
2. Note that Definition 2 can be relaxed if h is only differentiable [13, Thm. 2.1], and Lemma 1 can be extended to non-Lipschitz controllers if (1) admits a unique solution [14].

## 3. METHODOLOGIES

### A. General Case

1. 将状态约束的导数比作generalized inertia, by analogy to inertia in kinematic systems.
2. To ensure safety when r ≥ 2, a controller must be able to dissipate this generalized inertia, i.e. ensure h(k)(x(t)) ≤0, ∀k ≤ r for all t such that h(x(t)) = 0.
3. 这个方法有点像前向仿真的方法，只不过不是对所有可能得控制输入都进行仿真不现实，所以选择一种最能保证安全的方法（文中就给了一种相对保守的方法）来进行仿真。
![20240208170256](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240208170256.png)
4. 这种前向仿真方法的main result，得到的是一个valid CBF且满足输入约束:
![20240208170846](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240208170846.png)
5. 这种方法的优劣：
   While Theorem 1 theoretically applies to any system for which a nonempty SH exists, in practice, it may be limited by the requirement to propose a "good" u∗ (i.e. one which yields a large SH ). Also, for most systems, H(x), ∂ψh∂x will not have explicit expressions. That said, computing H(x), ∂ψh∂xonly requires propagating two ODEs, which can be done efficiently. On the other hand, the advantage of this approach is that if H(x(0)) ≤ 0, then one immediately knows SH can be rendered forward invariant under the input constraints.
6. 第二种方法避开了计算几个比较复杂的公式，但是得到CBF的方法不一样
   Next, we present an alternative approach that avoids the complexity of (13)-(15) but yields a different SH .

### B. Special Case of Constant Control Authority

1. Instead of allowing for any u∗ satisfying Assumptions 1-2, which could make (6) difficult to compute, in this section, we set the control input so as to regulate the system to a constant rate of generalized inertia dissipation. That is, choose any usuch that h(r)(x, u) is a predefined constant.
2. 假设h(x)的r阶导是一个预先定义的常数：That is, choose any u such that h(r)(x, u) is a predefined constant.然后通过仿真得到valid CBF（在r=2时不用仿真可以得到一个解析解）。
3. B中方法相比与A中方法在计算效率上的优势：but t′c(x) is computed via polynomial root-finding rather than ODE propagation, making (24) easier to compute than (13)-(15) when implementing condition (4).

## 4. CASE STUDY FOR SPACECRAFT APPLICATION

## 5. CONCLUSIONS
