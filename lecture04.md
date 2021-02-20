# Lecture 04 Model Free Prediction

### 4.1 Introduction

* Estimate the value function of an unknown MDP 通过agent与environment交互来估计过程

### 4.2 Monte Carlo Learning

* learns directly from episodes of experience; from complete episodes no boot-strapping; can only apply to episodic MDPs \(all episodes must terminate\) .
* Monte Carlo policy evaluation uses **empirical mean return** instead of expected mean return.
* **First Visit Monte Carlo Policy Evaluation**

  To evaluate state s, take the first time step t that the state s is visited in an episode. Increment counter and total return, and take the mean. 取每个样本第一次visit state s的return的平均值，根据大数定律，样本均值趋近于整体期望，即policy value.

* **Every Visit Monte Carlo Policy Evaluation**

  区别于first visit MC方法，取所有visit state s的return的均值进行估计。

* Incremental mean$$\mu_k=\sum_{i=1}^kx_i/k=(x_k+\sum_{i=1}^{k-1}x_i)/k=(x_k+(k-1)\mu_{k-1})/k=\mu_{k-1}+(x_k-\mu_{k-1})/k$$ 
* Incremental Monte Carlo updates

  同上$$N(S_t) \leftarrow N(S_t)+1$$ ,$$V(S_t) \leftarrow V(S_t)+(G_t-V(S_t))/N(S_t)$$.

  在non-stationary的情况下，用$$V(S_t) \leftarrow V(S_t)+(G_t-V(S_t))/\alpha$$ .

### 4.3 Temporal Difference Learning





