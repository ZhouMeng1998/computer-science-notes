# Parallel Programming in Java

### Week1 - task parallelism

#### 1.1 - task creation and termination

![计算机生成了可选文字: ，0\乙0F CDRE 6VMQz D卩 B在 SC 从F《一'](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/200331-184010.png)

JAVA通过ASYNC与FINISH这两个信号来确定并行代码的范围(起止)与结束。

比如左边求一个数组的sum，并行编程是把左边和右边单独计算计算（divide-and-conquer），然后合并;左右分别计算的过程即并行，用ASYNC信号量进行协调，结束并行则是靠FINISH信号量。 

比如右边S2,S3,S4三行代码是**并行（非并发**），下面的第五行则要等它们三个都执行完毕再执行。

这样一来，S2,S3,S4就可以用到多个processor(core)同时运行

![计算机生成了可选文字: 1-finish{ asyncSl;// 2 3 5 asynchronouslycomputesum酐thelowerhalfofthearray computesumoftheupper、halfofthearrayinparallelwithSl S2； S3;//combinethet到0partiaISumsafter、bothSIandS2havefinished](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/200342-117414.png)

#### 1.2 - Tasks in Java's Fork/Join Framework

[summary](https://www.coursera.org/learn/parallel-programming-in-java/supplement/wlDUr/1-2-lecture-summary)

![ト  れ ( 0 戸 ・ フ 今 一 - 2 、 の ・ 7  を を = 鈊 し 3 っ  化 ()H く フ 引 1  ( ) 2 印 0 つ  QC フ  ア 9 盟 フ ・ 7 フ ら u  ( W09  气 い 01  い つ ](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/200334-393410.png)

仔细看，这是一个归并算法的伪代码

![FORK 今 ](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/200329-132830.png)

用了fork，join就是并发(concurrent)了

#### 1.3 computation graphs

![( 第 巳 ( 0 町 ](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/200327-460574.png)

让我想到了git里的fork和关键路径问题(陈越数据结构)

 三个重要概念:

- Work:1 + 10 + 1 +      10 = 22 即计算总量（或运行总时长）
- **Span(critical path length, CPL)**:所有并行计算的fork中，the longest path，图中s1->s2->s4是12，s1->s3->s4也是12，所以span就是12
- Ideal parallelism(并行数) = work   / span，最理想状态是work / span就是并行数，这里是22/12≈2，所以并非理想情况

#### 1.4 Multiprocessor Scheduling, Parallel Speedup

![1601729573035](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/205253-298173.png)

不同的**scheduling**(进程调度)带来的性能提升是不一样的。观察左边两张表，如果P0做S1-S2-S3-S6-S7, P1做S4,S5，P1不干活叫做**idle**(空闲)，总时间就是P0的时间，即T = 1+1+1+10+1= 14s

而下面一种情况P0是S1-S6-S7，T = 1+10+1 = 12s

明显第二种scheduling更高效。

三种情形:

1. 只有一个processor，T1 = work = 16
2. 无限processor，T∞ = span = 12，span为critical path length
3. P个processor，T∞ ≤ Tp ≤ T1

**Speedup(P) (性能优化指标) = T1 / Tp <= work / span = ideal parallelism**

#### 1.5 Amdahl's Law

*`Lecture Summary`: In this lecture, we studied a simple observation made by `Gene Amdahl` in 1967: if q ≤ 1 is the fraction of WORK in a parallel program that must be executed sequentially, then the best speedup that can be obtained for that program for any number of processors, P , is Speedup(P) ≤ 1/q.*

*This observation follows directly from a lower bound on parallel execution time that you are familiar with, namely TPP ≥ SPAN(G). If fraction q of WORK(G) is sequential, it must be the case that SPAN(G) ≥ q × WORK(G). Therefore, Speedup(P) = T11/TPP must be ≤ WORK(G)**/(q × WORK(G)) = 1/q since T11 = WORK(G) for greedy schedulers.*

*Amdahl’s Law reminds us to watch out for sequential bottlenecks both when designing parallel algorithms and when implementing programs on real machines. As an example, if q = 10%, then Amdahl's Law reminds us that the best possible speedup must be ≤ 10 (which equals 1/q ), regardless of the number of processors available.*

**Optional Reading:** Wikipedia article on [Amdahl’s law](https://en.wikipedia.org/wiki/Amdahl%27s_law#Speedup_in_a_serial_program).

设q为你程序中不得不顺序执行(execute sequentially)statements的比例，即**不能并发只能并行statements的数量**。Amdahl's law是说给定q，Speedup(p) <= 1 / q。这好理解，假设你程序中所有statements must be executed sequentially，那么1个processor与infinite processors是没区别的；而假设你所有statements can be executed concurrently，那么processor越多，速度越快。

详细推论请看上面的第二段文字。

**总之，Speedup(p)与q成反比，程序中顺序执行的statements越多，并发优化的余地就小，反之可并行的statements越多，并发优化就越明显。我们设计程序的时候，应尽量减少sequential execution的余地**

#### 1.6 Demonstration

async/finish

![1601731752413](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/212913-388107.png)

fork/join

![](https://raw.githubusercontent.com/ZhouMeng1998/IMG/main/typora202010/04/155138-906645.jpeg?token=AL5RCTDKIRCM7IRHK2G2FPC7PF7UQ)

注意sequential_threshold，如果数据比较少，用fork/join进行并发反而比sequential execution(即hi - lo < sequential_threshold的情形)要慢，这是因为else分支中递归的入栈出栈操作消耗时间，所以sequential_threshold尽量大一点，比如1000.



