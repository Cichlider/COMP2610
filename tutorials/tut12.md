# Tutorial 12 — Hamming Codes and Arithmetic Coding

COMP2610 / COMP6261 Information Theory · Semester 2, 2025  
Exercises by Eric Hall · [Original PDF](../tutpdf/tut12.pdf)

## Exercise 1 — Hamming Codes

### English question

- (a) Encode the string `0111` using the $(7,4)$ Hamming code.
- (b) Decode the string `1100000` using the $(7,4)$ Hamming code, referring to the Venn diagram.
- (c) What is the syndrome of `1100000`?
- (d) What is the maximum number of bit flips that the $(7,4)$ Hamming code can guarantee it can correct? For an initial message with the same number of input bits, how many bits would an $n$-repetition code need to send to guarantee correction of the same number of bit flips?

> The Venn diagram mentioned in part (b) is absent from the PDF.

### 中文翻译

(a) 用 $(7,4)$ 汉明码编码 0111。(b) 参考维恩图解码 1100000。(c) 求 1100000 的校验综合。(d) $(7,4)$ 汉明码保证能纠正几位翻转？对同样长度的原消息，要达到相同纠错保证，重复码需要发送几位？

### 知识点

**汉明码**用 3 个校验位保护 4 个数据位。原 PDF 没附维恩图，以下采用常见的偶校验约定。位置 1、2、4 放校验位，3、5、6、7 放数据位。三个校验集合为 $\{1,3,5,7\}$、$\{2,3,6,7\}$、$\{4,5,6,7\}$。每组的 XOR 应为 0。**校验综合**记录失败的校验组，按 $(s_4s_2s_1)$ 排列时可读成单个错误的位置。

### 解题讲解

(a) 将 0111 放在 3、5、6、7。要使各组偶校验，得到 $(p_1,p_2,p_4)=(0,0,1)$，码字是 **0001111**。

(b) 1100000 的校验失败位置权重为 1 和 2，因此第 3 位有误。翻转后码字为 **1110000**，取出数据位得到 **1000**。

(c) 校验综合 $(s_4s_2s_1)=\mathbf{011}$。按 $(s_1s_2s_4)$ 书写时为 110，含义相同。若课堂维恩图采用不同位序，具体码字和综合需按该位序重算。

(d) 最小汉明距离 3，任意两个合法码字至少差 3 位。每个码字周围一位错误的范围互不重叠，因此保证纠正 1 位。每个数据位重复 3 次、按多数译码也可保证纠正 1 位翻转，4 位共发 $4\times3=12$ 位。

## Exercise 2 — Arithmetic Coding

### English question

Suppose we want to encode a sequence of zeroes and ones using arithmetic coding. The input sequence starts with 0 or 1 with probability $\frac12$ each. After the first symbol, the next symbol is the same as the previous one with probability $\frac35$, different with probability $\frac15$, or the string terminates with probability $\frac15$.

- (a) Encode the string `011` using arithmetic coding.
- (b) Decode the string you encoded in part (a).
- (c) Choose your own string to encode and decode.

### 中文翻译

用算术编码表示 0/1 串。起始符号 0、1 各有 $1/2$ 概率，此后重复前一符号的概率为 $3/5$，改变为 $1/5$，结束为 $1/5$。(a) 编码 011。(b) 解码刚得到的结果。(c) 自选一串并完成编码与解码。

### 知识点

**算术编码**从半开区间 $[0,1)$ 开始，按当前模型的概率划分子区间，每读一个符号就缩小到对应子区间。取一个整个落在最终区间里的二进制网格区间来传输。以下按 **0、1、EOS** 的次序划分，EOS 表示串结束。二进制串 010 表示区间 $[2/8,3/8)$，其宽度为 $2^{-3}$。

### 解题讲解

(a) 编码 011 后还要处理 EOS：
$$
[0,1)\xrightarrow{0}[0,0.5)
\xrightarrow{1}[0.3,0.4)
\xrightarrow{1}[0.32,0.38)
\xrightarrow{\mathrm{EOS}}[0.368,0.38).
$$
可用 **01011111**，其网格区间 $[95/256,96/256)$ 完全落在最终区间内。

(b) 取 $95/256=0.37109375$ 作为代表值。在各层它依次落在上述 0、1、1、EOS 子区间，恢复 **011**。

(c) 选 **0**。区间先变为 $[0,0.5)$，EOS 子区间为 $[0.4,0.5)$。传 **0111**，其网格区间为 $[7/16,8/16)$。代表值 $7/16$ 先落入 0，再落入 EOS，所以解出 **0**。

## Exercise 3 — Arithmetic Coding with Adaptive Distributions

### English question

- (a) Why might we want to use an adaptive distribution?
- (b) What is the intuition behind what the Dirichlet distribution represents?
- (c) Suppose the alphabet consists of `a`, `b` and `c`, and the end-of-stream symbol has probability $\frac14$. In the Dirichlet distribution, `a`, `b` and `c` have virtual counts of 3, 1 and 1, respectively. Encode the string `bb` using arithmetic coding with adaptive probabilities.
- (d) Decode the string obtained in part (c).

### 中文翻译

(a) 为什么使用自适应分布？(b) Dirichlet 分布直观上代表什么？(c) 字母表为 a、b、c，EOS 概率固定为 $1/4$，虚拟计数分别为 3、1、1。用自适应算术编码表示 bb。(d) 解码得到的码串。

### 知识点

**自适应模型**在观察符号后更新概率。**Dirichlet 分布**是对「一组概率本身可能取哪些值」的分布。其参数可当作初始计数，观察到某符号就给它加一，预测概率等于更新后该项占总计数的比例。EOS 固定占 $1/4$，所以 a、b、c 按计数瓜分其余 $3/4$。

### 解题讲解

(a) 源概率未知或局部频率有变化时，可以边编码边学习，使常见符号分得更宽的区间。编码端和解码端都按同一规则更新即可同步。

(b) 比如 $(3,1,1)$ 的初始预测倾向 a。每观察到一次 b，b 的计数就加一，下次 b 的预测概率提高。

(c) 按 **a、b、c、EOS** 划分。首轮 b 的区间为 $[0.45,0.60)$。读到第一个 b 后计数为 $(3,2,1)$，下轮 a、b 的比例分别为 $0.375,0.25$。再取 b，区间为 $[0.50625,0.54375)$。EOS 取最后四分之一，得到 $[0.534375,0.54375)$。可传 **10001001**，其区间 $[137/256,138/256)$ 在其中。

(d) 用 $137/256=0.53515625$ 开始。首轮落入 b，更新到 $(3,2,1)$。第二轮再落入 b，更新为 $(3,3,1)$。第三轮落入固定的 EOS 分支，输出 **bb**。
