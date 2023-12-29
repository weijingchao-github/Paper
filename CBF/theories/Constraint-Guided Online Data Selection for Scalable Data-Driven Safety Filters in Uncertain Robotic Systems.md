# Constraint-Guided Online Data Selection for Scalable Data-Driven Safety Filters in Uncertain Robotic Systems

## Key Points

系统精确模型未知，但是一般会有一个nominal model，用数据驱动的方法(Gaussian Process, GP)学习CBF或CLF限制的差值△(x, u)，如下图
![20231209215804](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231209215804.png)
用差值修正后，能够以一定概率的满足系统精确模型下的CBF/CLF限制
![20231209220216](https://cdn.jsdelivr.net/gh/weijingchao-github/image_hosting_service@main/picture_bed/20231209220216.png)
利用所有收集到的数据来提升GP计算复杂度大，这篇文章的主要贡献是提出一种新的constraint-guided online data selection algorithm来降低GP inference的时间复杂度。

**摘要：**

1. 背景：As the use of autonomous robotic systems expands in tasks that are complex and challenging to model, the demand for robust data-driven control methods that can certify safety and stability in uncertain conditions is increasing.
2. 问题与挑战：However, the practical implementation of these methods often faces scalability issues due to the growing amount of data points with system complexity, and a significant reliance on high-quality training data.
3. 解决方案：In response to these challenges, this study presents a scalable data-driven controller that efficiently identifies and infers from the most informative data points for implementing data-driven safety filters. Our approach is grounded in the integration of a model-based certificate function-based method and Gaussian Process (GP) regression, reinforced by a novel online data selection algorithm that reduces time complexity from quadratic to linear relative to dataset size.
4. 解决方案的效果：Our findings reveal that our efficient online data selection algorithm, which strategically selects key data points, enhances the practicality and efficiency of data-driven certifying filters in complex robotic systems, significantly mitigating scalability concerns inherent in nonparametric learning-based control methods.

## 1. INTRODUCTION

### A. Motivation

1. **data-driven safety filter**: An alternative to the a-posteriori certification approach is using a model-based certifying filter, supplemented by data to address the limitations imposed by imperfect models. In this scheme, a certifying filter is designed using available mathematical models to ensure compliance with system-critical constraints, and then the filter is enhanced by incorporating data from the actual system to address discrepancies arising from the imperfect model.
2. The data-driven component of the filter learns how to address the effect of the discrepancy between the mathematical model and the actual system in choosing the control input that renders the system to satisfy the desired constraints.
3. there are two primary challenges associated with the data-driven certifying filter。
4. when a large dataset is available, it is crucial to investigate which data points are most critical for meeting the certifying filter's objective to properly address the scalability challenge. This raises the motivating question of the paper: by focusing on the most relevant data for system-critical constraints, can we extend the applicability of data-driven certifying filters to more complex and uncertain real-world robotic systems?

### B. Contributions

1. In this paper, we introduce an efficient approach for determining the most relevant data points for deploying datadriven certifying filters on real-world robotic systems.
2. Our method expands on our earlier work [8], [9], where we designed a data-driven filter that combines a model-based control method rooted in certificate functions, such as Control Barrier Functions (CBFs [10]) and Control Lyapunov Functions (CLFs [11]), with a Gaussian Process (GP) regression for the datadriven component. The filtered control input, guaranteed to satisfy system-critical constraints with high probability, is determined by solving a second-order cone program (SOCP). We delve into understanding which data points are critical for ensuring the feasibility of the SOCP filter and subsequently, for meeting the system-critical constraints. Guided by this understanding, we develop an efficient online data selection algorithm for the filter. Each time the SOCP controller is executed, this algorithm selects only the most relevant data points to secure the SOCP's feasibility, which considerably enhances the time complexity of the GP-based safety filter.

## 2. RELATED WORK

1. The integration of these certificate filters with data-driven methods has become increasingly popular for systems with uncertain dynamics.
2. Gaussian Process (GP) regression models provide a probabilistic assurance of prediction quality under mild assumptions.
3. Our work instead tackles the problem of robust control design, studying online which data is most relevant to achieve a desired certification property in the resulting data-driven control policy. Furthermore, our approach characterizes the relationship between data and safety in the control input space, emphasizing the richness of each data point for the specific certification objective, rather than relying on data density measures.

## 3. CERTIFYING FILTERS FOR UNCERTAIN SYSTEMS

### A. Uncertain Dynamics and Certifying Filter

1. This filtering structure is known by various names, most notably as a safety filter[4], [40]. Since this structure decouples the design process for safety assurance from the design procedure for achieving performance and thus, reducing the complexity of the control system design, it has been demonstrated to be an effective control architecture for numerous real-world applications.

### B. Certificate Function-based Design

1. Thus, this procedure implicitly assumes that the nominal model is sufficiently accurate in its approximation of the true plant to enable the identification of a valid CBF or CLF. This assumption is also present in prior works that most closely align with our research [12], [13], [16], [25], [26]. This approach is considered reasonable for feedback linearizable systems with known relative degree, owing to the inherent robustness properties of CBFs and CLFs [53], [54]. Indeed, the practice of using first-principle nominal models for designing CBFs is widely adopted for numerous complex robotics systems [55]–[57].

## 4. DATA-DRIVEN CERTIFYING FILTERS

1. The data-driven certifying filters we introduce in this section employ **Gaussian Process (GP)** regression to learn the estimate of ∆ from data.
2. If the constraint (15) is satisfied, from Assumption 1, we have a guarantee that the true certifying constraint in (5b) is satisfied with a probability of at least 1 − δ.

## 5. CONSTRAINT GUIDED ONLINE DATA SELECTION

1. In this section, we present the core contribution of our paper: a constraint-guided online data selection algorithm that improves the time complexity of GP inference for the GP-CFSOCP from O(N 2) to O(N ).
2. our approach, similar to many existing Sparse GP methods, is based on the idea that it is not necessary to reduce the uncertainty globally [62]–[64]. Instead, we aim to reduce the uncertainty for specific input classes relevant to our problem.

## 6. RESULTS

1. 总结了本文开展的工作。
2. Our investigation into the quantification of information from individual data points for the certifying filter establishes a foundation for a more profound understanding of the relationship between data and certifying control laws. Potential future research directions include incorporating data selection objectives during the data collection process for sampleefficient learning and expanding our framework to address systems with multiple certifying constraints.
