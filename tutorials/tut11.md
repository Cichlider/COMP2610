# Tutorial 11 — Discrete Memoryless Channels

COMP2610 / COMP6261 Information Theory · Semester 2, 2025  
Exercises by Zhifeng Tang, modified by Mohammad Amin Zarrabian and Eric Hall · [Original PDF](../tutpdf/tut11.pdf)

## Exercise 1

### English question

A binary symmetric channel with inputs $\mathcal X=\{0,1\}$ and outputs $\mathcal Y=\{0,1\}$ has transition matrix

$$
Q=\begin{pmatrix}
1-q & q\\
q & 1-q
\end{pmatrix}.
$$

- (a) Find the mutual information $I(X;Y)$ between the input and output for a general input distribution $p_X=(p,1-p)^{\mathsf T}$. Show that the channel capacity is $C=1-H_2(q)$ bits.
- (b) What is the lowest upper bound on the achievable rates over this channel if we are willing to accept an error probability of 5%?

### 中文翻译

二元对称信道的输入、输出均为 0 或 1，转移矩阵见英文题目。(a) 输入分布为 $(p,1-p)$，求互信息并证明容量是 $1-H_2(q)$。(b) 如果允许 5% 的错误概率，求可达码率的最紧上界。

### 知识点

**二元对称信道（BSC）**以相同概率 $q$ 翻转 0 和 1。$h_2(p)=-p\log_2p-(1-p)\log_2(1-p)$ 是二元熵，原题写作 $H_2(p)$。**码率**以每次使用信道传送的信息比特数计。要区分信道本身的翻转概率、译码后的逐位错误率和整块错误率。

### 解题讲解

(a) $P(Y=0)=p(1-q)+(1-p)q=q+p(1-2q)$。因此 $I(X;Y)=h_2(q+p(1-2q))-h_2(q)$。均匀输入使第一个熵取到最大值 1，故 $C=1-h_2(q)$。

(b) 若 5% 指独立均匀消息位的平均译码错误率 $e$，二元 Fano 不等式给 $H(M_i\mid\hat M_i)\le h_2(e_i)$。对 $k$ 个消息位相加并用凹性平均，得 $H(M\mid\hat M)\le kh_2(e)$。传 $k$ 位用 $n$ 次信道，则 $k[1-h_2(e)]\le I(M;\hat M)\le nC$，故 $R\le[1-h_2(q)]/[1-h_2(0.05)]$，分母约 $0.713603$。这是该错误模型下的标准上界。

若 5% 指**整块**错误率，渐近强逆定理给固定错误率小于 1 时的容量上界 $R\le C$。若 5% 指信道翻转率本身，则代入 $q=0.05$，容量约为 $0.71360$ bit/次。原题未进一步指定错误率含义与块长。

## Exercise 2

### English question

A binary erasure channel with inputs $\mathcal X=\{0,1\}$ and outputs $\mathcal Y=\{0,e,1\}$ has transition matrix

$$
Q=\begin{pmatrix}
1-q & 0\\
q & q\\
0 & 1-q
\end{pmatrix}.
$$

- (a) Find the mutual information $I(X;Y)$ between the input and output for a general input distribution $p_X=(p,1-p)$. Show that the channel capacity is $C=1-q$ bits.
- (b) What is the lowest upper bound on the achievable rates over this channel if we are willing to accept an error probability of 25%?
- (c) What is the lowest upper bound on the achievable rates over this channel if we are willing to accept an error probability of 50%?

### 中文翻译

二元擦除信道的输入为 0 或 1，输出为 0、擦除符号 $e$ 或 1。(a) 求输入分布 $(p,1-p)$ 时的互信息，并证明容量为 $1-q$。(b) 允许 25% 错误概率时求码率上界。(c) 将允许的错误概率改成 50%。

### 知识点

**二元擦除信道（BEC）**未擦除时能完全恢复输入。擦除本身与输入独立，因此观察到 $e$ 时，对输入仍有原本的不确定性。逐位错误约束下，用上一题的 Fano 上界。

### 解题讲解

(a) $H(X\mid Y)=q h_2(p)$，所以 $I(X;Y)=(1-q)h_2(p)$，在 $p=1/2$ 时达到 $C=1-q$。

(b) 若指平均消息位错误率，$R\le(1-q)/[1-h_2(0.25)]\approx(1-q)/0.188722$。

(c) 若平均位错误率允许 $0.5$，独立均匀消息位可直接猜测达到该错误率，此条件不给出有限的码率上界。若 (b)、(c) 指固定**整块**错误率，渐近上界均为 $1-q$。若 25%、50% 指信道擦除率 $q$，对应容量为 $0.75$、$0.50$ bit/次。

## Exercise 3

### English question

Consider a channel with inputs $\mathcal X=\{a,b,c\}$, outputs $\mathcal Y=\{a,b,c,d\}$ and transition matrix

$$
Q=\begin{pmatrix}
\frac34 & \frac14 & 0\\
\frac14 & \frac12 & \frac14\\
0 & \frac14 & \frac12\\
0 & 0 & \frac14
\end{pmatrix}.
$$

- (a) Assuming $p_X=\left(\frac14,\frac14,\frac12\right)^{\mathsf T}$, what is the mutual information $I(X;Y)$ between the input and output?
- (b) Suppose we send an input drawn from the same distribution over the channel and decode $y$ to the input $x$ that maximises $P(Y=y\mid X=x)$. What is the average probability of error?
- (c) Calvin claims to have constructed a block code for $Q$ with a rate of 0.01 and a bit error probability of 1%. Is his claim possible? Justify your answer.
- (d) Hobbes claims to have constructed a block code for $Q$ with a rate of 100 and a bit error probability of 1%. Is his claim possible? Justify your answer.

### 中文翻译

三种输入 $a,b,c$、四种输出 $a,b,c,d$ 的信道矩阵见英文题目。输入概率为 $(1/4,1/4,1/2)$。(a) 求互信息。(b) 收到 $y$ 后选择使 $P(y\mid x)$ 最大的 $x$，求平均错误率。(c) 码率 0.01 且位错误率 1% 是否可能？(d) 码率改成 100 呢？

### 知识点

**最大似然（ML）译码**比较各个输入产生所见输出的概率。**最大后验（MAP）译码**比较 $P(x)P(y\mid x)$。平均错误率等于 1 减去所有正确译码情形的联合概率。编码定理说低于容量的码率可随块长增加使错误概率任意小。

### 解题讲解

- (a) 用矩阵乘输入概率列向量，输出分布为 $(1/4,5/16,5/16,1/8)$。三列的熵分别为 $h_2(1/4),1.5,1.5$。所以 $I=H(Y)-\tfrac14h_2(1/4)-\tfrac34(1.5)\approx0.59598$ bit/次。
- (b) 对 $a,b,c,d$，ML 分别选 $a,b,c,c$。正确概率是 $\tfrac14\tfrac34+\tfrac14\tfrac12+\tfrac12\tfrac12+\tfrac12\tfrac14=11/16$，错误概率为 $5/16$。
- (c) 容量至少是 (a) 取到的 $0.59598$，所以码率 $0.01$ 低于容量，足够长的码可以达到不高于 1% 的位错误率。
- (d) $C\le\log_2 3$。允许 1% 平均消息位错误时，Fano 界也只给 $R\le\log_2 3/[1-h_2(0.01)]\approx1.7243$ bit/次，因此 100 不可能。

## Exercise 4

### English question

Find the capacity of the discrete memoryless channel $Y=X+Z$, where $P(Z=0)=P(Z=a)=\frac12$ and $X$ takes values in $\{0,1\}$. Assume $X$ is independent of $Z$. The parameter $a$ can be any integer, so $Y$ can take integer values outside $\{0,1\}$.

### 中文翻译

输入 $X\in\{0,1\}$ 与独立噪声 $Z$ 相加得到 $Y$，噪声以相同概率取 0 或整数 $a$。求容量。

### 知识点

分别列出每个输入可能产生的输出。输出集合重叠时，接收方可能无法区分输入。若 $a=0$，题干中两个噪声取值重合，按等概率选两个加数的生成过程理解，此时 $Z$ 恒为零。

### 解题讲解

$X=0$ 的输出集合为 $\{0,a\}$，$X=1$ 的输出集合为 $\{1,1+a\}$。

- 当 $a=1$ 或 $a=-1$ 时两集合恰有一个共同输出，共同输出对于两个输入都以 $1/2$ 的概率发生，相当于擦除概率为 $1/2$ 的 BEC，故 $C=1/2$ bit/次。
- 其他整数 $a$ 下两个集合不相交，输出能唯一确定输入。均匀输入使 $I=H(X)=1$ bit/次，因此 $C=1$。
