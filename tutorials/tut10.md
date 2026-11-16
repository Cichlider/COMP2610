# Tutorial 10 — Channel Capacity

COMP2610 / COMP6261 Information Theory · Semester 2, 2025  
Exercises by Manish Kumar and Mohammad Amin Zarrabian, edited by Eric Hall · [Original PDF](../tutpdf/tut10.pdf)

## Exercise 1 — Channel Capacity

### English question

Consider the discrete memoryless channel $Y=X+Z\pmod{11}$, where the input $X$ and output $Y$ take integer values in $\{0,1,2,\ldots,10\}$. The noise $Z$ takes each of the values 1, 2 and 3 with probability $\frac13$. Assume $Z$ is independent of $X$.

- (a) Find the capacity.
- (b) What is the maximizing $p^\star(x)$?

### 中文翻译

无记忆信道满足 $Y=(X+Z)\bmod11$，输入和输出为 0 至 10，噪声 $Z$ 独立于 $X$，均匀取 1、2、3。(a) 求容量。(b) 找到使互信息最大的输入分布。

### 知识点

**离散无记忆信道**的每次输出只依赖当次输入，给定输入序列时各次输出独立。**容量** $C=\max_{p_X}I(X;Y)$，单位为 bit/次。模 11 加法超出 10 时按 11 回绕。

### 解题讲解

固定 $X=x$ 只会把噪声的三个可能输出平移，所以 $H(Y\mid X)=H(Z)=\log_2 3$。$H(Y)\le\log_2 11$。取 $P(X=x)=1/11$ 时，每种噪声平移后仍均匀，故输出也均匀并达到上界。答案 $C=\log_2(11/3)\approx1.87447$ bit/次，均匀输入可达。

## Exercise 2 — Erasures and Errors in a Binary Channel

### English question

Consider a channel with binary inputs that has both erasures and errors. The probability of error is $\epsilon$ and the probability of erasure is $\alpha$. The PDF's channel diagram gives the following transition probabilities.

| Input | Output $0$ | Erasure $e$ | Output $1$ |
| --- | ---: | ---: | ---: |
| $0$ | $1-\alpha-\epsilon$ | $\alpha$ | $\epsilon$ |
| $1$ | $\epsilon$ | $\alpha$ | $1-\alpha-\epsilon$ |

- (a) Find the capacity of this channel.
- (b) Specialise to the binary symmetric channel ($\alpha=0$).
- (c) Specialise to the binary erasure channel ($\epsilon=0$).

### 中文翻译

二元输入信道可误码或擦除。擦除概率为 $\alpha$、翻转概率为 $\epsilon$、正确概率为 $1-\alpha-\epsilon$。(a) 求容量。(b) 令 $\alpha=0$ 得到二元对称信道。(c) 令 $\epsilon=0$ 得到二元擦除信道。

### 知识点

**擦除**表示接收方知道本次输出缺失。**翻转**表示输出变成另一个比特。给定未擦除时，翻转条件概率为 $q=\epsilon/(1-\alpha)$。$h_2(q)=-q\log_2 q-(1-q)\log_2(1-q)$ 是两种结果概率为 $q,1-q$ 时的熵，零概率项按 0 计。

### 解题讲解

(a) 当 $\alpha<1$，令 $E$ 表示是否擦除。$E$ 独立于 $X$，且能从 $Y$ 判断。用互信息链式法则，$I(X;Y)=(1-\alpha)I(X;Y\mid E=0)$，因为擦除时输出恒定。未擦除分支是翻转率 $q$ 的二元对称信道，条件输出熵为 $h_2(q)$，而输出熵最多 1，均匀输入达到。故 $C=(1-\alpha)[1-h_2(\epsilon/(1-\alpha))]$。当 $\alpha=1$，容量为 0。

(b) $C=1-h_2(\epsilon)$。(c) $C=1-\alpha$。

## Exercise 3 — Binary Multiplier Channel

### English question

Consider the channel $Y=XZ$, where $X$ and $Z$ are independent binary random variables taking values 0 and 1. Let $Z$ be Bernoulli($\alpha$), so $P(Z=1)=\alpha$.

- (a) Find the capacity of this channel and the maximizing distribution on $X$.
- (b) Suppose the receiver can observe $Z$ as well as $Y$. What is the capacity?

### 中文翻译

$X,Z$ 是独立的二元变量，$Y=XZ$，$P(Z=1)=\alpha$。(a) 求容量与最优输入分布。(b) 若接收者还能看到 $Z$，容量是多少？

### 知识点

这个信道的错误只有一种方向，$X=0$ 永远输出 0，而 $X=1$ 才可能被乘成 0。令 $p=P(X=1)$，用 $I(X;Y)=H(Y)-H(Y\mid X)$ 求容量。

### 解题讲解

(a) $P(Y=1)=\alpha p$，因此 $I=h_2(\alpha p)-p h_2(\alpha)$。对 $p$ 求导得 $\alpha\log_2[(1-\alpha p)/(\alpha p)]-h_2(\alpha)$。当 $0<\alpha\le1$，凹性给出最大值点
$$
p^*=\frac1{\alpha(1+2^{h_2(\alpha)/\alpha})},\qquad
C=\log_2(1+2^{-h_2(\alpha)/\alpha}).
$$
代回可验证右式。当 $\alpha=0$，输出恒为 0，容量为 0。

(b) $I(X;Y,Z)=I(X;Z)+I(X;Y\mid Z)=0+\alpha H(X)$。$Z=0$ 时输出无信息，$Z=1$ 时 $Y=X$。均匀输入使 $H(X)=1$，所以容量为 $\alpha$。

## Exercise 4 — Can Signal Alternatives Lower Capacity?

### English question

Show that adding a column to a channel transition matrix does not decrease capacity.

### 中文翻译

证明给信道转移矩阵增加一列不会降低容量。

### 知识点

按本课程的列向量约定，一列是给定某个输入时各输出的条件概率。加一列表示增加一种可用输入符号，原有条件分布继续适用。

### 解题讲解

新信道可把新增输入的概率设为 0，再使用原信道的最优输入分布。这样得到的输入输出联合分布及互信息与原信道相同。由于新容量还可以在更多输入分布上取最大值，$C_{\mathrm{new}}\ge C_{\mathrm{old}}$。
