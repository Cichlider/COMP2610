# Tutorial 9 — Shannon and Huffman Codes

COMP2610 / COMP6261 Information Theory  
Zhifeng Tang · [Original PDF](../tutpdf/tut9.pdf)

## Question 1 — Shannon Codes and Huffman Codes

### English question

Consider a random variable $X$ that takes four values with probabilities $\left(\frac13,\frac13,\frac14,\frac1{12}\right)$.

- (a) Construct a Huffman code for $X$.
- (b) Show that there are two different sets of optimal codeword lengths. In particular, show that the assignments $(1,2,3,3)$ and $(2,2,2,2)$ are both optimal.
- (c) Conclude that there are optimal codes with codeword lengths for some symbols that exceed the Shannon code length $\left\lceil\log\frac1{p(x)}\right\rceil$.

### 中文翻译

$X$ 有四个取值，概率为 $(1/3,1/3,1/4,1/12)$。(a) 构造 Huffman 码。(b) 证明 $(1,2,3,3)$ 和 $(2,2,2,2)$ 都是最优码长。(c) 说明最优码某些符号的长度可以超过 Shannon 码长 $\lceil\log_2(1/p(x))\rceil$。

### 知识点

Huffman 算法最小化**平均**码长，合并权重相同时可有多个选择。$\lceil u\rceil$ 表示向上取整。

### 解题讲解

(a) 先合并 $1/12+1/4=1/3$，此时三个节点权重都为 $1/3$。把合并节点与第二个原符号合并，可以得到 **0、10、110、111**。

(b) 若第二步合并的是前两个原符号，得到 **00、01、10、11**。两套都来自 Huffman 算法且平均长都是 2 bits。

(c) 第三个符号概率 $1/4$，Shannon 长度为 2。在第一套最优码里它占 3 位。

## Question 2 — Huffman Code

### English question

Consider a random variable $X$ with probabilities

$$
p=\left(\frac1{21},\frac2{21},\frac3{21},\frac4{21},\frac5{21},\frac6{21}\right).
$$

- (a) Find a binary Huffman code for $X$.
- (b) Find a ternary Huffman code for $X$.
- (c) Calculate $L=\sum_i p_i l_i$ in each case.

### 中文翻译

对概率 $(1,2,3,4,5,6)/21$ 的六个符号，求 (a) 二元 Huffman 码，(b) 三元 Huffman 码，(c) 两种码的平均长度。

### 知识点

**三元前缀码**用 0、1、2，每轮合并三个最低权重。完整三叉树的叶子数为奇数，六个实际符号可添加一个权重 0 的虚拟叶，最后去掉其码字。三元平均码长以三元符号为单位。

### 解题讲解

(a) 用未归一化权重合并 $1+2=3$、$3+3=6$、$4+5=9$、$6+6=12$、$9+12=21$。按原顺序，一组码是 **1110、1111、110、00、01、10**，长度为 $(4,4,3,2,2,2)$。

(b) 合并 $0+1+2=3$，再合并 $3+3+4=10$，最后 $5+6+10=21$。一组码是 **201、202、21、22、0、1**，长度为 $(3,3,2,2,1,1)$。

(c) 二元平均长 $51/21=17/7$ bits，三元平均长 $34/21$ 个三元符号。

## Question 3 — Data Compression

### English question

Find an optimal set of binary codeword lengths $l_1,l_2,\ldots$ for an instantaneous code for each of the following probability mass functions. Minimise $\sum_i p_i l_i$.

- (a) $\mathbf p=\left(\frac{10}{41},\frac9{41},\frac8{41},\frac7{41},\frac7{41}\right)$
- (b) $\mathbf p=\left(\frac9{10},\left(\frac9{10}\right)\left(\frac1{10}\right),\left(\frac9{10}\right)\left(\frac1{10}\right)^2,\left(\frac9{10}\right)\left(\frac1{10}\right)^3,\ldots\right)$

### 中文翻译

为以下分布寻找使平均码长最小的即时二元码长。(a) $(10,9,8,7,7)/41$。(b) 第 $i$ 个概率为 $0.9(0.1)^{i-1}$，$i=1,2,\ldots$。

### 知识点

**即时码**可以在完整码字到达时立即识别，下文使用前缀树。几何分布去掉首项并将尾部重新归一化，会得到原来的形状。

### 解题讲解

(a) 合并 $7+7=14$、$8+9=17$、$10+14=24$、$17+24=41$，按原顺序的最优长度为 $(2,2,2,3,3)$，平均为 $96/41$ bits。

(b) 一组最优码是 **0、10、110、1110、…**，长度 $l_i=i$，平均长为 $1/0.9=10/9$。证明可设最优平均长度的下确界为 $L_*$。若第一项的码长至少为 2，它单独贡献至少 $1.8>10/9$。因此求下确界可只考虑第一项长度为 1 的树。其余符号共用另一侧，去掉共同的首位后，条件分布和原分布相同，故 $L_*\ge1+0.1L_*$，即 $L_*\ge10/9$。构造的码达到下界。

## Question 4 — Shannon Code

### English question

Consider the following method for generating a code for a random variable $X$ that takes $m$ values $\{1,2,\ldots,m\}$ with probabilities $p_1,p_2,\ldots,p_m$. Assume that $p_1\ge p_2\ge\cdots\ge p_m$. Define

$$
F_i=\sum_{k=1}^{i-1}p_k,
$$

the sum of the probabilities of all symbols less than $i$. The codeword for $i$ is the number $F_i\in[0,1]$ rounded off to $l_i$ bits, where $l_i=\left\lceil\log\frac1{p_i}\right\rceil$.

- (a) Show that the code constructed by this process is prefix-free and that the average length satisfies

  $$
  H(X)\le L<H(X)+1.
  $$

- (b) Construct the code for the probability distribution $(0.5,0.25,0.125,0.125)$.

### 中文翻译

将符号按概率降序排列，令 $F_i=\sum_{k<i}p_k$，把它的二进制小数保留前 $l_i=\lceil\log_2(1/p_i)\rceil$ 位作为码字。(a) 证明前缀性质和 $H(X)\le L<H(X)+1$。(b) 编码分布 $(0.5,0.25,0.125,0.125)$。

### 知识点

原文 “rounded off” 在 Shannon 编码这里按**截取前若干位**理解。取前 $l_i$ 位等价于选择包含 $F_i$、长度 $2^{-l_i}$ 的二进制网格区间。较短的码字是另一串的前缀时，后者的网格区间会被前者包含。

### 解题讲解

(a) 对 $i<j$，降序概率给 $l_i\le l_j$，而 $F_j-F_i\ge p_i\ge2^{-l_i}$。两点不能落在同一个长度 $2^{-l_i}$ 的网格区间，因此 $j$ 的前 $l_i$ 位不会等于 $i$ 的码字。对 $-\log_2p_i\le l_i<-\log_2p_i+1$ 按 $p_i$ 加权，即得平均长度的界。

(b) 累积值为 $0,1/2,3/4,7/8$，长度为 $1,2,3,3$。截取后为 **0、10、110、111**。
