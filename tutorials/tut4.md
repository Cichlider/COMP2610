# Tutorial 4 — Entropy and Information

COMP2610 / COMP6261 Information Theory · Week 4, Semester 2, 2026  
[Original PDF](../tutpdf/tut4.pdf)

## Question 1

### English question

Suppose $Y$ is a geometric random variable with probability mass function

$$
P(Y=y)=p(1-p)^{y-1},\qquad y=1,2,\ldots
$$

Determine the mean and variance of $Y$.

### 中文翻译

$Y$ 是几何随机变量，$P(Y=y)=p(1-p)^{y-1}$，$y=1,2,\ldots$。求 $Y$ 的均值和方差。

### 知识点

**几何分布**记录第一次成功发生在第几次试验。均值 $\mathbb E[Y]$ 是长期平均。方差 $\operatorname{Var}(Y)=\mathbb E[(Y-\mathbb EY)^2]$ 衡量数值偏离均值的程度。

### 解题讲解

设 $q=1-p$。第一次成功时 $Y=1$，失败时已经花掉 1 次，剩余等待时间 $Y'$ 和 $Y$ 同分布。令 $m=\mathbb E[Y]$、$s=\mathbb E[Y^2]$，按首轮结果求平均：
$$
m=p+q(1+m)=1+qm,\qquad
s=p+q(1+2m+s)=1+2qm+qs.
$$
所以 $m=1/p$，$s=(2-p)/p^2$，方差为 $s-m^2=(1-p)/p^2$。当 $p=1$ 时总是一次成功，方差为 0。

## Question 2

### English question

The World Series is a seven-game series that terminates as soon as either team wins four games. Let $X$ represent the outcome of a World Series between teams A and B. Possible values of $X$ include AAAA, BABABAB and BBBAAAA. Let $Y$ be the number of games played, ranging from 4 to 7.

Assuming that A and B are equally matched and that the games are independent, calculate:

- (a) $H(X)$.
- (b) $H(Y)$.
- (c) $H(Y\mid X)$.
- (d) $H(X\mid Y)$.

### 中文翻译

A、B 两队打七局四胜制，任何一队先赢四局就结束。$X$ 是完整胜负序列，例如 AAAA、BABABAB 或 BBBAAAA，$Y$ 是总局数。假设两队等强且各局独立，求 (a) $H(X)$，(b) $H(Y)$，(c) $H(Y\mid X)$，(d) $H(X\mid Y)$。

### 知识点

结束在第 $y$ 局时，最后一局必须由冠军获胜，前 $y-1$ 局恰好已赢 3 局。**条件均匀**表示在同一局数下，所有合法序列等可能。

### 解题讲解

固定 $y$ 有 $M_y=2\binom{y-1}3$ 种序列，依次为 2、8、20、40。每个长度 $y$ 的合法序列概率是 $2^{-y}$，所以 $P(Y=y)$ 依次为 $1/8,1/4,5/16,5/16$。

- (a) 每个序列的信息量为 $y$，因此 $H(X)=\mathbb E[Y]=4/8+5/4+6(5/16)+7(5/16)=5.8125$ bits。
- (b) 对局数分布套用熵公式，得 $H(Y)\approx1.92379$ bits。
- (c) 已知完整序列就知道局数，$H(Y\mid X)=0$。
- (d) $H(X\mid Y)=H(X)-H(Y)\approx3.88871$ bits，也可对 $\log_2 M_y$ 取加权平均。

## Question 3

### English question

Recall that $\operatorname{Var}[X]=\mathbb{E}[X^2]-(\mathbb{E}[X])^2$. Use Jensen's inequality to show that the variance must always be nonnegative.

### 中文翻译

已知 $\operatorname{Var}(X)=\mathbb E[X^2]-(\mathbb E[X])^2$，用 Jensen 不等式证明方差非负。

### 知识点

**凸函数**的图像位于任意两点连成的线段下方。Jensen 不等式是 $f(\mathbb E X)\le\mathbb E[f(X)]$，即凸函数在平均值处的值不超过函数值的平均。

### 解题讲解

取 $f(t)=t^2$，它的二阶导数是 2，故为凸函数。于是 $(\mathbb E[X])^2\le\mathbb E[X^2]$。移项就得 $\operatorname{Var}(X)\ge0$。严格凸性给出等号条件，即 $X$ 几乎必然为常数。

## Question 4

### English question

Let $X$ and $Y$ be independent Bernoulli random variables on $\{0,1\}$ with parameter $\frac12$:

$$
p(X=0)=p(X=1)=\frac12,\qquad
p(Y=0)=p(Y=1)=\frac12.
$$

- (a) Compute $I(X;Y)$.
- (b) Let $Z=X+Y$. Compute $I(X;Y\mid Z)$.
- (c) Do the above quantities contradict the data-processing inequality? Explain your answer.

### 中文翻译

$X,Y$ 是独立且均匀的 0/1 随机变量。(a) 求 $I(X;Y)$。(b) 令 $Z=X+Y$，求 $I(X;Y\mid Z)$。(c) 解释结果是否与数据处理不等式矛盾。

### 知识点

**互信息** $I(X;Y)=H(X)-H(X\mid Y)$ 衡量知道 $Y$ 后平均减少的 $X$ 的不确定性。**条件互信息** $I(X;Y\mid Z)=H(X\mid Z)-H(X\mid Y,Z)$。**数据处理不等式**在 $X\to Y\to Z$（给定 $Y$ 后 $X$、$Z$ 独立）时给出 $I(X;Z)\le I(X;Y)$。

### 解题讲解

(a) 独立时条件分布与原分布相同，所以 $I(X;Y)=0$。

(b) $Z=0,2$ 时 $X$ 已确定。$Z=1$ 时有 $(0,1),(1,0)$ 两种等可能组合，故 $H(X\mid Z)=P(Z=1)\cdot1=1/2$ bit。给定 $Y,Z$ 可算 $X=Z-Y$，所以 $H(X\mid Y,Z)=0$，答案为 $1/2$ bit。

(c) 此处 $Z$ 同时由 $X,Y$ 产生，给定 $Y$ 时 $Z$ 仍依赖 $X$。例如固定 $Y=0$ 有 $Z=X$，因此不满足上述马尔可夫条件。观察和为 1 会让两者互相决定。
