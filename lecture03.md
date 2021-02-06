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
* 




