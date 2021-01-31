# Lecture 02 Markov Decision Processes

### 2.1 Introduction to MDP

* Environment is fully observable or assumed to be fully observable \(converting POMDP into MDP\)
* **Transition Probability** $$P_{ss'} = P(S_{t+1}=s' | S_t = s)$$ 
* **Transition Matrix** $$P = \begin{pmatrix} P_{11},P_{12}, ..., P_{1n} \\ ...\\ P_{n1},P_{n2}, ..., P_{nn}  \end{pmatrix}$$ 每行的概率加和为1
* **\[Def\] Markov Process** $$(S, P)$$ where S is a finite set of states, and P is a transition matrix.

### 2.2 Markov Reward Process

* **\[Def\] Markov Reward Process** $$(S, P, R, \gamma) $$ where R is a reward function $$R_s = E(R_{t+1}|S_t=s)$$, and $$\gamma \in [0,1]$$is a discount factor.
* **Return** is the total discounted reward from step t afterwards $$G_t = R_{t+1}+\gamma R_{t+2} + ...$$ 
  * 为什么用t+1而不是t? 因为站在t时间点, agent要分析$$S_t$$的状态来给出下一步的reward, 如此往复. Notation convention
  * 这里$$G_t$$是其中一个sample样本, 后面我们需要取期望来估计全局.
  * 为什么加入$$\gamma$$? 有多种角度来解释. 首先, 我们相对于未来的reward更倾向于近期即得的reward, 当取值为1时preference of when to reward无差别. If we know all sequences will terminate, we can use undiscounted MRP. 另外, 使用$$\gamma$$源于数学运算方便, 避免无限循环, 解释由于对未来的不确定性所作出判断的价值递减, 在金融领域相当于折现率, 等等. _问题:最终这个随机过程是否收敛, 是否平稳stationary? 在什么取值范围内满足这种性质?_
* **Value** is the expected return starting from state s $$v(s)= E(G_t|S_t=s)$$ 
* **Bellman Equation for MRP**  此处是重点 Bellman方程贯穿整个算法

  这里推导用到 $$E(X)=E(E(X|Y))$$ 和马氏链性质

  $$v(s) = E(G_t|S_t=s)  \\= E(R_{t+1}+\gamma R_{t+2}+...|S_t=s)  \\=  E(R_{t+1}+\gamma (R_{t+2}+\gamma R_{t+3}+...)|S_t=s)  \\=E(R_{t+1}+\gamma G_{t+1}|S_t=s)  \\= E(R_{t+1}+\gamma E(G_{t+1}|S_{t+1}=s',S_t=s)|S_t=s)   \\= E(R_{t+1}+\gamma E(G_{t+1}|S_{t+1}=s')|S_t=s)  \\= E(R_{t+1}+\gamma v(s')|S_t=s)$$ 

  * 这个公式可以简单理解为 当前状态下的value等于即时reward的平均值 加上下一个状态的value的平均值的折现.
  * 这里的value只与一阶state有关,  后面会将算法复杂化加入action/policy等等.
  * 用矩阵向量表示 $$v = R+\gamma Pv \Rightarrow v=(I-\gamma P)^{-1}R$$ 
  * computation complexity is$$O(n^3)$$, where n is the number of states. 对small MRPs 可以采用这种算法. 对large MRPs 可以用dynamic programming, Monte-Carlo evaluation, temporal difference learning.

### 2.3 Markov Decision Process

* **\[Def\] Markov Decision Process** $$(S, P, A, R, \gamma) $$ where A is a finite set of actions, $$P^a_{ss'} = P(S_{t+1}=s' | S_t = s, A_t=a)$$ and  $$R^a_s = E(R_{t+1} | S_t = s, A_t=a)$$.
* **Policy** is a conditional distribution of actions given the state. $$\pi(a|s) = P(A_t=a | S_t = s)$$. Defines the behaviors of an agent. 
* 如果我们将action平均化, 这个MDP过程可以转化成MRP过程. $$P^\pi_{ss'} =\sum_{a \in A} \pi(a|s) P^a_{ss'}$$ and $$R^\pi_s =\sum_{a \in A} \pi(a|s) R^a_s$$ 
* **State-Value** is the expected return starting from state s, and then following policy $$\pi$$. $$v_\pi(s)= E_\pi(G_t|S_t=s)$$ 评估状态好坏
* **Action-Value** is the expected return starting from state s, taking action a, and then following policy $$\pi$$. $$q_\pi(s,a)= E_\pi(G_t|S_t=s, A_t=a)$$ 评估行为好坏
* **Bellman Equation** $$v_\pi(s)=E_\pi(R_{t+1}+\gamma v_\pi(s')|S_t=s)$$ and $$q_\pi(s,a)=E_\pi(R_{t+1}+\gamma q_\pi(s',a')|S_t=s,A_t=a)$$ .
  * v和q之间的关系 $$v_\pi(s)=\sum_{a \in A} \pi(a|s) q_\pi(s,a)$$ and $$q_\pi(s,a)=R^a_s+\gamma \sum_{s' \in S} P^a_{ss'}v_\pi(s')$$ . Then, we have $$v_\pi(s)=\sum_{a \in A} \pi(a|s) (R^a_s+\gamma \sum_{s' \in S} P^a_{ss'}v_\pi(s'))$$ and $$q_\pi(s,a)=R^a_s+\gamma \sum_{s' \in S} P^a_{ss'}(\sum_{a' \in A} \pi(a'|s') q_\pi(s',a'))$$ .











