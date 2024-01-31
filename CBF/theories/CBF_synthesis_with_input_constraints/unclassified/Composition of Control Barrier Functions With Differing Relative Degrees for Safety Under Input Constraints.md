# Composition of Control Barrier Functions With Differing Relative Degrees for Safety Under Input Constraints

## Key Points

**开展的工作：**
![20240127190820](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240127190820.png)
摘要里基本上都提到了：为解决input constraints，构建控制动力学系统，原系统的输入是控制动力学系统状态的函数，将状态约束和输入约束不管各约束是多少relative degree，都可以用soft-minimum composite方法组合成一个CBF，这个CBF既满足状态约束又满足输入约束。

这篇文章还有好多没有看懂的地方，方法的优点在于用平滑函数组合多个状态约束和输入约束，且可以将不同relative degree的约束组合在一起；问题可能在于要引进一个新的控制动力学系统，且这个系统没有给出构造方法，例子里也是直接给出了这个系统。

**future work:**
Currently, our approach applies to systems with continuous dynamics. Future work could extend it to hybrid systems with rigid contacts by leveraging ideas from [24].

**摘要：**

- This paper presents a new approach for guaranteed safety subject to input constraints (e.g., actuator limits) using a composition of multiple control barrier functions (CBFs).
- First, we present a method for constructing a single CBF from multiple CBFs, which can have different relative degrees. This construction relies on a soft minimum function and yields a CBF whose 0-superlevel set is a subset of the union of the 0-superlevel sets of all the CBFs used in the construction.
- Next, we extend the approach to systems with input constraints. Specifically, we introduce control dynamics that allow us to express the input constraints as CBFs in the closed-loop state (i.e., the state of the system and the controller). The CBFs constructed from input constraints do not have the same relative degree as the safety constraints. Thus, the composite soft-minimum CBF construction is used to combine the input-constraint CBFs with the safety-constraint CBFs.
- Finally, we present a feasible real-time-optimization control that guarantees that the state remains in the 0-superlevel set of the composite soft-minimum CBF.

**Key Words：**
无

## 1. INDRODUCTION

**这篇文章的Introduction介绍的非常好，综述了很多合成CBF with input constraints的方法**

验证一个candidate CBF是真正的CBF是很困难的

1. Nevertheless, verifying a candidate CBF (i.e., confirming that it satisfies the conditions to be a CBF) can be challenging [11].
2. For systems without input constraints (e.g., actuator limits), a candidate CBF can often be verified provided that it satisfies certain structural assumptions (e.g., constant relative degree). In contrast, verifying a candidate CBF under input constraints can be challenging, and this challenge is exacerbated in the case where the desired forward invariant set (e.g., the safe set) is described using multiple CBFs. Offline sum-of-squares optimization methods can be used to verify a candidate CBF [12]–[15]. Alternatively, valid CBFs can be synthesized offline by griding the state space [16].
3. 第3，4段综述了很多合成CBF with input constraints的方法。
4. 本文开展的工作：第5，6段。

## 2. NOTATION

1. Throughout this paper, we assume that all functions are sufficiently smooth such that all derivatives that we write exist and are continuous.

## 3. COMPOSITE SOFT-MINIMUM CBF

### A. Problem Formulation

### B. Composite Soft-Minimum CBF Construction and Control

这一节讲如何将多个可以有不同relative degree的CBF组合成一个CBF，用的soft minimum进行组合，组合得到的CBF相较于安全约束保守，方法可以称为composite soft-minimum法。这种方法加了很多充分条件，即有一些限制才能用。

1. 公式(10)搞不明白为什么要加一个松弛项。

## 4. GUARANTEED SAFETY WITH INPUT CONSTRAINTS

### A. Problem Formulation

### B. Control for Safety with Input Constraints

1. 将原系统的输入看作控制动力学系统的状态反馈函数
![20240127162545](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240127162545.png)
2. 把系统动力学和控制动力学级联起来，这样状态约束和输入约束能直接罗列在一起了
![20240127165428](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240127165428.png)
3. 级联起两个动力学方程和状态约束后，可以用上一章的composite soft-minimum法进行组合。
   Since Proposition 1 implies that the cascade (28) with the CBFs (29) satisfy (A1) and (A2), it follows that the composite soft-minimum CBF construction from the previous section can be applied to combine the CBFs (29) that describe a set Ss = ˆSs × Sc that combines the safe set ˆSs and the set of controller states Sc that yield control signals in the admissible set U. In other words, we can apply the composite soft-minimum CBF construction to enforce safety and input constraints.
4. Control architecture that uses the composite soft-minimum CBF h
![20240127190820](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240127190820.png)

## APPENDIX I_ RELATIVE DEGREE OF A NONLINEAR CASCADE
