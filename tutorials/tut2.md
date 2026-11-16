# Tutorial 2 — Probability and Bayesian Inference

COMP2610 / COMP6261 Information Theory · Week 2, Semester 2, 2023  
Manish Kumar · [Original PDF](../tutpdf/tut2.pdf)

## Question 1

### English question

*From Bishop (2006).* There are three coloured boxes: red ($r$), blue ($b$) and green ($g$).

| Box | Apples | Oranges | Limes |
| --- | ---: | ---: | ---: |
| Red | 3 | 4 | 3 |
| Blue | 1 | 1 | 0 |
| Green | 3 | 3 | 4 |

A box is chosen at random with probabilities $p(r)=0.2$, $p(b)=0.2$ and $p(g)=0.6$. A piece of fruit is then chosen at random from the box.

- (a) What is the probability of selecting an apple?
- (b) If the selected fruit is an orange, what is the probability that it came from the green box?

### 中文翻译

以概率 0.2、0.2、0.6 选择红、蓝、绿箱，再在选中的箱子里等概率抽一个水果。各箱水果数量见英文表格。(a) 求抽到苹果的概率。(b) 已知抽到橙子，求它来自绿箱的概率。

### 知识点

**先验**是看证据前的概率，**后验**是给定证据后的概率。贝叶斯公式 $P(A\mid B)=P(B\mid A)P(A)/P(B)$ 来自用两种顺序计算同一个交集。条件右边的事件决定分母。

### 解题讲解

(a) 将选箱概率乘各箱内苹果比例后相加，$0.2(3/10)+0.2(1/2)+0.6(3/10)=0.34$。

(b) 三箱贡献的橙子概率依次为 $0.08,0.10,0.18$，合计 $0.36$。只在抽到橙子的情形中比较，绿箱占 $0.18/0.36=0.5$。

## Question 2

### English question

A scientist conducts 1,000 trials of an experiment involving variables $X$ and $Y$, each with possible values $\{0,1\}$. The scientist records the following counts.

| | $X=0$ | $X=1$ |
| --- | ---: | ---: |
| $Y=0$ | 100 | 250 |
| $Y=1$ | 150 | 500 |

Compute each of the following, showing all your working.

- (a) $p(X=1,Y=1)$.
- (b) $p(X=1)$.
- (c) $\mathbb{E}[X]$.
- (d) $p(Y=1\mid X=1)$.
- (e) $p(Y=1\mid X=0)$.
- (f) Let $Z$ be a noisy version of the XOR of $X$ and $Y$, with

  $$
  p(Z=1\mid X=x,Y=y)=
  \begin{cases}
  0.9 & \text{if } (x,y)=(0,1) \text{ or } (1,0),\\
  0.1 & \text{if } (x,y)=(0,0) \text{ or } (1,1).
  \end{cases}
  $$

  Compute $p(X=1,Y=1\mid Z=1)$.

### 中文翻译

实验重复 1000 次，记录取值均为 0 或 1 的 $X,Y$，计数见英文表格。写出计算过程，求 (a) $P(X=1,Y=1)$，(b) $P(X=1)$，(c) $\mathbb E[X]$，(d) $P(Y=1\mid X=1)$，(e) $P(Y=1\mid X=0)$。(f) 带噪异或输出 $Z$ 在输入不同时以 0.9 的概率为 1，输入相同时以 0.1 的概率为 1。求 $P(X=1,Y=1\mid Z=1)$。

### 知识点

**联合概率**查一个格子，**边缘概率**把不关心的变量加掉，**条件概率**用给定行或列的总数作分母。**期望**是数值的概率加权平均。**异或**在两个输入不同时输出 1。

### 解题讲解

(a) $500/1000=0.5$。(b) $(250+500)/1000=0.75$。(c) $0(0.25)+1(0.75)=0.75$。(d) $500/750=2/3$。(e) $150/250=0.6$。

(f) 不同的输入占 $(150+250)/1000=0.4$。因此 $P(Z=1)=0.9(0.4)+0.1(0.6)=0.42$。分子是输入 $(1,1)$ 且噪声使 $Z=1$ 的概率 $0.5(0.1)=0.05$，答案为 $0.05/0.42=5/42$。

## Question 3

### English question

*From Barber (2011).* Two balls are placed in a box as follows:

- Toss a fair coin.
- If it lands heads, put a white ball in the box. Otherwise, put a red ball in the box.
- Toss the coin again.
- If it lands tails, put a red ball in the box. Otherwise, put a white ball in the box.

Draw a ball three times, replacing it after each draw. All three draws are red. What is the probability that both balls in the box are red?

### 中文翻译

抛公平硬币两次。每次正面就放一颗白球，反面就放一颗红球。两颗球放好后，放回抽取三次，三次均为红球。求箱中两颗都为红球的概率。

### 知识点

**条件独立**指给定共同条件后，各观测可以按独立事件相乘。本题固定箱内组成后，每次放回抽取才具有相同且独立的红球概率。

### 解题讲解

箱中红球数 $K=0,1,2$ 的先验分别为 $1/4,1/2,1/4$。给定 $K=k$，三次全红的概率为 $(k/2)^3$。观察到三次全红后，两颗都红的后验为
$$
\frac{(1/4)1^3}{(1/4)0^3+(1/2)(1/2)^3+(1/4)1^3}=\frac45.
$$

## Question 4

### English question

Several results from the lectures generalise when we condition on additional random variables.

- (a) For random variables $X$ and $Y$, the conditional probability is defined as

  $$
  p(X\mid Y)=\frac{p(X,Y)}{p(Y)}.
  $$

  Using this definition, show that for random variables $X$, $Y$ and $Z$, the following conditional version of Bayes' rule holds:

  $$
  p(X\mid Y,Z)=\frac{p(Y\mid X,Z)p(X\mid Z)}{p(Y\mid Z)}.
  $$

- (b) The sum rule (marginalisation) for random variables $X_1,\ldots,X_n$ states that

  $$
  p(X_1,\ldots,X_{i-1},X_{i+1},\ldots,X_n)
  =\sum_x p(X_1,\ldots,X_{i-1},X_i=x,X_{i+1},\ldots,X_n).
  $$

  Using this fact and the definition of conditional probability, show that

  $$
  p(X_1,\ldots,X_{i-1},X_{i+1},\ldots,X_n\mid Y)
  =\sum_x p(X_1,\ldots,X_{i-1},X_i=x,X_{i+1},\ldots,X_n\mid Y),
  $$

  where $Y$ is another random variable.

### 中文翻译

在给定额外变量的情况下证明两条规则。(a) 从条件概率定义推出给定 $Z$ 的贝叶斯公式。(b) 从联合分布的求和规则推出给定 $Y$ 时，仍可对 $X_i$ 求和消去该变量。

### 知识点

可以把 $Z=z$ 当作新的样本范围，在这个范围内继续使用乘法与加法规则。**边缘化**是对互斥且穷尽的取值求和。以下条件概率都在相应分母为正时使用。

### 解题讲解

(a) 用小写表示具体取值。按定义 $P(x\mid y,z)=P(x,y\mid z)/P(y\mid z)$，而 $P(x,y\mid z)=P(x\mid z)P(y\mid x,z)$，代入即得原式。

(b) 设 $U$ 包含除 $X_i$ 外的其他变量。固定 $Y=y$，
$$
P(U=u\mid Y=y)=\frac{\sum_x P(U=u,X_i=x,Y=y)}{P(Y=y)}
=\sum_x P(U=u,X_i=x\mid Y=y).
$$
