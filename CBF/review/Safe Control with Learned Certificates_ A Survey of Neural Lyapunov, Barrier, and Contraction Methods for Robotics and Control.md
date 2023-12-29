# Safe Control with Learned Certificates: A Survey of Neural Lyapunov, Barrier, and Contraction Methods for Robotics and Control

## Key Points

综述了利用神经网络来合成certificates(CBF, CLF, Contraction Metric)的方法。

- Section II provides the relevant background from control theory, introducing Lyapunov functions, barrier functions, and contraction metric certificates.
- Section III discusses prior, non-neural approaches to certificate synthesis
- Section IV discusses how neural networks can be used to synthesize certificates and their corresponding safe controllers. This section attempts to unify the various synthesis methods presented in the literature, but also includes some historical discussion.
- Section V discusses issues that arise when implementing certificate-based controllers on hardware, and Section VI presents a number of case studies applying these techniques to practical robotic systems, both in simulation and hardware.
- Finally, Sections VII and VIII concludes by discussing some open problems in this area.

**摘要：**
Learning-enabled control systems have demonstrated impressive empirical performance on challenging control problems in robotics, but this performance comes at the cost of reduced transparency and lack of guarantees on the safety or stability of the learned controllers. In recent years, new techniques have emerged to provide these guarantees by learning certificates alongside control policies — these certificates provide concise, data-driven proofs that guarantee the safety and stability of the learned control system. These methods not only allow the user to verify the safety of a learned controller but also provide supervision during training, allowing safety and stability requirements to influence the training process itself.

**开源代码：**
<https://github.com/MIT-REALM/neural_clbf>
<https://github.com/sundw2014/C3M>

## 1. INTRODUCTION

1. MANY desirable properties of dynamical systems, including stability, safety, and robustness to disturbance, can be proven via the use of certificate functions.
2. In recent years, new techniques have emerged for automatically synthesizing certificate functions. For systems with polynomial dynamics, the search for a valid certificate can be framed as a convex semi-definite optimization problem through the use of sum-of-squares (SoS) techniques [6]. Unfortunately, SoS methods are limited to polynomial systems and scale poorly to higher dimensional systems [7]. To address these shortcomings, an emerging body of work in the control theory, machine learning, and robotics communities have employed neural networks to learn approximate certificate functions [8].
3. Unlike traditional approaches to learning for control that search only for a control policy (such as many reinforcement learning, or RL, methods), certificate-based techniques simultaneously search for a control policy and a certificate that proves the soundness of that policy.
4. Unlike traditional approaches to learning for control that search only for a control policy (such as many reinforcement learning, or RL, methods), certificate-based techniques simultaneously search for a control policy and a certificate that proves the soundness of that policy.
5. Our survey includes theoretical discussion of all three common types of control certificate: Lyapunov functions, barrier functions, and contraction metrics. However, reflecting the prevalence of Lyapunov and barrier functions in the literature, our case studies focus mainly on these two types of certificate (readers interested in case studies involving contraction metrics are referred to the tutorial paper by Tsukamoto, Chung, and Slotine [5])

## 2. BACKGROUND

### A. Dynamical systems

### B. Stability and Lyapunov certificates

1. The concept of stability can also be extended to the case where the goal is a set Xg ⊆ X rather than a point, in which case the norm distance between points in the above hierarchy is replaced with distance between a point and Xg.

### C. Safety and barrier certificates

### D. Contraction metric certificates

系统能否跟踪期望路径的性质。

1. In our previous discussion of stability, we assumed that the control system designer is interested in stabilizing the system about a fixed point; however, in many applications we are more interested in trajectory tracking rather than stabilization.
2. Contraction is a property of the closed-loop system, not of any particular trajectory, and thus the existence of a metric satisfying condition (16) suffices to prove that a control system is capable of exponentially stabilizing any dynamically feasible nominal trajectory.
3. A contraction metric proves that the system will exponentially converge to track any feasible reference trajectory. The error ||x(t) − x∗(t)||shrinks exponentially, with transient overshoot limited by the condition number of M and the steady-state tracking error is bounded proportional to the worst-case disturbance.

## 3. PRIOR WORK ON CERTIFICATE SYNTHESIS

1. In this section, we discuss prior work on certificate synthesis methods. We separate this discussion into two parts. First, we cover early methods for certificate synthesis, including **numerical methods, polynomial optimization, and simulation-guided synthesis**. These methods represent an important step in the history of certificate synthesis, but the poor scalability of these early methods, particularly when dealing with nonlinear dynamics, sparked the development of the neural techniques that are the focus of this survey.
2. Of course, neural certificates are not the only class of methods that have evolved to fill this gap. The second part of this section discusses two parallel lines of work, **safe RL and reachability**, that are similar in purpose to neural certificate methods but often use different vocabularies and methods.

### A. Early approaches: numerical solutions and optimization

1. 数值方法、优化方法和仿真引导方法的局限性
   there is currently no generally-applicable scalable framework.
2. 数值方法：给定闭环系统，可以用数值工具求解得到certificates：
   When the dynamics of the closed-loop system are linear and stable,  ̇x = (A − BK)x for feedback gainsK, then a quadratic Lyapunov function will exist of the formV (x) = xT P x for some symmetric positive definite matrixP . In this case, P can be found by solving the continuous Lyapunov equation numerically (most numerical linear algebra packages provide this functionality, including MATLAB [26] and SciPy [27]).
3. SoS方法的局限性：
   Unfortunately, the computational complexity of these techniques grows exponentially in the degree of polynomials involved and they are limited to systems with polynomial dynamics [6]. Additionally, SoS optimization is only convex when searching for either a certificate or a controller; the optimization problem becomes non-convex and often encounters numerical issues when searching for a certificate and controller simultaneously [28].
4. A related technique for certificate synthesis for nonlinear systems is the **simulation-guided synthesis** [31].
5. 这三种方法的局限性：
   Due to the poor scalability of these methods, particularly with regard to nonlinear or high-dimensional dynamics, they have not seen widespread adoption since their introduction (with the notable exception of SoS methods, although substantial concerns remain about the scalability of SoS methods in practice [10]).

### B. Parallel approaches: safe RL and HJ reachability

1. It is important to acknowledge that certificate-based control is not the only line of research that deals with the problem 6of guaranteeing safety and stability for control systems. In particular, safe RL [25] and Hamilton-Jacobi reachability [24] have received a large amount of research interest in recent years.
2. safe RL is a collection of methods that seek to optimize a control policy to achieve good performance on a specified task (i.e. by maximizing some reward) while respecting a number of constraints on the behavior of the controlled system [25]. There are three classes of safe RL methods in particular that highlight connections to certificate-based control.
3. there are also a class of methods for safe control synthesis and verification based on Hamilton-Jacobi (HJ) reachability analysis. HJ methods, which are sometimes also referred to as HamiltonJacobi-Isaacs (HJI) methods to emphasize the connection to game theory, typically frame the safe control problem as a two-player zero-sum game between the controller and an adversary.
4. There are fundamental connections between the HJ value function and certificate functions.
5. Historically, HJ methods have been limited by the complexity of solving the HJI PDE in highdimensional state spaces (which usually requires covering the state space with a discrete mesh of sufficient resolution before iteratively solving the PDE, [24]). However, there has been an exciting trend towards using neural networks to approximate solutions of HJ reachability problems [42], [43], paralleling the use of neural networks for general certificate synthesis, substantially reducing the amount of computation required for HJ analysis.
6. Based on these developments, we anticipate that HJ reachability methods and neural certificates will continue to converge over the coming years, with each community applying insights from the other to develop more scalable and flexible algorithms.

## 4. LEARNING NEURAL CERTIFICATES

1. 将输入转换为状态的函数，系统变成闭环系统，certificates可以验证闭环系统的稳定性和安全性（或直接从CLF, CBF等中获得控制量）：
   All of the certificates discussed above allow the controls engineer to prove that her controller design is sound (or, in the case of CLFs and CBFs, derive a sound controller directly from the certificate).
2. 用自监督学习的方法得到certificates:
   However, these methods share a common drawback: there has historically been no general, scalable method for finding these certificates [1]. In this section, we will discuss how we can apply self-supervised learning to learn these certificates using neural networks (so-called because the algorithm requires no human labeling to supervise its learning; it can generate its own labels).
3. SoS规划可能求不出解的原因：
   the SoS and simulation-guided synthesis methods discussed in Section III restrict V to the span of a chosen set of basis functions (e.g. polynomials of fixed degree), then solve (17) as a convex (or bi-level convex) program. The convexity imposed by a particular choice of V(e.g. the set of polynomials up to a certain degree) makes solving (17) more efficient but can be overly restrictive, resulting in (17) becoming infeasible if V is not rich enough.
4. The neural certificate framework can be seen as a natural extension of this approach by searching over a much richer function space. To avoid the limitations imposed by the choice of function space, V is represented as the space of neural networks of particular depth and width (chosen as hyperparameters by the user). By increasing the size of these networks, this representation can approximate any continuous function [45], [46], alleviating limitations due to the choice of function space. Although this same universal approximation property also applies to polynomials (i.e. a polynomial of large enough degree can also approximate any continuous function on some domain), in practice the scaling for neural networks is much more favorable (the number of parameters in the input layer of a neural network grows with O(nd) with ninput dimensions and d dimensions in the next layer, while the number of monomials in a d-degree polynomial in ndimensions grows with O(nd)).

### A. Remarks on certificate learning

1. Most of certificate theory for continuous-time dynamical systems assumes that the certificate is continuously differentiable, so it is important that continuous-time certificates are learned using networks with continuously-differentiable activation functions such as tanh,softplus, or the exponential linear unit (ELU). In the discrete-time case, Lyapunov and barrier certificates are required only to be continuous [63]; accordingly, works that focus on the discrete-time case have learned certificates using rectified linear unit (ReLU) activation functions, which are continuous but not differentiable at the origin [64].
2. it is important to note that although we frame the certificate-synthesis problem as a feasibility problem in (17), there are several metrics of certificate quality that might be included as an objective for the certificate search.
3. Either objective could be incorporated into the certificate-learning pipeline by adding an appropriately normalized term to the loss function (19), but care should be taken to not allow the neural certificate to overfit to this term at the expense of violating the certificate conditions.

### B. Learning certificates and controllers together

1. 可以只学习ceritificates，也可以certificates和controllers一起学习：
   Learning the certificate alone is useful when a controller is already known and we seek to verify its performance, or in cases when learning a certificate such as a CLF or CBF allows us to derive a controller. When it is necessary to explicitly learn a controller alongside the certificate.

### C. Example: learning a Lyapunov function

### D. Example: learning a CBF

### E. Example: learning a contraction metric

### F. History of certificate learning

1. In addition to different types of certificate, later works have expanded this framework to more challenging problems in control, such as multi-agent control in [11], black-box dynamical models in [67], the RL context in [9], and the robust case in [10]. Many of these later works are particularly notable for providing theoretical and algorithmic contributions to address difficulties that arise in practice

## 5. IMPLEMENTATION CONSIDERATIONS

1. Successfully deploying a control system on hardware is more challenging than demonstrating the performance of that system in simulation. In hardware, effects such as state estimation error, control frequency and delay, external disturbances, unmodeled dynamics, and actuator limits can degrade the safety and stability of the controller unless suitable steps are taken to mitigate these effects. This section will discuss a number of strategies to mitigate these effects.

### A. Mitigating measurement uncertainty

1. Although [76] provides the theoretical basis for barrier certificates that are robust to errors in state estimation, these "measurement-robust" barrier functions are strictly more difficult to synthesize than standard barrier functions (due to the tightening of condition (13)). We are not aware of any published work learning (or otherwise automatically synthesizing) measurement-robust barrier functions

### B. Observation-feedback control certificates

1. In Section V-A, we ask how certificates might be adapted to handle an uncertain state estimate; a natural extension of this question is how certificates might be adapted to the case where the control policy is a function of observations themselves (i.e. observation-feedback or "pixels-to-torques" control).

### C. Robustness to disturbance and model uncertainty

1. The most challenging case of model uncertainty is when there is no a priori knowledge of the structure (e.g. additive, control-dependent, etc.) or extent of the uncertainty. In these cases, the model uncertainty may be estimated from data.

### D. Certificate adaptation

certificates运行时自适应调整。

1. This raises the natural question: instead of trying to be robust to a wide range of possible model errors, could we rely on the nominal model for the bulk of the training process and then transfer the learned certificates to the true model using a smaller amount of data from the real system, thus "adapting" the certificate to the true model?
2. One line of work in certificate adaptation takes inspiration from system identification: if the difference between the nominal and real models can be learned, then certificatebased controllers can adjust for this difference at runtime.
3. Choi, Casten ̃neda,et al. demonstrate that a neural network can be used to learn either the model residue (∆f , ∆u) or the Lie derivative residue(a, b) via reinforcement learning [13] or Gaussian process regression [62].

### E. Certificate verification

验证certificates是否符合要求(valid)，有学习出certificates后进行后验的方法，也有边学习边验证的方法。

1. Several methods for verifying learned certificates have been proposed, each with its own advantages and drawbacks. Here, we will discuss the three most common methods for verification: probabilistic methods based on generalization error bounds, Lipschitz arguments, and optimization-based methods.
2. Third, this after-the-fact verification scheme does little to guide the training process, since it is only used after training is complete (this drawback applies to both Lipschitz arguments and generalization error bounds).
3. The third common category of verification methods, based on optimization, fills this gap by running periodically throughout the training process to verify the certificate as it is learned (and provide feedback in the form of counterexamples where the certificate is not yet valid). These approaches typically take the form of a learner-verifier architecture, sometimes also referred to as counterexample-guided inductive synthesis (CEGIS [8], [49], [3], [64], [50]).
4. As a final note on the topic of verification, it is important to note that control certificates can still be valuable without exhaustive verification, for two reasons. First, even nonverified certificates can act as useful supervision for training control policies [9]. Second, it is possible to deploy a nonverified Lyapunov or barrier certificate safely using a real-time safety monitor. This monitor tracks the rate of change of the certificate and checks whether the derivative condition (4c) (for Lyapunov functions) or (12) (for barrier functions) is violated; any such violation indicates that the certificate is no longer able to guarantee stability or safety and the system should enter a fail-safe mode.

### F. Effects of actuator limits

输入受限在一个集合内，u ∈ U, The only complication is ensuring that this QP will be feasible.

1. A neural certificate architecture can accommodate this constraint through the use of differentiable convex programming [89], which allows back-propagation through a the result of solving a quadratic program like (24).
2. Although solving this optimization problem at training-time incurs an additional offline cost, it enables a learning-enabled controller to provide assurance that it will respect actuation limits at runtime (as contrasted with black-box learned policies such as those derived from reinforcement learning, which make no such guarantees).

### G. Attainable control frequencies

1. In contrast, certificate-based controllers effectively encode long-term system properties (like safety and stability) into local properties of the certificate function; synthesizing a certificate can be seen as compiling long-term behaviors into local properties. As a result, certificate-based controllers need consider only a single-step horizon when evaluating a controller such as (10a). Empirically, this results in at least an order of magnitude increase in attainable control frequency as compared to robust MPC [10].
2. Because a neural certificate control framework shifts the burden of computation to the offline stage (synthesizing the certificate), it is well suited for deployment on robots with limited computational resources or in situations where high control frequencies are required.

## 6. CASE STUDIES

## 7. LIMITATIONS AND FUTURE WORK

In our opinion, certificate-based learning for control has great promise but a number of drawbacks

### A. Limitations

1）Data requirements & Generalization

1. Presently, the field's understanding of the amount of data required to successfully train a neural certificate is based largely on intuition and experience; there is not yet a firm theoretical footing to predict the data required by a certificate-learning framework.
2. Closely related is the issue of generalization error, which relates a learned certificate's performance on a finite training set with its performance on the full state space (as discusses in Section V-E).

2）Scalable verification

1. As mentioned in Section V-E, there has yet to be an effective solution to the certificate verification problem that scales to networks involving > 100neurons. Probabilistic guarantees based on generalization error bounds [44], [14], [11] or almost Lyapunov theory [82] have the potential to scale by replacing exhaustive verification with probabilistic guarantees, but this theory has yet to be fully developed and integrated into the certificate learning process (all existing applications of these techniques are post hoc).

### B. Future work

1）Model-free certificate learning and theoretical connections to RL

1. On a theoretical level, deep connections between certificate learning and reinforcement learning remain unexplored. For example, [34] shows that it is possible to construct a reward function for specific RL problems so that the corresponding value function is also a Lyapunov function, but it is not well understood whether this is possible more generally. In particular, what conditions must the reward function satisfy so that the value function implies a Lyapunov function? Is it always possible to construct such a reward, even when non-stability objectives are included in the reward function?

2）Heterogeneous multi-agent certificates

1. However, these works focus exclusively on the case when every agent in the fleet has identical dynamics and constraints, as this allows a single certificate function to be learned for all agents at once. To extend these methods to heterogeneous multi-agent systems (e.g. a fleet of multiple autonomous delivery trucks, each with its own fleet of UAVs).

3）Distributed systems & networks control

1. Related to the subject of heterogeneous multi-agent control, we believe there is an opportunity for fruitful research in learning certificates for distributed systems and networks.
2. The application of certificate learning in this area also presents an interesting opportunity to apply graph neural networks [99], [100] to learn network control certificates.

## 7. CONCLUSION

1. A general framework for automatic certificate synthesis has long eluded control theorists.
2. In this context, neural certificates represent an important step forward for the state of the art for computational synthesis of nonlinear controllers. Neural certificates do not require a choice of hand-designed basis, as LP-based methods do, nor are they limited to systems with polynomial dynamics, as SoS methods are.
