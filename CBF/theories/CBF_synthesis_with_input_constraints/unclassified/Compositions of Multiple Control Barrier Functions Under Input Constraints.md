# Compositions of Multiple Control Barrier Functions Under Input Constraints

## Key Points

**开展的工作：**

这篇文章讲了一种缩放/微调手段，对象是一些列针对单一约束已经可行的CBF，如果idea按照我设想的框架，那可以好好看看。
微调后可能仍然存在infeasibility的情况，本文还讲了在控制不变集中挖去不可行点（用采样的方法）来增加CBF约束的方法以满足可行性的手段。

**future work:**
Future work in this area may include robust and sampled-data extensions of this framework, generalizations to other classes of systems, or extensions to relate this algorithm to the maximal viability kernel.

**摘要：**
This paper presents a methodology for ensuring that the composition of multiple Control Barrier Functions (CBFs) always leads to feasible conditions on the control input, even in the presence of input constraints.
This paper addresses this challenge by providing tools to 1) decouple the design of multiple CBFs, so that a CBF can be designed for each constraint function independently of other constraints, and 2) ensure that the set composed from all the CBFs together is a viability domain.

**Key Words：**
无

## 1. INTRODUCTION

**这一部分总结的很好**：（第一段）单约束求CBF的方法已经很多了，（第二段）但是将多个CBF组合起来由于输入约束可能会导致不可行，（第三、四段）现有一些简化处理的假设及现有一些方法的缺点，（第五段）本文的方法与不足。

1. One open challenge in the CBF literature is that most works assume that the viability domain is sufficiently simple to be described by the zero sublevel (or superlevel) set of a single CBF. More complex viability domains could be expressed as the intersection of the zero sublevel sets of multiple CBFs, e.g. when each CBF represents a single obstacle in a cluttered environment. **This is sometimes achieved by taking a smooth [6], nonsmooth [7], or adaptive [8] maximum over several CBFs, or by simply applying multiple CBFs at once in a Quadratic Program (QP) [9], [10].** However, these approaches all assume that one is able to find a collection of CBFs whose CBF sets form a viability domain when intersected, or else the QP could become infeasible, as is illustrated by the two planar constraints in Fig. 1. Finding such a collection of CBFs is a much more challenging problem than finding a single CBF. The authors are not aware of any general algorithms analogous to [1]–[5] for finding several CBFs at once, excepting learning approaches [11], [12], which can only yield probabilistic safety guarantees.
2. The most common strategy to employ multiple CBFs is to assume that all the CBFs act independently of each other [13]–[15]. For example, the CBFs may apply to different states with decoupled input channels [14], [15], or it may be the case that only one CBF acts at a time [13]. The latter is equivalent to assuming that the boundaries of the individual CBF zero sublevel sets, i.e. the CBF zero level sets, do not intersect, as shown in Fig. 2. In this case, the CBFs may be designed in a one-at-a-time fashion using existing algorithms. However, if this does not hold, then the CBFs must be designed all-at-once, or else the intersection of the CBF sets may not be a viability domain.
3. 这篇文章的两个贡献：
   - Compared to prior works, this paper presents two contributions. First, we present a methodology for decoupling the design of multiple CBFs in the presence of prescribed input bounds.
   - Second, we present an iterative algorithm to find a viability domain parameterized by these decoupled CBFs. That is, instead of using zonotopes, [17], [18], polytopes [19], [20], or other parameterized functions [22], [24], [25], this paper expresses viability domains in terms of an intersection of CBF sets. **As each CBF forbids state trajectories from crossing the boundary of its own CBF set**, **our algorithm focuses on verifying Nagumo's condition only at the states where the boundaries of multiple CBF sets intersect**.
4. 本文方法的局限性：
   Note that, compared to [16]–[22], the viability domains resulting from this algorithm will generally be more conservative, as our intent is to enable the use of existing (usually conservative) CBF literature rather than to approximate the maximal viability kernel.

## 2. PRELIMINARIES

### A. Notations

### B. Model

### C. Safety Definitions

### D. Safe Quadratic Program Control

### E. Assumptions and Motivating Example

1. The principal challenge addressed in this paper is the problem of multi-CBF compositions. For this reason, we assume that the single-CBF problem is sufficiently solved.

## 3. METHODOLOGY

### A. When All CBFs are Non-Interfering

1. 主要结论是Theorem 1和Theorem 2.

### B. Modifying the Quadratic Program

1. 在3.1节得到的结论是对安全集内部全有效，这里提出我们只需对安全集边缘有效即可。
2. 对QP目标函数的改进（加缩放项）
![20240125170100](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240125170100.png)

### C. When the CBFs are Interfering

## 4. APPLICATION TO ORIENTATION CONTROL

## 5. CONCLUSION

1. We have presented conditions under which multiple CBFs are guaranteed to be jointly feasible in the presence of prescribed input bounds, while allowing each CBF to be designed in a one-at-a-time fashion under more conservative assumptions on the available control authority.
2. However, even under these assumptions, it is still possible for there to exist points where an optimization-based controller with multiple constraints may become infeasible. Thus, we also introduced an algorithm to iteratively remove such points from the allowable state set using additional CBFs until this set becomes a viability domain and the safe controller is always feasible.
