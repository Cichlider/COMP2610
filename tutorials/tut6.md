# Tutorial 6

COMP2610 / COMP6261 Information Theory  
Naisheng Liang · [Original PDF](../tutpdf/tut6.pdf)

## Question 1 — Entropy

### English question

Let $p=(p_1,p_2,\ldots,p_m)$ be a probability distribution on $m$ elements, with $p_i\ge 0$ and $\sum_{i=1}^m p_i=1$. Define a new distribution $q$ on $m-1$ elements by setting $q_i=p_i$ for $i\in\{1,2,\ldots,m-2\}$ and $q_{m-1}=p_{m-1}+p_m$. Show that

$$
H(p)=H(q)+(p_{m-1}+p_m)H\left(
\frac{p_{m-1}}{p_{m-1}+p_m},
\frac{p_m}{p_{m-1}+p_m}
\right).
$$

### 中文翻译

将概率向量 $p$ 最后两项 $p_{m-1},p_m$ 合成一项，得到 $q$。证明原熵等于合并后的熵，加上「落入合并项的概率 × 在其中区分原两项的熵」。

### 知识点

**熵的分组公式**来自条件熵的链式法则。先确定结果属于哪组，再在组内确定具体结果。只有存在多个候选结果的组会产生组内不确定性。

### 解题讲解

令 $X$ 为原结果，$Y$ 为合并后的标签。$Y$ 由 $X$ 决定，所以 $H(X)=H(Y)+H(X\mid Y)$。其余各组都只有一个候选，最后一组出现概率是 $s=p_{m-1}+p_m$，组内分布为 $(p_{m-1}/s,p_m/s)$。故 $H(p)=H(q)+sH(p_{m-1}/s,p_m/s)$。若 $s=0$，整项按零计。

## Question 2 — Mutual Information and Relative Entropy

### English question

Let $X$, $Y$ and $Z$ be random variables with joint probability mass function $p(X,Y,Z)$.

- (a) Show that

  $$
  I(X,Y;Z)-I(Y,Z;X)=I(Y;Z)-I(X;Y).
  $$

- (b) Show that the relative entropy between the joint distribution and the product of the marginals satisfies

  $$
  D\left(p(x,y,z)\,\middle\|\,p(x)p(y)p(z)\right)=I(X;Y)+I(X,Y;Z).
  $$

### 中文翻译

给定三个变量 $X,Y,Z$ 的联合分布。(a) 证明 $I(X,Y;Z)-I(Y,Z;X)=I(Y;Z)-I(X;Y)$。(b) 证明联合分布到三个边缘分布乘积的相对熵为 $I(X;Y)+I(X,Y;Z)$。

### 知识点

**相对熵** $D(p\|q)=\sum p\log_2(p/q)$ 衡量两个分布的差异。它一般有方向，且非负。互信息等于联合分布到边缘乘积分布的相对熵。

### 解题讲解

(a) 用链式法则分别展开 $I(X,Y;Z)=I(Y;Z)+I(X;Z\mid Y)$ 和 $I(Y,Z;X)=I(Y;X)+I(Z;X\mid Y)$，条件互信息对称，作差后抵消。

(b) 在 $p(x,y,z)>0$ 的格子上将比值写为
$$
\frac{p(x,y,z)}{p(x)p(y)p(z)}
=\frac{p(x,y,z)}{p(x,y)p(z)}\frac{p(x,y)}{p(x)p(y)}.
$$
取对数后按联合分布平均。第一项给 $I(X,Y;Z)$，第二项对 $z$ 求和后给 $I(X;Y)$。

## Question 3 — Markov Chain

### English question

Consider a Markov chain $X_1\to X_2\to X_3$. It starts in one of $n$ states, $X_1\in\{1,2,\ldots,n\}$. It then goes down to $k<n$ states, $X_2\in\{1,2,\ldots,k\}$, before going back to $m>k$ states, $X_3\in\{1,2,\ldots,m\}$.

- (a) What is the upper bound on $I(X_1;X_3)$?
- (b) Evaluate $I(X_1;X_3)$ for $k=1$ and conclude that no dependence can survive.

### 中文翻译

马尔可夫链 $X_1\to X_2\to X_3$ 的三个变量分别最多取 $n,k,m$ 个值，其中 $k<n$ 且 $k<m$。(a) 求 $I(X_1;X_3)$ 的上界。(b) 当 $k=1$ 时求互信息并说明含义。

### 知识点

**马尔可夫链**表示给定中间状态后，后一步的分布不依赖前一步。取值最多 $k$ 个的变量熵至多 $\log_2 k$，均匀时达到上限。

### 解题讲解

(a) 数据处理不等式给出 $I(X_1;X_3)\le I(X_1;X_2)\le H(X_2)\le\log_2 k$。最后一步可由到均匀分布的相对熵 $\log_2 k-H(X_2)\ge0$ 得到。

(b) $k=1$ 时上界为零，而互信息非负，所以 $I(X_1;X_3)=0$，两者独立。

## Question 4 — Inequalities

### English question

A coin lands heads with probability $\frac15$. It is flipped $N$ times, where $N$ is even.

- (a) Use Markov's inequality to bound the probability of observing $N/2$ or more heads.
- (b) Use Chebyshev's inequality to bound the probability of observing $N/2$ or more heads. Express your answer in terms of $N$.

### 中文翻译

一枚硬币正面概率是 $1/5$，独立抛 $N$ 次，$N$ 为正偶数。(a) 用 Markov 不等式，(b) 用 Chebyshev 不等式，分别给出出现至少 $N/2$ 次正面的概率上界。

### 知识点

每次正面记作 1，反面记作 0。这种变量叫 **Bernoulli 变量**，均值是 $p$、方差是 $p(1-p)$。独立变量相加时均值和方差分别相加。

### 解题讲解

令 $K$ 为正面次数，则 $\mu=N/5,\sigma^2=4N/25$。

(a) $P(K\ge N/2)\le(N/5)/(N/2)=2/5$。

(b) $K\ge N/2$ 意味着离均值至少 $3N/10$，所以 $P(K\ge N/2)\le(4N/25)/(3N/10)^2=16/(9N)$。
