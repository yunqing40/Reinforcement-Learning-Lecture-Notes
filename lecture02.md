# Lecture 02 Markov Decision Processes

### 2.1 Introduction to MDP

* Environment is fully observable or assumed to be fully observable \(converting POMDP into MDP\)
* **Transition Probability** $$P_{ss'} = P(S_{t+1}=s' | P_t = s)$$ 
* **Transition Matrix** $$P = \begin{pmatrix} P_{11},P_{12}, ..., P_{1n} \\ ...\\ P_{n1},P_{n2}, ..., P_{nn}  \end{pmatrix}$$ 每行的概率加和为1
* **\[Def\] Markov Process** $$(S, P)$$ where S is a finite set of states, and P is a transition matrix.

### 2.2 Markov Reward Process

* **\[Def\] Markov Reward Process** $$(S, P, R, \gamma) $$ where R is a reward function $$R_s = E(R_{t+1}|S_t=s)$$, and $$\gamma \in [0,1]$$is a discount factor.
* **Return** is the total discounted reward from step t afterwards $$G_t = R_{t+1}+\gamma R_{t+2} + ...$$ 
  * 这里$$G_t$$是其中一个sample样本, 后面我们需要取期望来估计全局.
  * 这里为什么加入$$\gamma$$? 有多种角度来解释. 首先, 我们相对于未来的reward更倾向于近期reward, 当取值为1时preference of when to reward无差别. If we know all sequences will terminate, we can use undiscounted MRP. 另外, 有$$\gamma$$源于数学运算方便, 避免无限循环, 解释由于对未来的不确定性所作出判断的价值递减, 在金融领域相当于折现率, 等等. _问题:最终这个随机过程是否收敛, 是否平稳stationary? 在什么取值范围内?_
* **Value** is the expected return starting from state s $$v(s)= E(G_t|S_t=s)$$ 







