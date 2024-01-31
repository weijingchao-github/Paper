# Safety Verification and Controller Synthesis for Systems with Input Constraints

## Key Points

**开展的工作：**

- 利用一系列的SoS迭代步骤同时合成CBC和控制器
    1. 初始化控制器和CBC
        ![20240122210037](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240122210037.png)
        ![20240122210133](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240122210133.png)
    2. 更新控制器
        ![20240122210303](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240122210303.png)
    3. 更新CBC
        ![20240122210404](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240122210404.png)
    4. 更新中间多项式λk1
        ![20240122210515](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240122210515.png)
- 方法的优势：合成CBC而不是CBF，CBC只对安全集边界有控制约束，安全集内部没有控制约束，因而相对来说没那么保守。
- 方法的缺陷：好像迭代中没有控制器提升步骤；更新λk1和λk2好像没有什么意义（λk1可能有点意义但是λk2可能真没什么意义）。
- 方法特点：扩大安全集的方法We introduce additional constraints B(x)−σenlBk−1(x) ∈ Σ[x] to enlarge the volume of the control invariant set Bk by enforcing Bk−1 ⊆ Bk.
- 方法效果：CBF得到的安全集是CBC安全集的子集。

**future work:**
In the future we aim at extending the formulation to discrete time systems.

**摘要：**
Unlike the related control Barrier functions approach, **our formulation only considers the vector field within the tangent cone of the zero level set defined by the certificates（只考虑安全集边缘）**, and is shown to be less conservative by means of numerical evidence.
For polynomial systems with semi-algebraic initial and safe sets, CBCs and safe control laws can be synthesized using sum-of-squares decomposition and semi-definite programming.

**Key Words：**
无

## 1. INTRODUCTION

1. 关于CBF目前表示保守性的描述：
   Direct numerical synthesis approaches by sum-of-squares programming [19], [11], machine learning [20], and deep learning [21] have been proposed. All these methods, either via convex optimisation, or learning techniques, consider the synthesis of a CBF with a relaxation term included in the synthesis procedure. From the standpoint of control invariant sets, it is guaranteed that there exists a class-K relaxation term to bound the safety variation, but imposing such a term at every point inside the set during the control synthesis introduces conservativeness. Abandoned this term during the synthesis process has been considered in [22], and using Positivstellensatz, a weaker condition on invariance is imposed for systems without input limits.
2. 本文对象和方法：
   For systems with polynomial dynamics and semi-algebraic safe and initial sets, we use sumof-squares programming and the generalised S-procedure to synthesize a CBC, as well as a Lipschitz continuous safe control law which fulfills the actuation constraints.

## 2. CONTROL BARRIER CERTIFICATES

1. 现有的工作没有考虑CBF和控制器一起合成的问题，（本文的方法）仅要求不变集边界的安全性（从而降低保守性）
   Existing work on Barrier certificates synthesis either limits the analysis to noisy autonomous systems, or tries to design a control law in an online quadratic programming framework. There is no work focusing on combining Barrier certificates construction with controller design, which only requires safety on the boundary of the invariant set.

### A. Control Barrier Certificates Formulation

1. Control Reachable Set, Control Invariant Set, Safety, Control Barrier Certificates的概念。
2. Control Barrier Certificates(CBC)的定义和证明值得好好看看，它与CBF不同的是只在安全集边界有CBF限制。
![20240122161419](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20240122161419.png)
3. We note here the formulation (5) is different from that of CBF based QP. Here, in the interior of the control invariant set B, the solution of (5) is the direct projection from u∗(x) on the control admissible set U.

## 3. COMPUTATION METHOD

### A. SOS for CBC Synthesis

1. 构造的是多项式CBC和多项式控制输入。
2. The small positive real scalars ǫ1, ǫ2 ensure strict inequality for (3a) and (3c).
3. We note that in Theorem 2 we only require a polynomial multiplier λ, but not a SOS one since the condition∂B(x)∂x (f (x) + g(x)u(x)) ≥ 0 is only imposed on the boundary B(x) = 0.
4. Here, like existing work of using SOS to synthesize Barrier certificates, we use an iterative procedure for control Barrier certificate synthesis and safe control law design.
5. We introduce additional constraints B(x)−σenlBk−1(x) ∈ Σ[x] to enlarge the volume of the control invariant set Bk by enforcingBk−1 ⊆ Bk.

## 4. SIMULATION RESULTS AND DISCUSSION

### A. Nonlinear Control Affine Systems

**这一章分析了CBC得到的安全集为什么比CBF得到的安全集范围大，值得重视**

1. CBF得到的安全集是CBC安全集的子集：
   Actually we have B2 ⊂ B1, which is proved by there exists a SOS multiplier σ, such that B1(x) − σB2(x) ∈ Σ[x].
   原因：The reason is that, we trivially have σcbf + α ∈ R[x]. A larger search area enables us to find a larger control invariant set. On the other hand, the additional term λ1B1(x) can be regarded as an adapted relaxation term compared with a fixed class-K function used in CBF approach. By using a zeroth order base for the polynomial multiplier λ1 and expanding the definition domain of CBF to the whole real space, our formulation is equivalent to CBF. Higher order basis selections hereby reduce conservativeness.
2. 从relaxation coefficient λ1 and α的角度分析了为什么CBF相对于CBC更加保守。

### B. LTI Systems

### C. Comparison with Control Barrier Functions

1. CBF方法相比于CBC比较保守的一个原因：
   For the case where the control invariant set is constructed a priori, although the CBF approach endows Lipschitz continuity for the resulting controller, it also introduces unnecessary conservativeness since  ̇B2(x) is bounded by a fixed additional relaxation term. Although there are existing works propose to tune the relaxation coefficientα online [14], additional computational complexity and necessary cost trade-off are also introduced.
2. Our approach (5), on the other hand, is less restricted with an adapted relaxation coefficient λ1. For systems with mode switching such as power systems, formulation (5) ensures safety.
3. CBC相比于CBF还有一个特点就是CBC没有定义安全集之外的控制约束，也就没有了CBF所拥有的“吸引力”。

## 5. CONCLUSION

1. We prove that the existence of a control invariant set inside the safe region is sufficient for safety of nonlinear control systems. The formulation only imposes boundary conditions, thus alleviating conservatism.
2. For polynomial systems with semi-algebraic initial and safe sets, we propose an iterative procedure with using SOS program to synthesize the CBC with encoding general affine control limits. We also show that CBC has less conservativeness compared with CBF from numerical simulations. In the future we aim at extending the formulation to discrete time systems.
