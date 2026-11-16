# Tutorial 3 — Entropy and Information

COMP2610 / COMP6261 Information Theory · Week 3, Semester 2, 2023  
Angela Zhang · [Original PDF](../tutpdf/tut3.pdf)

## Question 1

### English question

Let $X$ be a random variable with possible outcomes $\{1,2,3\}$. Let the probabilities of the outcomes be

$$
p(X=1)=\frac{\theta}{2},\qquad
p(X=2)=\frac{\theta}{2},\qquad
p(X=3)=1-\theta,
$$

for some parameter $\theta\in[0,1]$. Suppose we see $N$ observations $x_1,\ldots,x_N$. Let $n_i$ denote the number of times we observe $X=i$, i.e.

$$
n_i=\sum_{k=1}^N
\begin{cases}
1 & \text{if }x_k=i,\\
0 & \text{otherwise}.
\end{cases}
$$

- (a) Write down the likelihood function of $\theta$ given the observations in terms of $n_1$, $n_2$ and $n_3$.
- (b) Suppose the observations are $3,3,1,2,3,2,2,1,3,1$. Compute the maximum likelihood estimate of $\theta$. *Hint:* Compute the log-likelihood function and check when the derivative is zero.

### 中文翻译

随机变量 $X$ 可取 1、2、3，对应概率为 $\theta/2,\theta/2,1-\theta$，其中 $0\le\theta\le1$。观察 $N$ 次，用 $n_i$ 记录 $i$ 出现的次数。(a) 写出关于 $\theta$ 的似然函数。(b) 给定序列 $3,3,1,2,3,2,2,1,3,1$，求最大似然估计。提示是取对数后令导数为零。

### 知识点

**参数**决定分布。**似然**固定已观察的数据，把这些数据的概率看成参数的函数。独立同分布（i.i.d.）表示各次独立、概率规则相同。取自然对数 $\ln$ 能把乘积变为和且保持大小顺序，导数衡量曲线斜率。

### 解题讲解

(a) 在独立同分布的观测模型下，序列概率相乘得 $L(\theta)=(\theta/2)^{n_1+n_2}(1-\theta)^{n_3}$。

(b) 计数为 $(3,3,4)$，所以 $\ln L=6\ln(\theta/2)+4\ln(1-\theta)$。导数 $6/\theta-4/(1-\theta)$ 在 $\theta=0.6$ 处为零，左正右负，两端似然均为零，故 $\hat\theta=0.6$。它等于 1 或 2 在样本中出现的比例 $6/10$。

## Question 2

### English question

Consider the following joint distribution over $X$ and $Y$.

| $p(X,Y)$ | $X=1$ | $X=2$ | $X=3$ | $X=4$ |
| --- | ---: | ---: | ---: | ---: |
| $Y=1$ | 0 | 0 | 1/8 | 1/8 |
| $Y=2$ | 1/8 | 1/16 | 1/16 | 0 |
| $Y=3$ | 1/8 | 1/8 | 0 | 0 |
| $Y=4$ | 0 | 1/16 | 1/16 | 1/8 |

- (a) Show that $X$ and $Y$ are not statistically independent. *Hint:* It suffices to find one pair $(x,y)$ for which $p(X=x,Y=y)\ne p(X=x)p(Y=y)$.
- (b) Compute:
  1. $H(X)$
  2. $H(Y)$
  3. $H(X\mid Y)$
  4. $H(Y\mid X)$
  5. $H(X,Y)$

### 中文翻译

联合分布见英文表格。(a) 证明 $X$ 与 $Y$ 不独立。(b) 计算 (i) $H(X)$、(ii) $H(Y)$、(iii) $H(X\mid Y)$、(iv) $H(Y\mid X)$、(v) $H(X,Y)$。

### 知识点

概率 $p$ 的结果有 $-\log_2 p$ bit 的**自信息量**。$\log_2 8=3$ 表示 $2^3=8$。**熵** $H(X)=-\sum_xp(x)\log_2p(x)$ 是平均信息量，零概率项按 0 计。**条件熵**先算每个给定取值下的熵，再按该取值概率平均。**链式法则** $H(X,Y)=H(Y)+H(X\mid Y)$ 来自对 $p(x,y)=p(y)p(x\mid y)$ 取对数并平均。

### 解题讲解

(a) 各行、各列之和都是 $1/4$。左上格是 0，独立时应为 $(1/4)(1/4)=1/16$，因此不独立。

(b) (i)、(ii) 都是 $\log_2 4=2$ bits。(iii) 各行除以 $1/4$ 后得到的熵依次为 $1,1.5,1,1.5$，平均为 $1.25$ bits。(iv) 按列同理，四列熵为 $1,1.5,1.5,1$，平均也是 $1.25$ bits。(v) 全表有六个 $1/8$ 和四个 $1/16$，所以联合熵是 $6(1/8)3+4(1/16)4=3.25$ bits，也等于 $2+1.25$。

## Question 3

### English question

A standard deck of cards contains four suits (♥ hearts, ♦ diamonds, ♣ clubs and ♠ spades), each with 13 values (A, 2, 3, 4, 5, 6, 7, 8, 9, 10, J, Q and K). A, J, Q and K stand for ace, jack, queen and king. Hearts and diamonds are red, and clubs and spades are black. J, Q and K are face cards.

Each of the 52 cards is identified by its value $v$ and suit $s$ and denoted $vs$. For example, 2♥ is the two of hearts, J♣ is the jack of clubs, and 7♠ is the seven of spades. Let $c$ denote a card's colour and let $f=1$ if the card is a face card and $f=0$ otherwise.

A card is drawn at random from a thoroughly shuffled deck. Calculate:

- (a) The information in observing a red king, $h(c=\mathrm{red},v=K)$.
- (b) The conditional information in observing a king given that a face card was drawn, $h(v=K\mid f=1)$.
- (c) The entropies $H(S)$ and $H(V,S)$.

### 中文翻译

一副标准牌有四个花色、每花色 13 个点数。红桃与方块是红色，J、Q、K 是人头牌。均匀抽一张，求 (a) 红色 K 的信息量，(b) 已知是人头牌时抽到 K 的条件信息量，(c) 花色的熵和点数与花色的联合熵。

### 知识点

单个事件的信息量是概率的负对数。给定条件后，要用**条件概率**取负对数。均匀分布在 $m$ 个结果上时，每个结果的信息量相同，熵为 $\log_2 m$。

### 解题讲解

(a) 红色 K 有两张，概率 $2/52$，信息量 $\log_2 26\approx4.7004$ bits。(b) 12 张人头牌中有 4 张 K，信息量 $\log_2 3\approx1.5850$ bits。(c) 花色有四种等可能结果，$H(S)=2$ bits。花色与点数共同指定一张牌，$H(V,S)=\log_2 52\approx5.7004$ bits。

## Question 4

### English question

Let $X$ be a random variable taking a finite number of values. What general inequality relates $H(X)$ and $H(Y)$ if:

- (a) $Y=2^X$?
- (b) $Y=\cos X$?

### 中文翻译

$X$ 只取有限个值。当 (a) $Y=2^X$，(b) $Y=\cos X$ 时，比较 $H(X)$ 与 $H(Y)$。

### 知识点

**确定性函数**让每个输入对应唯一输出，所以 $H(Y\mid X)=0$。若在有正概率的输入上，输出也能唯一反推输入，就叫在该范围内**一一对应**。

### 解题讲解

链式法则给 $H(X)=H(X,Y)=H(Y)+H(X\mid Y)$。由于条件熵非负，$H(Y)\le H(X)$。

(a) $2^X$ 严格递增，可反解 $X=\log_2 Y$，故 $H(Y)=H(X)$。(b) 一般只能保证 $H(Y)\le H(X)$。如 $X$ 等概率取 $-1,1$，余弦相同，熵由 1 bit 变 0。若在实际可能的输入上余弦值互异，则取等号。
