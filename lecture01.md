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

ML includes Supervised Learning, Unsupervised Learning and RL.

### 1.3 Elements of a RL problem 基本元素

* **Input/Output Elements**

  * **Reward \(** $$R_t$$ **\)**

  A reward is a scalar feedback signal that indicates how well agent is doing at step t. 

  **\[Def\] Reward Hypothesis** All goals can be described by the maximization of expected cumulative reward.

  * **Observation \(** $$O_t$$ **\)**
  * **Action \(** $$A_t$$ **\)**

* **主体**

  * **Environment**
  * **Agent**

  Agent receives observation and reward to take action at each step t.

  After taking action, the environment will be updated and will provide the updated reward and observation as inputs to the agent at the next step.

  在environment和agent之间形成循环。

* **Goal**
  * Select actions to maximize total future reward.

    May sacrifice immediate reward to gain more long term reward. 

    考虑最大化未来累积奖励而不是即时奖励。
* **State**
  * History $$H_t = A_1, O_1, R_1, A_2, O_2, R_2, ..., A_t, O_t, R_t$$ 
  * \_\_$$S_t = f(H_t)$$ __
  * Types of States
    * Environment state $$S^e_t$$ . It's not usually visible to the agent. It may contain irrelevant information. 
    * Agent state $$S^a_t$$ . It's the information used by RL algorithm.

      **\[Def\] Markov State** A state $$S_t$$ is Markov if and only if $$P(S_{t+1}|S_t) = P(S_{t+1}|S_1,S_2,...,S_t)$$. 马尔科夫链无记忆性。
  * Observability
    * Full Observability $$O_t = S^e_t = S^a_t$$ --&gt; Markov decision process \(MDP\)
    * Partial Observability $$S^e_t \ne S^a_t$$ --&gt; partially observable Markov decision process \(POMDP\) 这里估计 $$S^a_t$$ 可以假设观测 $$O_t$$ 是完整的，或者假设 $$S^e_t$$ 概率分布，或者用recurrent neural network \(RNN\)  $$\sigma (W_tO_t+W_sS^a_{t-1})$$ 估计等等。

### 1.4 Major Components of a RL Agent

* **Policy** Agent's behavior function. A map from state to action. 
  * Deterministic policy $$\pi (s) = a$$ 
  * Stochastic policy $$\pi (a|s) = P(A=a|S=s)$$ 
* **Value function** Evaluate how good each state/action is. A prediction of future reward.
  * $$v_\pi(s) = E_\pi (R_t + \gamma R_{t+1} + \gamma^2 R_{t+2} +...|S_t = s)$$ 
* **Model** Agent's representation of the environment. Predicts what the environment will do next.
  * Transition P predicts the next state. $$P^a_{ss'} = P(S'=s'|S=s, A=a)$$ 
  * Reward R predicts the next reward. $$R^a_s = E(R|S=s, A=a)$$ 









\*\*\*\*

















## References

1. An Introduction to Reinforcement Learning by Richard S. Sutton and Andrew G. Barto, 2nd ed.  [\[pdf\]](http://www.andrew.cmu.edu/course/10-703/textbook/BartoSutton.pdf)
2. Algorithms for Reinforcement Learning by Csaba Szepesvari, 2009.  [\[pdf\]](https://sites.ualberta.ca/~szepesva/papers/RLAlgsInMDPs.pdf)

