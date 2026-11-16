# Tutorial 5 — Fundamental and Probabilistic Inequalities

COMP2610 / COMP6261 Information Theory · Week 5, Semester 2, 2026  
[Original PDF](../tutpdf/tut5.pdf)

## Question 1

### English question

Let $X$, $Y$ and $Z$ be jointly distributed random variables. Prove the following relations and find the conditions for equality in the inequalities.

- (a) $H(X,Y\mid Z)\ge H(X\mid Z)$.
- (b) $I(X,Y;Z)\ge I(X;Z)$.
- (c) $H(X,Y,Z)-H(X,Y)\le H(X,Z)-H(X)$.
- (d) $I(X;Z\mid Y)=I(Z;Y\mid X)-I(Z;Y)+I(X;Z)$.

### 中文翻译

设 $X,Y,Z$ 有联合分布。证明 (a) $H(X,Y\mid Z)\ge H(X\mid Z)$，(b) $I(X,Y;Z)\ge I(X;Z)$，(c) $H(X,Y,Z)-H(X,Y)\le H(X,Z)-H(X)$，(d) $I(X;Z\mid Y)=I(Z;Y\mid X)-I(Z;Y)+I(X;Z)$。给出不等式取等条件。

### 知识点

**链式法则**逐个加入变量。例如 $I(X,Y;Z)=I(X;Z)+I(Y;Z\mid X)$。条件互信息是条件分布之间的相对熵的平均，因此非负，在每个有正概率的条件下独立时为零。条件熵为零意味着已知条件就可确定该变量。

### 解题讲解

- (a) 左边减右边为 $H(Y\mid X,Z)\ge0$。当 $Y$ 由 $(X,Z)$ 确定时取等。
- (b) 左边减右边为 $I(Y;Z\mid X)\ge0$。当 $Y$、$Z$ 给定 $X$ 后独立时取等。
- (c) 改写成 $H(Z\mid X,Y)\le H(Z\mid X)$，右边减左边仍是 $I(Y;Z\mid X)$，取等条件同 (b)。
- (d) 按两种顺序展开 $I(X,Y;Z)$，得 $I(Y;Z)+I(X;Z\mid Y)=I(X;Z)+I(Y;Z\mid X)$。移项并利用互信息对称性即得所求恒等式。

## Question 2

### English question

For each pair, indicate the general relationship using $\ge$, $=$ or $\le$.

- (a) $H(5X)$ vs. $H(X)$
- (b) $I(g(X);Y)$ vs. $I(X;Y)$
- (c) $H(X_0\mid X_{-1})$ vs. $H(X_0\mid X_{-1},X_1)$
- (d) $\dfrac{H(X,Y)}{H(X)+H(Y)}$ vs. $1$

### 中文翻译

判断以下左右两边的一般关系，分别填 $\ge$、$=$ 或 $\le$。(a) $H(5X)$ 与 $H(X)$。(b) $I(g(X);Y)$ 与 $I(X;Y)$。(c) $H(X_0\mid X_{-1})$ 与 $H(X_0\mid X_{-1},X_1)$。(d) $H(X,Y)/(H(X)+H(Y))$ 与 1。

### 知识点

一一对应的变换保留熵。确定性变换不能增加与另一变量的互信息。增加已知条件后，**平均**条件熵只会减少或持平。联合熵不超过边缘熵之和，差值就是互信息。

### 解题讲解

(a) $=$，因为可除以 5 找回 $X$。(b) $\le$，因为 $Y\to X\to g(X)$，可用数据处理不等式。(c) $\ge$，差为 $I(X_0;X_1\mid X_{-1})$。(d) 当分母正时 $\le$，因为 $H(X)+H(Y)-H(X,Y)=I(X;Y)\ge0$。若两个变量都确定，分母为零，原比值无定义。

## Question 3 — Markov's Inequality for Probabilities

### English question

Let $p(x)$ be a probability mass function. Prove that for all $d\ge 0$,

$$
\Pr\{p(X)\le d\}\log\left(\frac{1}{d}\right)\le H(X).
$$

> The PDF states $d\ge 0$. The expression $\log(1/d)$ is defined for $d>0$.

### 中文翻译

设 $p(x)$ 为概率质量函数。证明题中关于 $\Pr\{p(X)\le d\}$ 与 $H(X)$ 的不等式。原题将范围写为 $d\ge0$。

### 知识点

**Markov 不等式**用于非负变量 $W$。对 $t>0$，$P(W\ge t)\le\mathbb E[W]/t$，因为光是 $W\ge t$ 的情形就贡献至少 $tP(W\ge t)$ 的期望。

### 解题讲解

令 $W=-\log_2 p(X)$，它非负且均值是 $H(X)$。对 $0<d<1$，事件 $p(X)\le d$ 等价于 $W\ge\log_2(1/d)$，应用 Markov 不等式并乘回阈值即可。$d\ge1$ 时左边非正，结论也成立。$d=0$ 时原表达式无定义，可以按 $d\downarrow0$ 的极限读作 0，因为 $tP(W\ge t)\le\mathbb E[W\mathbf 1_{W\ge t}]\to0$（有限熵时）。

## Question 4 — Asymptotic Equipartition Property

### English question

A discrete memoryless source emits statistically independent binary digits with probabilities $p(1)=0.005$ and $p(0)=0.995$. The digits are taken 100 at a time. A binary codeword is assigned to every sequence of 100 digits that contains three or fewer ones.

- (a) Assuming all codewords have the same length, find the minimum length required to assign a codeword to every such sequence.
- (b) Calculate the probability of observing a source sequence that has no assigned codeword.
- (c) Use Chebyshev's inequality to bound that probability. Compare the bound with the actual probability computed in part (b).

### 中文翻译

无记忆二元信源独立地产生各位，$P(1)=0.005$，$P(0)=0.995$。每 100 位为一块，只给至多三个 1 的块分配码字。(a) 求统一码长的最小值。(b) 求未获分配的概率。(c) 用 Chebyshev 不等式给上界，并与精确值比较。

### 知识点

**码字**是代表整个源块的比特串。长度 $L$ 可提供 $2^L$ 个不同码字。**AEP** 指 i.i.d. 信源长块的每符号自信息会靠近信源熵，因而可优先编码一批高概率块。本题指定了有限长度下的具体覆盖范围。**Chebyshev 不等式**给出 $P(|K-\mu|\ge t)\le\sigma^2/t^2$。

### 解题讲解

(a) 码字数需要 $\sum_{k=0}^3\binom{100}k=166751$，介于 $2^{17}$ 和 $2^{18}$ 之间，故最少 18 bits。

(b) $K\sim\operatorname{Bin}(100,0.005)$，所求为
$$
P(K\ge4)=1-\sum_{k=0}^3\binom{100}k(0.005)^k(0.995)^{100-k}\approx0.00167327.
$$

(c) $\mu=0.5,\sigma^2=0.4975$。$K\ge4$ 必有 $|K-0.5|\ge3.5$，所以上界 $0.4975/3.5^2\approx0.0406122$，高于精确概率。
