# Control Barrier Function Based Quadratic Programs for Safety Critical Systems

## Key Points

CBF的开山论文。
The remainder of the paper is organized as follows. Two barrier functions, specifically, reciprocal barrier functions and zeroing barrier functions, are formulated in Sect. II, and are extended to control barrier functions in Sect. III. Quadratic programs that unify control Lyapunov functions and control barrier functions are introduced in section IV. The theory developed in the paper is illustrated on the adaptive cruise control and lane keeping problems in Sect. V, with simulations reported in Sect. VI. Conclusions are provided in Sect. VII.

**摘要和关键字：**

CBF, CLF, QP, Nonlinear control, Safety, Set invariance

this paper develops a methodology that allows safety conditions—expressed as control barrier functions— to be unified with performance objectives—expressed as control Lyapunov functions—in the context of real-time optimizationbased controllers.

## 1. INTRODUCTION

### A. Background

1. Two notions of a barrier function associated with a set C are commonly utilized: one that is unbounded on the set boundary, i.e., B(x) → ∞ as x → ∂C, termed a reciprocal barrier function here, and one that vanishes on the set boundary,h(x) → 0 as x → ∂C, called a zeroing barrier function here.

### B. Contributions

1. The first contribution of this paper is to formulate conditions on the derivative of a (reciprocal or zeroing) barrier function that are minimally restrictive on the interior of C.
2. this perspective allows for the consideration of multiple control objectives (expressed via multiple CLFs) together with forceand torque-based constraints.

### C. Organization and Notation

## 2. RECIPROCAL AND ZEROING BARRIER FUNCTIONS

### A. Reciprocal Barrier Functions

### B. Zeroing Barrier Functions

1. Intrinsic to the notion of RBF is the fact, formalized in (10), that such a function tends to plus infinity as its argument approaches the boundary of C. Unbounded function values, however, may be undesirable when real-time/embedded implementations are considered. Motivated by this and the barrier certificates in [18], we study a barrier function that vanishes on the boundary of the set C.
2. Proposition 2. Let h : D → R be a continuously differentiable function defined on an open set D ⊆ Rn. If h is a ZBF for the dynamical system (1), then the set C defined by h is asymptotically stable. Moreover, the function VC defined in(20) is a Lyapunov function.
![20231214223007](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231214223007.png)
3. Note that asymptotic stability of C implies forward invariance of C as described in [39].
4. Therefore, existing robustness results in the literature (such as [47], [48]) can be used to characterize the extent to which forward invariance of the set C is robust with respect to different perturbations on the dynamics (1).

### C. Relationships of RBFs, ZBFs and Set Invariance

1. Theorem 1 and Prop. 1 in the two previous subsections show that the existence of a RBF (resp., a ZBF) is a sufficient condition for the forward invariance of Int(C) (resp., C). This section investigates cases where the converse holds and other relations among these two types of barrier functions.
2. Proposition 3. Consider the dynamical system (1) and a nonempty, compact set C defined by (2)-(4) for a continuously differentiable function h. If C is forward invariant, then h|C is a ZBF defined on C.
3. The assumption  ̇h(x) > 0 for all x ∈ ∂C is called contractivity in [45], because the flow on the boundary of C points inward.
![20231215102128](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231215102128.png)

## 3. CONTROL BARRIER FUNCTIONS

### A. Reciprocal Control Barrier Functions

1. When the set Int(C) is not forward invariant under the natural dynamics of the system,  ̇x = f (x), how can a controller be specified that will ensure the invariance of Int(C).

### B. Zeroing Control Barrier Functions

### C. Higher Relative Degree

1. In the preceding two subsections, if the function h has a relative degree greater than 1, then Lg h = 0 and the setKrcbf (x) or Kzcbf (x) trivially equals to U or the empty set.
2. Another means to construct RCBFs for h with relative degree r ≥ 2 is given in [49], where a backstepping-inspired method for its construction is provided.

## 4. QPS FOR MEDIATING SAFETY AND PERFORMANCE

### A. Control Lyapunov Functions

### B. Combining CLFs and CBFs via QP

1. A distinct advantage of the QP perspective is that it allows for the unification of control performance objectives (represented by CLFs) subject to the trajectories belonging to desired "safe" sets (as dictated by CBFs).
2. 控制量u*的Lipschitz continuity:
   **Theorem 3.** Suppose that the following functions are all locally Lipschitz: the vector fields f and g in the control system(21), the gradients of the RCBF B and CLF V , as well as the cost function terms H(x) and F (x) in (CLF-CBF QP). Suppose furthermore that the relative degree one condition,Lg B(x) 6 = 0 for all x ∈ Int(C), holds. Then the solution,u∗(x), of (CLF-CBF QP) is locally Lipschitz continuous forx ∈ Int(C). Moreover, a closed-form expression can be given for u∗(x).

## 5. TWO AUTOMOTIVE SAFETY PROBLEMS VIA QPS

### A. Adaptive Cruise Control Via QPs

1. The cost function in the QP is selected in view of achieving the control objective encoded in the CLF, i.e., achieving the desired speed, subject to balancing the relaxation factors that ensure solvability and continuity of (ACC QP).

### B. Lane Keeping Via QPs

## 6. SIMULATION RESULTS

### A. Simulation results for ACC

### B. Comparison of two QPs

### C. Comparison of RCBFs and ZCBFs

### D. LK simulation

## 7. CONCLUSIONS
