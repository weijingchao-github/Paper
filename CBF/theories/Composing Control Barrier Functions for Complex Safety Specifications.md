# Composing Control Barrier Functions for Complex Safety Specifications

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
In this letter, we propose a framework to describe compositional safety specifications with control barrier functions (CBFs). The specifications are formulated as Boolean compositions of state constraints, and we propose an algorithmic way to create a single continuously differentiable CBF that captures these constraints and enables safety-critical control.

**Key Words：**
无

## 1. INTRODUCTION

1. 研究趋势：多CBF约束下的组合问题
   As the complexity of safety-critical control systems increases, complex combinations of multiple safety constraints tend to arise more frequently, which creates a need for controllers incorporating multiple CBFs.
2. 目前多CBF约束组合的两种方法：直接使用多个CBF作为约束，将多个CBF合成一个作为约束
   The literature contains an abundance of studies on multiple CBFs. Some approaches directly used multiple CBFs in control design. For example, [2], [3] incorporated multiple constraints into optimization-based controllers; [4] synthesized controllers with multiple CBFs that act independently; [5] investigated the compatibility of CBFs; and [6] ensured feasible controllers with multiple CBFs. These works usually linked safety constraints with AND logic: they maintained safety w.r.t. constraint 1 AND constraint 2, etc. Other approaches combined multiple constraints into a single CBF. These include versatile combinations, such as Boolean logic with both AND, OR and negation operations, which was established in [7], [8] by nonsmooth CBFs. Similarly, [9] used Boolean logic to create a smooth CBF restricted to a safe set in the state space; [10] combined CBFs with AND logic via parameter adaptation; while [11], [12] used signal temporal logic to combine CBFs in a smooth manner.
3. 本文的主要工作：
   In this letter, we propose a framework to capture complex safety specifications by CBFs. We combine multiple safety constraints via Boolean logic, and propose an algorithmic way to establish a single CBF for nontrivial safety specifications. Our method leverages both the Boolean logic from [7] and the smooth combination idea from [11], while merging the benefits of these approaches. We address multiple levels of logical compositions of safety constraints, i.e., arbitrary combinations of AND and OR logic, which was not established in [11], while we create a continuously differentiable CBF to avoid discontinuous systems like in [7]. Meanwhile, as opposed to [9], the stability of the resulting safe set is guaranteed.

## 2. CONTROL BARRIER FUNCTIONS

1. CBF-QP的显式解
![20231130214247](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231130214247.png)

### A. Motivation: Multiple CBFs

1. 介绍了直接使用多个CBF作为约束能得到可行解的情况
   这种方法存在的问题：1）多CBF约束下QP可能不存在可行解；->合成一个CBF，尽管安全集可能更保守些，但肯定存在可行解。
2. 通过介绍直接使用多个CBF作为约束求可行解的困难情况，This highlights that multiple CBFs are more challenging to use than a single one.
**思考：**多CBF约束下QP可能不存在可行解是不是这种形式不好，合成一个CBF后能否以原各安全集的交集作为安全集并且求解可行，还是说必须牺牲安全集的范围来换取解的可行性。

## 3. COMPLEX SAFETY SPECIFICATIONS

Now we propose a framework to construct a single CBF that captures complex safety specifications, wherein safety is given by Boolean logical operations between multiple constraints.

### A. Operations Between Sets

1. 不同的 h(x)因为数量级不同，合成一个前要归一化 **（用这个方法的话，这一步很重要）**
   Note that hi may have various physical meanings and orders of magnitude for different i. Thus, for numerical conditioning (especially when we use exponentials later on), one may scale hi to γi ◦ hi with continuously differentiableγi ∈ Ke. For example, γi(r) = tanh(r) scales to the intervalγi(hi(x)) ∈ [−1, 1] that may help numerics.

### B. Smooth Approximations to Construct a Single CBF

While the union and intersection of sets are described by a single function in (17) and (20), the resulting expressions,maxi∈I hi(x) and mini∈I hi(x), may not be continuously differentiable in x [7], thus they are not CBFs. As main result, we propose a CBF by smooth approximations of maxand min, and describe its properties. The CBF will be used to enforce complex safety specifications as a single constraint.

1. Union of Sets
2. Intersection of Sets

### C. Single CBF for Arbitrary Safe Set Compositions

介绍了任意交并组合的统一方法，有点集合论的感觉。

## 4. CONCLUSION

## APPENDIX

对论文中一些定理的证明过程。
