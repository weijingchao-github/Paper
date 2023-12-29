# Collision Free Navigation with Interacting, Non-Communicating Obstacles

## Key Points

本文提出了多智能体在无法相互通信的情况下基于CBF-QP互相避障的PCCA算法。

**摘要：**
In this paper we consider the problem of navigation and motion control in an area densely populated with other agents. We propose an algorithm that, without explicit communication and based on the information it has, computes the best control action for all the agents and implements its own. Notably, the host agent (the agent executing the algorithm) computes the differences between the other agents' computed and observed control actions and treats them as known disturbances that are fed back into a robust control barrier function (RCBF) based quadratic program.

**Key Words：**
无

## 1. INTRODUCTION

1. We consider the problem of an autonomous vehicle or robot (referred to as the "host") operating in an environment with other autonomous or human-operated agents (referred to as "targets") that it has no communication with, yet interacts through observed actions.
2. Most papers concerning collision avoidance with interacting agents are in the field of robotics. The Interacting Gaussian Process (IGP) method [12] is a position-based approach that tackles the so-called "frozen robot problem" with humans acting as interacting moving obstacles to the mobile robot. The algorithm computes "likely" future positions of the host and the targets using a joint probability density function obtained from empirical data. No kinematic or dynamic model was used – it is just assumed that the robot and the pedestrians could occupy these precomputed positions at the scheduled time.
3. reciprocal velocity approach
4. acceleration-based approach with Control Barrier Functions (CBF)
5. In this paper, we set up a quasi-centralized QP based on Robust Control Barrier Functions (RCBFs) (see [6]) while still assuming no explicit communication between agents. Each agent computes optimal accelerations for all the agents, with information at its disposal, and implements its own control action.
6. Because the host predicts and then corrects the target acceleration, we refer to the algorithm as the Predictor-Corrector for Collision Avoidance (PCCA).

## 2. ROBUST CONTROL BARRIER FUNCTIONS

## 3. INTERACTING AGENTS WITH NO COMMUNICATION

1. 介绍了Centralized QP, Decentralized QP, PCCA QP

## 4. SIMULATION RESULTS

## 5. CONCLUSIONS

We considered the problem of navigation and motion control in an area shared with other agents. Without explicit communication, the control algorithm utilizes observed acceleration of each target agent and compares it to its "best" action as computed by the host. The difference between observed and computed accelerations guides a modification to the action taken by the host and a recomputed best action for the targets. The algorithm is shown to be stable and to avoid collisions if the sampling is fast enough. The result applies in the case the other agent is cooperating, as well as when it is not cooperating as assumed. The design allows a tight representation of obstacles which is beneficial in densely populated operating areas.
