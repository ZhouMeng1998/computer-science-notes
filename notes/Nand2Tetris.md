# 1. Boolean Functions and Gate Logic

#### 1.1 Boolean Logic

#### 1.2 Boolean Functions Synthesis

##### 1.2.1 Truth Table to Boolean Expression

<img src="https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/image-20201003094317907.png" alt="image-20201003094317907" style="zoom:200%;" />

- 只看f=1的行，即1，3，5行
- 每一行我们都用NOT和AND来表示一个式子，如第二行NOT(X) AND Y AND NOT(Z)
- 然后OR

![计算机生成了可选文字: TruthTabletoBooleanExpression (NOT(x)ANDNOT(y)ANDNOT(z)) (NOT(x)ANDYANDN0T(z)) （×ANDN0T(y)ANDNOT(z)) OR OR (NOT(x)ANDNOT(z))OR(xANDNOT(y)ANDNOT(z)) (NOT(x)ANDNOT(z))OR(NOT(Y)ANDNOT(z)) NOT(z)AND(NOT(x)ORNOT(y))](C:\Users\Philip\Desktop\Courses\笔记\cs-notes\computer-science-notes\IMG\clip_image001.png)

把这个式子不断化简，就得到NOT(Z) AND ((NOT(X)) OR NOT(y))

##### 1.2.2 AND, NOT

用NOT和AND就可以表示所有的Boolean function，因为OR是可以被NOT和AND表示的

##### 1.2.3 NAND

再进一步，用NAND可以表示所有的逻辑电路



![1601702798851](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/132640-519150.png)

用NAND表示NOT和AND

![1601703435323](C:\Users\Philip\AppData\Roaming\Typora\typora-user-images\1601703435323.png)

**习题：**

哪一个对应于NAND(x,x)？真值表如下所示

![1601703156358](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/133237-517953.png)

![1601703278135](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/133438-714350.png)

**答案：D，用公式，(X NAND Y) = NOT(X AND Y)，就是D**

#### 1.3 Logic Gates

