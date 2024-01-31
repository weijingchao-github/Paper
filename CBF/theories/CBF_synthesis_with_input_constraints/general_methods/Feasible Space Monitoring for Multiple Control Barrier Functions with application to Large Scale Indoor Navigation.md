# Feasible Space Monitoring for Multiple Control Barrier Functions with application to Large Scale Indoor Navigation

## Key Points

**safety filter:**

- safety monitor: handmake->Boolean logic->combine multiple to one: method from 3.COMPLEX SAFETY SPECIFICATIONS中的C.Single CBF for Arbitrary Safe Set Compositions
![20231201170302](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231201170302.png)

- intervention scheme: QP
![20231201170335](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231201170335.png)

- task policy
- fallback policy

**开展的工作：**
In this letter, we propose a framework to capture complex safety specifications by CBFs. We combine multiple safety constraints via Boolean logic, and propose an algorithmic way to establish a single CBF for nontrivial safety specifications. Our method leverages both the Boolean logic from [7] and the smooth combination idea from [11], while merging the benefits of these approaches.
对于多CBF约束问题，介绍了一种简单实用的方法，利用多CBF安全集的交并关系（有点像集合论），将多个CBF约束平滑的合成一个CBF约束。

**future work:**
无

**对象：**
二维图形（例子中用的二维矩形）

**仿真工具：**
MATLAB

**使用或开源的数据集：**
无

**是否开源：**
是，网址：<https://github.com/molnartamasg/CBFs-for-complex-safety-specs>

**摘要：**
We quantify the feasible solution space of the QP in terms of its volume. We introduce a novel feasible space volume monitoring control barrier function that promotes compatibility of barrier functions and, hence, existence of a solution at all times. We show empirically that our approach not only enhances feasibility but also exhibits reduced sensitivity to changes in the hyperparameters such as gains of nominal controller.

**Key Words：**
无

## 1. INTRODUCTION

1. Designing a safety-critical robot motion stack for ensuring the satisfaction of multiple, possibly time-dependent, state and input constraints is an active area of research.
2. In this work, we analyze the conditions under which a controller with multiple CBF constraints admit a solution for all time, a property we call persistent feasibility. At a given state and time, we quantify the feasible control input space defined by CBF constraints and input bounds in terms of its volume, and introduce a novel feasible-space control barrier function (FS-CBF) that restricts the rate-ofchange of the volume of the feasible space.
3. Existence of an FSCBF is shown to be a necessary and sufficient condition for enforcing compatibility of multiple CBFs.
4. This work, to the best of our knowledge, is the first to consider an optimization problem's feasible solution space volume and its gradient in control design.

## 2. NOTATION

## 3. SYSTEM DESCRIPTION

## 4. PROBLEM FORMULATION

1. Feasible CBF Space
![20240120102541](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240120102541.png)
2. 问题描述
Consider the dynamical system (1) subject toN barrier function constraints hi(t, x) ≥ 0 where eachhi, defined in (2), is a CBF with class-K function αi for the set Si respectively. If for the initial state x0 ∈ Rn,Uc(0, x0) ̸ = ∅, design a controller π that renders the CBFshi, i ∈ {1, .., N } persistently feasible, that is, Uc(t, x) ̸ = 0, ∀t > 0.

## 5. FEASIBLE VOLUME CONTROL BARRIER FUNCTION

### A. Polytope Volume Estimation

1. polytope volume预测方法：Monte Carlo, Chebyshev Ball of a Polytope, Inscribing Ellipsoid

### B. Polytope Volume Gradients

1. The sphere and ellipsoid on the other hand are computed using convex programs and, therefore, we can exploit sensitivity analysis [22] to compute the gradients of their volume w.r.t the polytope matrices A, b. Libraries like cvxpy [23] readily provide interface to differentiate through convex programs.
2. 本文作出的假设：
![20240120111533](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240120111533.png)
polytope的体积有可能是不可微的However, we note that the volume of the polytope as well as its inscribing sphere and ellipsoid are non-differentiable quantities.关于不可微的情况作者leave the non-smooth analysis to future work.
3. 未来可开展的工作：
   In practice, we may encounter states at which the volume is non-differentiable w.r.t matrices A, b. Cvxpy returns heuristic gradient values at points of nondifferentiability and we employ these in our implementations. In experiments, we did not observe any negative effects of this approximation, but a more formal non-smooth control theoretic analysis and consideration of generalized gradients, similar to non-smooth CBFs[2], [24] is left for future work.

### C. Polytope Volume barrier function


