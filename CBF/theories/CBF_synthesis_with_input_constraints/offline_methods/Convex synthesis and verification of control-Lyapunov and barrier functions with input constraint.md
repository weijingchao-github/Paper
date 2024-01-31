# Convex synthesis and verification of control-Lyapunov and barrier functions with input constraints

## Key Points

- 利用SoS合成CLF和CBF
![20240122095130](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240122095130.png)
![20240122095150](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240122095150.png)
- 方法的优势：不用在合成CLF/CBF时也要合成控制器，减少了保守性，不会受到只能是多项式控制器的约束。
- 方法的缺陷：先求解得到λ(i)(x)再用它来更新V感觉不合理，因为λ(i)(x)没有什么实际意义。
- 方法特点：也是用了内含椭圆来判断安全集的大小。
- 方法效果：与同时合成控制器的方法比较该方法合成的安全集更大。

**开展的工作：**
In this paper, we derive new necessary and sufficient conditions for CLFs/CBFs for polynomial dynamical systems with input constraints. We formulate these conditions as SOS feasibility problems, and present an iterative algorithm for enlarging an inner approximation of the stabilizable and/or safe region via sequential SOS optimization.

**future work:**
Currently, our approach applies to systems with continuous dynamics. Future work could extend it to hybrid systems with rigid contacts by leveraging ideas from [24].

**摘要：**

- 现有方法的缺陷：
    To certify existence of control actions, current techniques not only design a CLF/CBF, but also a nominal controller. This can make the synthesis task more expensive, and performance estimation more conservative.
- 本文的方法：
    In this work, we characterize polynomial CLFs/CBFs using sum-of-squares conditions, which can be directly certified using convex optimization. This yields a CLF and CBF synthesis technique that does not rely on a nominal controller. We then present algorithms for iteratively enlarging estimates of the stabilizable and safe regions.

**Key Words：**
无

## 1. INTRODUCTION

1. 目前很多文献对CBF和CLF研究存在的问题：
   The CLFs/CBFs are typically synthesized by hand or learned from data [25], [12] without rigorous verification.
   These previous methods either ignore input constraints [29], [10] or rely on the joint synthesis of a nominal control law of polynomial form [16], [19], [1], [32].
   现有SoS规划方法大多是CBF和控制器一起合成，这样做存在的问题：
   - To certify existence of control actions, current techniques not only design a CLF/CBF, but also a nominal controller. This can make the synthesis task more expensive, and performance estimation more conservative.
   - Reliance on this polynomial controller is restrictive if the actual stable/safe control policy is not polynomial. It also limits scalability, as the size of the SOS program increases rapidly with the degree of the controller.
2. 本文方法的概述：
   In this paper, we provide a new synthesis technique with formal guarantees that is conceptually simpler than previous formal methods [16], [19], [1], [32]. In particular, our technique allows one to verify CLFs and CBFs by solving a single convex optimization problem, under the assumption the dynamics are control-affine and the input constraints are polyhedral. This in turn leads to synthesis algorithms based on sequential convex optimization.
3. The basis of our technique is Sum-Of-Squares (SOS) optimization.

## 2. BACKGROUND

**这一节对SoS的基础讲的特别好**

1. In this section we give a brief introduction to Sum-Of-Squares (SOS) techniques for certifying polynomial nonnegativity.
2. Sum-of-squares optimization can also certify polynomial non-negativity on the feasible set of finitely-many polynomial inequalities, i.e., on a semialgebraic set K of the form{x ∈ Rn|b1(x) ≥ 0, . . . , bm(x) ≥ 0}.
3. the preorder of bi
4. the Positivstellensatz
5. The S-procedure（我们常见的形式）
![20240121183334](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240121183334.png)

## 3. PROBLEM FORMULATION

1. we note that through a change of variables, the dynamics of many robotic systems can be written using polynomials

### A. Control Lyapunov Functions (CLFs)

1. Our goal is to find a polynomial CLF V (x) and a scalar ρ that satisfy (7) and maximize (in some sense) the size of theΩρ. In other words, we seek a CLF that yields a large innerapproximation of the stabilizable region.

### B. Control Barrier Functions (CBFs)

1. Our goal is to find a polynomial CBF h(x) with a large certified safe region{x ∈ Rnx |h(x) > 0}.
2. Hence any approach for synthesizing CLFs can be used to synthesize CBFs with slight modification.

## 4. APPROACH

### A. CLF Certification

1. 现有CLF设计技术的问题：
   Current CLF design techniques [16], [19] ensure existence of u by finding an explicit polynomial control policy satisfying (7c). This imposes conservatism, since existence of a CLF does not imply existence of a polynomial controller.
2. Note by taking contrapositive statement, we have replaced the inconvenient ∃ quantifier with the ∀ quantifier, which is easier to work with in an SOS framework. Indeed, as quoted from [30, Chapter 9], "Our sum-of-squares toolkit is wellsuited for addressing questions with the ∀ quantifier over indeterminates. Working with the ∃ quantifier is much more difficult".
3. 提出了利用SoS规划方法验证CLF的Theorem 4.1
   In summary, this theorem shows we can directly certify CLFs using SOS programming. and, unlike [16], [19], this direct certification does not require explicit construction of a polynomial stabilizing control law.

### B. Synthesizing CLFs

### C. Extension to CBFs

## 5. RESULTS

与同时合成控制器的方法比较该方法合成的安全集更大。

## 6. CONCLUSION AND DISCUSSION
