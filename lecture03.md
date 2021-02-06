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
* Bellman equation: $$v_{k+1}(s)=\sum_{a \in A} \pi(a|s) (R^a_s+\gamma \sum_{s' \in S} P^a_{ss'}v_k(s'))$$ or $$v_{k+1} = R_\pi+\gamma P^\pi v_k$$ .
* Example: Random policy \(取所有路径产生value的期望，迭代到收敛 _问题: 证明收敛？_\) v.s. Greedy policy \(根据random policy每步结果只选择每个state的最优路径到收敛  _问题: 会不会陷入局部最优解？_\).





