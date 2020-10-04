[TOC]

# 1. Boolean Functions and Gate Logic

#### 1.2 Boolean Functions Synthesis

##### 1.2.1 Truth Table to Boolean Expression

<img src="https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/image-20201003094317907.png" alt="image-20201003094317907" style="zoom:200%;" />

- 只看f=1的行，即1，3，5行
- 每一行我们都用NOT和AND来表示一个式子，如第二行NOT(X) AND Y AND NOT(Z)
- 然后OR

![计算机生成了可选文字: TruthTabletoBooleanExpression (NOT(x)ANDNOT(y)ANDNOT(z)) (NOT(x)ANDYANDN0T(z)) （×ANDN0T(y)ANDNOT(z)) OR OR (NOT(x)ANDNOT(z))OR(xANDNOT(y)ANDNOT(z)) (NOT(x)ANDNOT(z))OR(NOT(Y)ANDNOT(z)) NOT(z)AND(NOT(x)ORNOT(y))](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/141901-795663.png)

把这个式子不断化简，就得到NOT(Z) AND ((NOT(X)) OR NOT(y))

##### 1.2.2 AND, NOT

用NOT和AND就可以表示所有的Boolean function，因为OR是可以被NOT和AND表示的

##### 1.2.3 NAND

再进一步，用NAND可以表示所有的逻辑电路



![1601702798851](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/132640-519150.png)

用NAND表示NOT和AND

![1601703435323](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/04/110937-705223.png)

**习题：**

哪一个对应于NAND(x,x)？真值表如下所示

![1601703156358](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/133237-517953.png)

![1601703278135](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/133438-714350.png)

**答案：D，用公式，(X NAND Y) = NOT(X AND Y)，就是D**

#### 1.3 Logic Gates

NAND, NOR, NOT, AND

![1601774711626](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/04/092515-146404.png)

![1601774946609](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/04/092907-451339.png)

从circuit到logic gates，lecture有个习题问*右图a，b，c的order影响最终输出吗？*,我当时用交换律得出结论不影响。**其实左图更直观，the order of these gates doesn't matter in terms of the output.**

![1601775405273](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/04/093646-181317.png)

这是一门CS课程，不是EE课程，所以我们**不关注implementation of hardwares，只关注interface**

#### 1.4 Hardware Description Language

下图描述的就是HDL语言，PARTS里面是implementation

![1601776677301](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/04/095758-60575.png)

注意，类似a=a，out=out这类代码很常见

习题1：如何用HDL表示下图红色的部分？

![1601776530414](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/04/095531-270538.png)

答案：OR (a = aAndNotb, b = notaAndb, out=out)

#### 1.5 Hardware Simulation

步骤：先用HDL来设计电路，然后放到hardware simulator中，将之模拟hardware，然后用test script(测试文件)去测试hardware的设计是否符合我们的要求(compare file)，看output是否和desired output match。

硬件开发流程：

- 首先是system architects设计好chip API，test script，compare file
- 然后developer去按设计造硬件。
- architect与developer就像设计院与施工方的关系

#### 1.6 Multi-Bit Buses

从chips到buses：加法器(Add16)这类稍微复杂的逻辑器件可以被看做是一个整体(entity)，这个entity又可以被用来设计其他更复杂的逻辑器件(如Add3Way16)。

这就是进一步抽象，我们无需过度关注AND,OR,NAND,NOT，而是改用multi-bit buses来设计hardware。

![1601779093512](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/04/103817-892120.png)

习题2：

*This is the interface declaration for an example chip named Example16, which we haven't discussed before:*

*IN c, Bus1[16], Bus2[16];*

*OUT out, out2[16];*

*Which of these lines are valid in HDL, when implementing the Example16 chip?*

- [ ] A: Add16(a=Bus1[0..15], b=Bus2[0..15], out=out2[0..14]);
- [ ] B: Add16(a=Bus1[0..15], b=Bus2[0..15], out[0..14]=out2[0..14]);
- [ ] C: Add16(a=true, b=false, out=out2);
- [ ] D: Add16(a=c, b=Bus2[0..15], out=out2);
- [ ] E: And(a=c, b=Bus2[7], out=out);



答案：B C E

- A: Add16需要的in是两个16 bits，out也是16bits，如果你让out=out2[0...14]，out就只有15bits，这就不符合Add16的输出规则
- B: out[0..14]=out2[0..14] means that we're discarding the most significant bit of Add16's out, and using the rest to connect to the 15 least significant bits of Example16's out2.
- C: As was mentioned previously in the lecture, true and false can represent a bus with constant signal of arbitrary width. a = true = 111111111111111; b= false = 000000000000000
- D: 'c' is a single bit, while Add16 expects a 16-bit bus as 'a'. 看到IN c就应该知道这是single bit，因为没指明长度
- E: This works, because And expects single bits as input 'a' and 'b'.

