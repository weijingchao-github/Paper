# SACSoN: Scalable Autonomous Control for Social Navigation

**摘要：**
通过机器学习方法使得将机器人引入人的环境后，机器人导航运动时尽量避免影响人的正常运动，目的是人能够像尽可能像引入机器人前一样运动，尽量不受干扰。
本文的主要工作是如何利用数据去训练策略和如何收集人与机器人交互的数据制作数据集。

1. In this letter, our goal is to develop methods for training policies for socially unobtrusive behavior, such that robots can navigate among humans in ways that don't disturb human behavior.
2. We introduce a definition for such behavior based on the counterfactual perturbation of the human: If the robot had not intruded into the space, would the human have acted in the same way? By minimizing this counterfactual perturbation, we can induce robots to behave in ways that do not alter the natural behavior of humans in the shared space.
3. our approach is based on two key contributions. First, we collect a large dataset where an indoor mobile robot interacts with human bystanders. Second, we utilize this dataset to train policies that minimize counterfactual perturbation.

**Key Words：**
Machine Learning for Robot Control, Data Sets for Robot Learning, social navigation

## 1. INTRODUCTION

1. we train the SACSoN (Scalable Autonomous Control for SocialNavigation) policy to minimize the impact on human behavior for vision-based navigation using a single camera. This requires us to both formalize the notion of counterfactual perturbation into an objective, and to collect a dataset that has the kinds of human-robot interactions that can allow our model to learn to predict human behavior in the presence of robots.
2. Thus, our work focuses on two complementary technical components: the design of a policy learning method that can utilize predictive models of humans for unobtrusive navigation, and the collection of a large dataset of human-robot interactions to train these predictive models.
3. Our work makes the following contributions: (i) a modelbased method for learning a socially compliant SACSoN policy for visual navigation around humans, (ii) an autonomous data collection system, HuRoN, that encourages rich interactions with human pedestrians using a novel training objective, and (iii) the HuRoN dataset, a large and diverse dataset comprising over 4000 human-robot interactions of an autonomous robot operating in a densely populated office-space environment. Please see the project page for the dataset and videos.
