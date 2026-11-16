# Tutorial 1 — Elementary Probability

COMP2610 / COMP6261 Information Theory · Week 1, Semester 2, 2023  
[Original PDF](../tutpdf/tut1.pdf)

## Question 1

### English question

A spinner is divided into five equal sections, labelled 1, 2, 3, 4 and 5. Compute the probability of:

- (a) Spinning a 4.
- (b) Spinning an even number.
- (c) Spinning a prime number.

### 中文翻译

一个转盘有五个等大的区域，编号 1 至 5。分别求转到 (a) 4、(b) 偶数、(c) 质数的概率。

### 知识点

**样本空间**是所有可能结果的集合。**事件**是其中我们关心的一组结果。若每个基本结果等可能，事件的概率等于符合条件的结果数除以总结果数。质数是大于 1 且只有 1 和自身两个正因数的整数。

### 解题讲解

五格等大，每个编号的概率是 $1/5$。(a) 只有 4，得 $1/5$。(b) 有 2 和 4，得 $2/5$。(c) 有 2、3、5，得 $3/5$。

## Question 2

### English question

Assume that ACT number plates have three letters followed by three digits, such as YOA077. What is the probability that a randomly chosen plate starts with ACT and ends in 7 (ACT##7)?

### 中文翻译

假设 ACT 车牌由三个字母加三个数字组成，例如 YOA077。随机选一张车牌，求它以 ACT 开头、以 7 结尾（ACT##7）的概率。

### 知识点

**乘法计数原理**把各位置可选数量相乘。题目按字母与数字可重复、所有合规组合等可能的模型计算。

### 解题讲解

总共有 $26^3\times10^3$ 种。固定 A、C、T 和最后的 7，中间两个数字各有 10 种选法。概率为 $10^2/(26^3\times10^3)=1/175760$。

## Question 3

### English question

The ACT Government plans to enforce speed limits during the morning rush hour on four routes into the city. The speed traps on routes A, B, C and D operate 40%, 30%, 20% and 30% of the time, respectively. Arya always speeds to work and uses those routes with probabilities 0.2, 0.1, 0.5 and 0.2, respectively. Compute the probability of:

- (a) Arya getting a ticket on any one morning.
- (b) Arya going five mornings without a ticket.

### 中文翻译

政府在通往市区的 A、B、C、D 四条路设测速点，启用率依次为 40%、30%、20%、30%。Arya 每天超速通勤，走这四条路的概率依次为 0.2、0.1、0.5、0.2。求 (a) 某天收到罚单的概率，(b) 连续五天没收到罚单的概率。

### 知识点

$P(T\mid A)$ 是已知走 A 时被罚的概率。交集满足 $P(A\cap T)=P(A)P(T\mid A)$。路线互斥且覆盖所有情况，故可将各路线的交集概率相加，这就是**全概率公式**。**补事件**的概率是 $1-P(T)$。独立事件同时发生的概率是各概率的乘积。

### 解题讲解

(a) 按题意将各路线的启用率视为走该路线时被罚的概率。$P(T)=0.2(0.4)+0.1(0.3)+0.5(0.2)+0.2(0.3)=0.27$。

(b) 假设每天的情况独立且概率相同，每天不被罚的概率为 $0.73$，五天都不被罚的概率为 $0.73^5\approx0.20731$。

## Question 4

### English question

An urn contains five blue, three red and two yellow marbles. If you draw three marbles, what is the probability that fewer than two are red if:

- (a) The marbles are drawn with replacement.
- (b) The marbles are drawn without replacement.

### 中文翻译

罐里有 5 颗蓝球、3 颗红球和 2 颗黄球。抽三次，求抽到的红球少于两颗的概率，分别考虑 (a) 放回，(b) 不放回。

### 知识点

**二项分布**计数 $n$ 次独立试验中成功的次数。每次成功概率为 $p$ 时，恰好 $k$ 次的概率是 $\binom nkp^k(1-p)^{n-k}$。组合数 $\binom nk$ 表示从 $n$ 个不同对象里选 $k$ 个，忽略顺序。不放回时可按等可能的无序子集计数。

### 解题讲解

(a) 0 颗红球的概率为 $0.7^3$。恰好 1 颗有 3 种出现位置，概率为 $3(0.3)(0.7)^2$。相加得 $0.784$。

(b) 分母是所有三球子集 $\binom{10}3=120$。分子是选三个非红球，或选一个红球加两个非红球。得 $(\binom73+\binom31\binom72)/120=49/60\approx0.81667$。

## Question 5

### English question

Nick will miss an important cricket match while taking his Information Theory exam, so he sets both VCRs to record it. The first VCR has a 70% chance of recording the match successfully, and the second has a 60% chance. Assume that the two events $A$ and $B$ are independent, with $P(A)=0.7$, $P(B)=0.6$, $P(A^c)=0.3$ and $P(B^c)=0.4$.

What is the probability that he gets home after the exam and finds:

- (a) No copies of the match?
- (b) One copy of the match?
- (c) Two copies of the match?

### 中文翻译

Nick 考试期间让两台录像机录比赛，成功概率分别为 0.7、0.6，录制是否成功相互独立。求回家发现 (a) 0 份，(b) 1 份，(c) 2 份录像的概率。

### 知识点

**独立**表示知道一台的结果不改变另一台的成功率。**互斥**表示两件事无法同时发生，互斥情形的概率直接相加。

### 解题讲解

(a) 两台都失败，$0.3\cdot0.4=0.12$。(b) 仅第一台成功或仅第二台成功，$0.7\cdot0.4+0.3\cdot0.6=0.46$。(c) 两台都成功，$0.7\cdot0.6=0.42$。三项之和为 1。
