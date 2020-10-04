* [1 Functions](#1-functions)
  * [1\.1 Environment Diagrams](#11-environment-diagrams)
  * [1\.2 Assignment Statements](#12-assignment-statements)
  * [1\.3 A Complex Example](#13-a-complex-example)
  * [1\.4 Define Functions](#14-define-functions)
  * [1\.5 Calling User\-Defined Functions](#15-calling-user-defined-functions)
  * [1\.6 Local Parameter &amp; Global Parameters](#16-local-parameter--global-parameters)
* [HW\-01](#hw-01)

### 1 Functions

------

#### 1.1 Environment Diagrams

![Environment Diagrams  Environment diagrams visualize the interpreter's process.  Just executed  Import statement  from math import pi  Global frame  tau -  Next to execute  pi  Assignment statement  Name  pi 3.1416  Value  Code (Left):  Statements and expressions  Arrows indicate evaluation order  Frames (right):  Each name is bound to a value  Within a frame, a name cannot be repeated ](https://raw.githubusercontent.com/ZhouMeng1998/IMG/main/typora202010/04/171504-240584.png?token=AL5RCTF7YJFAJYDOSUVS3EC7PGJNO)

左边是statements and expressions，右边是frame（栈帧），每一个name都仅能跟一个value绑定(bound)，name不能重复--->像JAVA常量池的概念

------

#### 1.2 Assignment Statements

![Assignment Statements  la-I  Just executed  2b = 2  3  b,  Next to execute  Execution rule for assignment statements:  Global frame  b  of — from left to right.  I.  2.  Evaluate all expressions to the right  Bind all names to the left of = to the resulting values in the current frame. ](https://raw.githubusercontent.com/ZhouMeng1998/IMG/main/typora202010/04/171509-172968.png?token=AL5RCTFFSLGITT3ATF5XNO27PGJNW)

1. 先计算"="右边的值（即evaluate）
2. 将右值赋给左边

------

#### 1.3 A Complex Example

![Discussion Question 1 Solution  (Demo)  Global  1  2  3  frame  h  max  func max(...)  func min(...)  h — min,  max = g  max  3  max(f(2, g (h (I, 5),  func min(...)  func max(...)  3  ! (2, g(h(l, 5),  3  3))  h(l,  func max(.  5),  5)  5 ](https://raw.githubusercontent.com/ZhouMeng1998/IMG/main/typora202010/04/171512-752454.png?token=AL5RCTDV7Q47H5CL73P5WU27PGJN4)

- 其实是分治，把大问题化成一个一个小问题，最终结果是3
- 也让我想起了邓俊辉数据结构的括号匹配与计算问题
- 同时，每call一个函数，就会创建一个相应的frame--->帮陈杨鑫做的list递归那题

------

#### 1.4 Define Functions

![Defining Functions  Assignment is a simple means of abstraction: binds names to values  Function definition is a more powerful means of abstraction: binds names to expressions  Function signature indicates how many arguments a function takes  >>> def parameters>)  return  <return expression> .  Function body defines the computational process expressed by a function  Execution procedure for def statements:  I.  2.  3.  Create a function with signature parameters>)  Set the body of that function to be everything indented after the first line  Bind  to that function in the current frame ](https://raw.githubusercontent.com/ZhouMeng1998/IMG/main/typora202010/04/171516-541797.png?token=AL5RCTAELZNPN5ZNOKBJHD27PGJOE)

- 创建function，声明(signature)为<name(参数列表)>
- 完善方法体
- 在current frame中把函数名称(比如swap)与函数的代码绑定,calling的时候程序计数器指针会跳到对应的函数位置--->注意不同于C的宏语法，宏只是字符串替换，宏只适用于小且频繁使用的函数，比如height(treeNode->lChild)      

------

#### 1.5 Calling User-Defined Functions

![Calling User-Defined Functions  Procedure for catting/apptying user—defined functions  I.  2.  3.  1  2  3  4  Add a local frame, forming a new environment  Bind the function's formal parameters to its  Execute the body of the function in that new  (version 1):  arguments in that frame  from operator import mul  def square(x):  return mul(x, x)  square(-2)  environment  Global frame  mul  square  Original name of  function called  Local frame  Formal parameter  bound to argument  square  x  {Return  value  -2  4  Built—in function  •func mul(...)  -Äfunc  User-defined  function  Return value  (not a binding!) ](https://raw.githubusercontent.com/ZhouMeng1998/IMG/main/typora202010/04/171528-985188.png?token=AL5RCTAWYVHVT3NOJVHLJ3K7PGJO6)

- Function  signature(即函数声明)很重要，它告诉编译器该创建一个什么样的local frame，比如参数列表只有一个x(叫formal parameter)，那么栈帧中就只会放一个x（传进去后叫local parameter）
- -2作为值传递给formal  parameter x赋值

![1  4  from operator import  def square(x):  return  square(-2)  mul  rames  Global frame  square  Objects  func mul(..  func square(x)  bind "square" to the function  "func square(x)"  First < Back  e that has just executed  Xt line to execute  Step 5 of 5  Forward >  Last  square  x  Return  value  -2  4 ](https://raw.githubusercontent.com/ZhouMeng1998/IMG/main/typora202010/04/171533-629367.png?token=AL5RCTGS5HBQCREN74X3JHS7PGJPG)

------

####  1.6 Local Parameter & Global Parameters

![Looking Up Names In Environments  Every expression is evaluated in the context of an environment.  So far, the current environment is either:  The global frame alone, or  A local frame, followed by the global frame.  Most important two things I'LL say al Z day:  An environment is a sequence of frames.  A name evaluates to the value bound to that name in the earliest  frame of the current environment in which that name is found.  to look up some name in the body of the square function:  E.g.,  Look for that name in the local frame.  If not found, look for it in the global frame.  (Built—in names like "max" are in the global frame too,  but we don't draw them in environment diagrams.) ](https://raw.githubusercontent.com/ZhouMeng1998/IMG/main/typora202010/04/171537-250687.png?token=AL5RCTDHBZGYBHOE2Q5TXJ27PGJPO)

前面讲到,任意一个时刻,一个变量都只能bound to one value,就好比函数中x只能对应于一个y.在操作一个变量的时候,会首先从current      environment（earliest frame）中去找,比如你现在就是进入了一个函数中,现在是local frame,那么就是从local frame找

```C
i = 0;

j = 1;

Fun(int i){

   i = 2;

   print(%d, i);----->输出的是2而不是1，因为首先从local frame去找

   print(%d, j);----->local frame没有，就去找global frame，结果找到是2

}
```

再看一个例子，看右边global frame里也有一个square，只不过那个square是函数名，而你需要的局部变量square则是一个整数，正因为"local frame优先"的原则，这里square顺利被赋值为-2，而不是那个函数square

![2  First  from operator import  def square(square):  return mul (square  square(-2)  mul  square)  Global frame  mul  Ysquare  func mul(..  •func square(square)  local framefft%  < Back  step 4 of 5  square  square  -2  Forward >  Last ](https://raw.githubusercontent.com/ZhouMeng1998/IMG/main/typora202010/04/171544-153995.png?token=AL5RCTEW2UOYBMFVOASPJJS7PGJP4)

------

### HW-01

看最后一行return f(a, b)，f肯定是一个函数，而如果你写f = sub(a, b)，sub(a, b)是一个函数调用，返回的是一个int数值，也就是把一个int赋给了f，然后你再return f(a, b)肯定报错

![from operator import add, sub  def a_plus_abs—b(a, b):  """Return a+abs(b) ,  5  a_p1us_abs_b(2,  5  but without calling abs.  3)  -3)  >>> # a check that you didn't change the return statement!  import inspect, re  ' , inspect.  C' return f(a, b) 'l  Sü7sub(a, b)  if b <  f  sub  else :  f add  f(a, b)  return ](https://raw.githubusercontent.com/ZhouMeng1998/IMG/main/typora202010/04/171547-815716.png?token=AL5RCTEDXVAVOJ2P74CGZL27PGJQA)