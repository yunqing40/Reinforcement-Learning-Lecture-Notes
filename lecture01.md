---
description: >-
  2021-01 Taking notes for Reinforcement Learning lectures taught by David
  Silver
---

# Lecture 01 Introduction to Reinforcement Learning

## 1. Reinforcement Learning \(RL\) Background Knowledge 强化学习基本概念

### 1.1 RL in different fields 学科交叉与应用

* Machine Learning in Computer Science
* Reward System in Neuroscience
* Classical/Operant Conditioning in Psychology
* Bounded Rationality in Economics
* Operations Research in Mathematics
* Optimal Control in Engineering

### 1.2 Relationship between RL and Machine Learning \(ML\) 和机器学习的关系

ML includes Supervised Learning, Unsupervised Learning and RL

### 1.3 Elements of a RL problem 基本元素

* **Input/Output Elements**

  * **Reward \(R\_t\)**

  A reward is a scalar feedback signal that indicates how well agent is doing at step t. 

  **\[Def\] Reward Hypothesis** All goals can be described by the maximization of expected cumulative reward.

  * **Observation \(O\_t\)**
  * **Action \(A\_t\)**

  \*\*\*\*

* **Goal**

Select actions to maximize total future reward.

May sacrifice immediate reward to gain more long term reward. 

考虑最大化未来累积奖励而不是即时奖励。

* **Environment**
* **Agent**

Agent receives observation and reward to take action at each step t.

After taking action, the environment will be updated and will provide the updated reward and observation as inputs to the agent at the next step.

\*\*\*\*

















## References

1. An Introduction to Reinforcement Learning by Richard S. Sutton and Andrew G. Barto, 2nd ed.  [\[pdf\]](http://www.andrew.cmu.edu/course/10-703/textbook/BartoSutton.pdf)
2. Algorithms for Reinforcement Learning by Csaba Szepesvari, 2009.  [\[pdf\]](https://sites.ualberta.ca/~szepesva/papers/RLAlgsInMDPs.pdf)

