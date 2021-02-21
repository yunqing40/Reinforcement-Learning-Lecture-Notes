# Lecture 04 Model Free Prediction

### 4.1 Introduction

* Estimate the value function of an unknown MDP 通过agent与environment交互来估计过程

### 4.2 Monte Carlo Learning

* learns directly from episodes of experience; from complete episodes no bootstrapping; can only apply to episodic MDPs \(all episodes must terminate\) .
* Monte Carlo policy evaluation uses **empirical mean return** instead of expected mean return.
* **First Visit Monte Carlo Policy Evaluation**

  To evaluate state s, take the first time step t that the state s is visited in an episode. Increment counter and total return, and take the mean. 取每个样本第一次visit state s的return的平均值，根据大数定律，样本均值趋近于整体期望，即policy value.

* **Every Visit Monte Carlo Policy Evaluation**

  区别于first visit MC方法，取所有visit state s的return的均值进行估计。

* Incremental mean$$\mu_k=\sum_{i=1}^kx_i/k=(x_k+\sum_{i=1}^{k-1}x_i)/k=(x_k+(k-1)\mu_{k-1})/k=\mu_{k-1}+(x_k-\mu_{k-1})/k$$ 
* Incremental Monte Carlo updates

  同上$$N(S_t) \leftarrow N(S_t)+1$$ ,$$V(S_t) \leftarrow V(S_t)+(G_t-V(S_t))/N(S_t)$$.

  在non-stationary的情况下，用$$V(S_t) \leftarrow V(S_t)+\alpha(G_t-V(S_t))$$ .

### 4.3 Temporal Difference Learning

* learns from incomplete episodes by bootstrapping; updates a guess towards a guess.
* 用estimated return TD target $$R_{t+1}+\gamma V(S_{t+1})$$来代替actual return $$G_t$$, $$V(S_t) \leftarrow V(S_t)+\alpha(R_{t+1}+\gamma V(S_{t+1})-V(S_t))$$. TD target和value的差称为TD error.
* TD和Monte Carlo差别 -- TD可以learn before knowing the final outcome, works in continuous \(non-terminating\) environment，而Monte Carlo需要complete episodes and final outcome. Monte Carlo里面的 $$G_t$$ 是unbiased estimation of $$V_\pi(S_t)$$，而TD target是biased. 同时, TD的variance is lower, 因为只有 $$R_{t+1}$$这一步产生noise. Monte Carlo has good convergence property and is not very sensitive to initial value, whereas, TD is more efficient and TD\(0\) converges to v and is more sensitive to initial value.
* 对比repeatedly using finite episodes Monte Carlo 和 TD\(0\) 两种方法 -- MC converges to solution with min mean-squared error  $$\sum_{k=1}^K \sum_{t=1}^{T_k} (g_t^k-V(s_t^k))^2$$ , whereas, TD converges to solution with max likelihood of Markov model $$P_{ss'}^a=\sum_{k=1}^K \sum_{t=1}^{T_k} 1 (s,a,s')/N(s,a)$$ and $$R_s^a=\sum_{k=1}^K \sum_{t=1}^{T_k} 1 (s,a)r_t^k/N(s,a)$$. TD exploits Markov property and usually more efficient in Markov environment. MC is more efficient in non-Markov environment.
* MC不做bootstrapping, TD和DP都有bootstrapping 树深度. DP没有sampling, MC和TD都有sampling 树广度.

### 4.4 TD \(lambda\)

* 用n步returns估计 $$G_t^{(n)}=R_{t+1}+\gamma R_{t+2}+...+\gamma ^{n-1}R_{t+n}+\gamma^nV(S_{t+n})$$ . 当n趋近于无穷时，TD趋近于MC. $$V(S_t) \leftarrow V(S_t)+\alpha(G_t^{(n)}-V(S_t))$$
* TD \(lambda\) 给不同的 $$G_t^{(n)}$$ 以 $$(1-\lambda)\lambda^{n-1}$$ 的权重平均化。 $$G_t^\lambda=(1-\lambda)\sum_{n=1}^\infty \lambda^{n-1}G_t^{(n)}$$, $$V(S_t) \leftarrow V(S_t)+\alpha(G_t^\lambda-V(S_t))$$
* TD \(lambda\)也需要complete episodes 但同时online updating
* **Eligibility Traces** combines both frequency heuristic and recency heuristic $$E_0(s)=0$$, $$E_t(s)=\gamma \lambda E_{t-1}(s)+1(S_t=s)$$. _???_ Backward view of TD \(lambda\), $$V(S_t) \leftarrow V(S_t)+\alpha\delta_tE_t(s)$$. 
* **\[Theorem\]** The sum of offline updates is identical for forward view and backward view of TD \(lambda\), $$\sum_{t=1}^T \alpha \delta_t E_t(s) = \sum_{t=1}^T \alpha(G_t^\lambda-V(S_t))1(S_t=s)$$ .

  当lambda=0 时,  $$E_t(s)=1$$. 当lambda=1时, forward TD就是MC, backward total updates和MC的一致.

 









