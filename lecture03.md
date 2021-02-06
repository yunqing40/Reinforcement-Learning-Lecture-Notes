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
* Bellman equation: $$v_{k+1}(s)=\sum_{a \in A} \pi(a|s) (R^a_s+\gamma \sum_{s' \in S} P^a_{ss'}v_k(s'))$$ or $$v_{k+1} = R_\pi+\gamma P^\pi v_k$$.   从state s 到action a再到第k步的state s'. 迭代更新成第k+1步的state s. 从后往前推 ??

### 3.3 Policy Iteration

* Example: Small Grid-world using Random policy \(取所有路径产生value的期望，迭代到收敛 _问题: 如何定义收敛？证明收敛？_\) v.s. Greedy policy \(根据random policy每步结果只选择每个state的最优路径到收敛  _问题: 会不会陷入局部最优解？_\).
* Given a policy $$\pi$$,  evaluate the policy $$v_\pi (s) = E(R_{t+1}+\gamma R_{t+2}+...|S_t=s)$$ and improve the policy by acting greedily with respect to $$v_\pi$$,  $$\pi'=greedy(v_\pi)$$. Do iteration and it always converges to the optimal policy $$\pi^*$$.
* **\[Proof\]** 1. Consider a deterministic policy $$\pi(s)$$.

  2. Improve the policy by acting greedily, $$\pi' (s) =argmax_{a \in A} q_\pi (s,a)$$ .

  3. This improves the value from any state s over one step, $$q_\pi(s,\pi'(s)) = max_{a \in A} q_\pi (s,a) \ge q_\pi(s,\pi(s)) = v_\pi(s)$$. 这里只更新一步policy，后面的步骤维持原deterministic policy不变.

  4. Therefore, improves the value function $$v_{\pi'}(s) \ge v_\pi(s)$$.

  $$v_\pi(s) \le q_\pi(s,\pi'(s)) = E_{\pi'}(R_{t+1}+\gamma v_\pi(S_{t+1})|S_t=s)\\ \le E_{\pi'}(R_{t+1}+\gamma q_\pi(S_{t+1},\pi'(S_{t+1}))|S_t=s)\\ \le E_{\pi'}(R_{t+1}+\gamma R_{t+2} + \gamma^2 q_\pi(S_{t+2},\pi'(S_{t+2}))|S_t=s)\\ ... \\ \le  E_{\pi'}(R_{t+1}+\gamma R_{t+2}+...|S_t=s) = v_{\pi'}(s)$$  

  5. If the improvements stop, according to Bellman optimality equation, we get the optimal policy.

* How to stop the iteration?
  * 定义$$\epsilon$$convergence of value function 收敛threshold
  * 定义最多K步 \(e.g. K=1时 policy iteration同value iteration\)

### 3.4 Value Iteration





