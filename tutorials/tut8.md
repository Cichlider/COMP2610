# Tutorial 8 — Huffman Codes

COMP2610 / COMP6261 Information Theory  
Mohammad Amin Zarrabian · [Original PDF](../tutpdf/tut8.pdf)

## Question 1 — Bad Codes

### English question

Which of these codes cannot be Huffman codes for any probability assignment?

- (a) {`0`, `10`, `11`}
- (b) {`00`, `01`, `10`, `110`}
- (c) {`01`, `10`}

### 中文翻译

判断以下哪几组码无论如何分配概率都无法成为二元 Huffman 码。(a) {0, 10, 11}。(b) {00, 01, 10, 110}。(c) {01, 10}。

### 知识点

**前缀码**中没有码字是另一码字的开头，因此可从左到右即时解码。二元 Huffman 算法每次合并两个最小权重，得到每个内部节点都有两个子节点的树。这样的树满足 **Kraft 等式** $\sum_i2^{-l_i}=1$，其中 $l_i$ 是码长。

### 解题讲解

(a) 可以，例如概率 $(0.5,0.3,0.2)$，先合并后两项，再分别分配给 10、11。(b) Kraft 和为 $3/4+1/8=7/8$，树上 11 的分支只有一个孩子。(c) Kraft 和为 $1/2$，两个符号的 Huffman 树直接用 0 和 1。因此不能的是 (b)、(c)。

## Question 2 — Optimal Code Lengths That Require One Bit Above Entropy

### English question

The source coding theorem shows that the optimal code for a random variable $X$ has expected length less than $H(X)+1$. Give an example of a random variable for which the expected length of the optimal code is close to $H(X)+1$. In other words, for any $\epsilon>0$, construct a distribution for which the optimal code has $L>H(X)+1-\epsilon$.

### 中文翻译

信源编码定理给出最优平均码长 $L<H(X)+1$。构造一个例子使这个差距任意接近 1，即对任意 $\epsilon>0$，使 $L>H(X)+1-\epsilon$。

### 知识点

二元前缀码的长度是整数。两个概率都为正的符号必须可区分，最短可分别分配 0、1，因此平均长恒为 1 bit。**二元熵函数**记作 $h_2(p)=-p\log_2p-(1-p)\log_2(1-p)$。

### 解题讲解

取分布 $(1-\delta,\delta)$，$0<\delta<1/2$。$L=1$，而当 $\delta$ 趋近 0 时 $H(X)=h_2(\delta)\to0$。给定 $\epsilon$，选足够小的正 $\delta$ 使 $H(X)<\epsilon$，就有 $L>H(X)+1-\epsilon$。

## Question 3 — Huffman Codes

### English question

- (a) Construct a binary Huffman code for the distribution $\mathbf p=(0.3,0.3,0.2,0.1,0.1)$ on five symbols. What is the average length of this code?
- (b) Construct a probability distribution $\mathbf p'$ on five symbols for which the code from part (a) has average length, under $\mathbf p'$, equal to its entropy $H(\mathbf p')$.

### 中文翻译

(a) 为五个概率为 $(0.3,0.3,0.2,0.1,0.1)$ 的符号构造二元 Huffman 码，并求平均长。(b) 找另一组概率，使同一个码在新分布下的平均长等于熵。

### 知识点

每次合并当前两个最小权重，节点权重为两者之和。给左右边标 0 与 1，沿根到叶读取码字。如果完整二叉树的码长为 $l_i$，令 $p_i'=2^{-l_i}$，则这些概率和为 1，而且 $-\log_2p_i'=l_i$。

### 解题讲解

(a) 合并次序为 $0.1+0.1=0.2$，$0.2+0.2=0.4$，$0.3+0.3=0.6$，最后 $0.4+0.6=1$。一组码字依次为 **00、01、10、110、111**。平均长为 $2(0.8)+3(0.2)=2.2$ bits。

(b) 取 $(1/4,1/4,1/4,1/8,1/8)$，则每项自信息恰好等于相应码长，平均长和熵都为 $2.25$ bits。

## Question 4 — Optimal Codes

### English question

Let $l_1,l_2,\ldots,l_{10}$ be the binary Huffman codeword lengths for the probabilities $p_1\ge p_2\ge\cdots\ge p_{10}$. Suppose we get a new distribution by splitting the last probability mass. What can you say about the optimal binary codeword lengths $\tilde l_1,\tilde l_2,\ldots,\tilde l_{11}$ for the probabilities

$$
p_1,p_2,\ldots,p_9,\alpha p_{10},(1-\alpha)p_{10},
\qquad 0\le\alpha\le 1?
$$

### 中文翻译

原有十个降序概率 $p_1\ge\cdots\ge p_{10}$，一组最优二元 Huffman 码长为 $l_1,\ldots,l_{10}$。将最后一项拆成 $\alpha p_{10}$ 和 $(1-\alpha)p_{10}$，其中 $0\le\alpha\le1$。新分布的最优码长有什么关系？

### 知识点

**最优子结构**是指在合并两个最低概率后，可以先求缩小问题的最优树，再把合并的叶子拆开。并列概率时可能有多套同样最优的树。

### 解题讲解

两项新概率都不超过 $p_{10}$，可选为最先合并的一对，合并后问题回到原来的十项。因此有一组最优码保留前九项长度，拆出的两个符号各用 $l_{10}+1$ 位。平均长度增加 $p_{10}$。若 $\alpha=0$ 或 1 且仍要求为零概率符号分配码字，上述构造仍可用。若移除零概率符号，则直接回到原分布。
