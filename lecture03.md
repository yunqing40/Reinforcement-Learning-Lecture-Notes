# Lecture 03 Planning by Dynamic Programming

### 3.1 Introduction to dynamic programming

* **Dynamic** means it has sequential or temporal components in the problem.
* **Programming** refers to mathematical optimization.
* **Dynamic programming** is a general solution method for problems with following two properties, Optimal substructure 是指最优问题可以分解成多个最优子问题，得到子问题的最优解就可以得到原问题的整体最优解 and Overlapping subproblems 子问题重复发生.

  Dynamic programming 可以用在

  * Scheduling algorithms
  * String algorithms \(e.g. sequence alignment\)
  * Graph algorithms \(e.g. shortest path algorithms\)
  * Graphical models \(e.g. Viterbi algorithms\)
  * Bioinformatics \(e.g. lattice models\)

* MDP satisfies both properties and Bellman equation gives recursive decomposition. Value function stores the solutions for reusing.
* **Planning** in MDP/MRP is that the environment is known and to solve either **prediction problem** \(input is the MDP space and the policy, output is the value\) or **control problem** \(input is the MDP space, output is the optimal value and the optimal policy\).

### 3.2 Policy Evaluation

* **Problem**: Evaluate a given policy; **Solution**: iterative application of Bellman equation backup.
* **Synchronous** backups: at each iteration k+1, for all $$s \in S$$, update $$v_{k+1}(s)$$ from $$v_k(s')$$, where s' is a successor state of s.
* Bellman equation: $$v_{k+1}(s)=\sum_{a \in A} \pi(a|s) (R^a_s+\gamma \sum_{s' \in S} P^a_{ss'}v_k(s'))$$ or $$v_{k+1} = R_\pi+\gamma P^\pi v_k$$.   从state s 到action a再到第k步的state s'. 迭代更新成第k+1步的state s. 从后往前推! 理论上，循环结果与初始值无关。那么假设从终点反推，和从任意状态回推经过足够多次循环都可以得到最优解，区别在于寻找速度和循环次数。

### 3.3 Policy Iteration

* Example: Small Grid-world using Random policy \(取所有路径产生value的期望，迭代到收敛\) v.s. Greedy policy \(根据random policy每步结果只选择每个state的最优路径到收敛\).
* Given a policy $$\pi$$,  evaluate the policy $$v_\pi (s) = E(R_{t+1}+\gamma R_{t+2}+...|S_t=s)$$ and improve the policy by acting greedily with respect to $$v_\pi$$,  $$\pi'=greedy(v_\pi)$$. Do iteration and it always converges to the optimal policy $$\pi^*$$.
* **\[Proof\]** 

  1. Consider a deterministic policy $$\pi(s)$$.

  2. Improve the policy by acting greedily, $$\pi' (s) =argmax_{a \in A} q_\pi (s,a)$$ .

  3. This improves the value from any state s over one step, $$q_\pi(s,\pi'(s)) = max_{a \in A} q_\pi (s,a) \ge q_\pi(s,\pi(s)) = v_\pi(s)$$. 这里只更新一步policy，后面的步骤维持原deterministic policy不变.

  4. Therefore, improves the value function $$v_{\pi'}(s) \ge v_\pi(s)$$.

  $$v_\pi(s) \le q_\pi(s,\pi'(s)) = E_{\pi'}(R_{t+1}+\gamma v_\pi(S_{t+1})|S_t=s)\\ \le E_{\pi'}(R_{t+1}+\gamma q_\pi(S_{t+1},\pi'(S_{t+1}))|S_t=s)\\ \le E_{\pi'}(R_{t+1}+\gamma R_{t+2} + \gamma^2 q_\pi(S_{t+2},\pi'(S_{t+2}))|S_t=s)\\ ... \\ \le  E_{\pi'}(R_{t+1}+\gamma R_{t+2}+...|S_t=s) = v_{\pi'}(s)$$  

  5. If the improvements stop, according to Bellman optimality equation, we get the optimal policy.

* How to stop the iteration?
  * 定义$$\epsilon$$convergence of value function 收敛threshold
  * 定义最多K步 \(e.g. K=1时 policy iteration同value iteration\)

### 3.4 Value Iteration

* 先将优化问题分解成一系列子问题，take an optimal action and then followed by an optimal policy from the successor state.

  **\[Theorem\]** A policy $$\pi(a|s)$$ achieves the optimal value from state s, $$v_\pi(s)=v_*(s)$$, if and only if for any state s' reachable from s the policy achieves the optimal value from state s'.

* $$v_*(s)=max_{a \in A} R_s^a  + \gamma \sum_{s' \in S} P_{ss'}^av_*(s')$$ . Do iteration.
* **Synchronous** backups: at each iteration k+1, for all states, update $$v_{k+1}(s)$$from  $$v_k(s')$$.
* 区别于policy iteration 使用Bellman expectation equation, value iteration 使用Bellman optimality equation 进行迭代。policy是隐函数。intermediate value functions可以不对应任何policy。
* $$v_{k+1}(s)=max_{a \in A} (R_s^a + \gamma \sum_{s' \in S} P_{ss'}^av_k(s'))$$ 矩阵表示 $$v_{k+1}=max_{a \in A} R^a +\gamma P^av_k$$. 从 s 到 a 到 s' 的反向推导过程。
* 收敛问题见 contraction mapping theorem

### 3.5 Summary

* 问题和对应算法
  * Prediction -- Bellman expectation equation -- iterative policy evaluation
  * Control -- Bellman expectation equation + greedy policy improvement -- policy iteration
  * Control -- Bellman optimality equation -- value iteration
* 算法复杂度
  * state-value function v $$O(mn^2)$$ m is the number of actions and n is the number of states.
  * action-value function q $$O(m^2n^2)$$.

### 3.6 Extensions of DP

* **Asynchronous** DP backs up states individually in any order. 可以节省计算量 只要所有states都陆续选择更新那么收敛。
  * In-place dynamic programming

    迭代时只储存一组value function $$v(s) \leftarrow max_{a \in A} (R_s^a + \gamma \sum_{s' \in S} P_{ss'}^av(s'))$$ 里面的v都是最新的v

  * Prioritized sweeping

    定义先更新哪个state，选择使得remaining Bellman error最大的\(绝对误差\)

  * Real-time dynamic programming 

    选择states that are relevant to agent 根据agent的经验选择
* 对比**Synchronous backups** 每次更新所有的states 储存两组value functions $$v_{new}(s) \leftarrow max_{a \in A} (R_s^a + \gamma \sum_{s' \in S} P_{ss'}^av_{old}(s'))$$ 之后更新v
* DP uses full-width backups 考虑全部后续actions/states

  DP适合medium size problems \(millions of states\)，对于large size problems 会有curse of dimensionality的问题， even one backup could be very expensive. 所以考虑sample backups.





### 

###  







