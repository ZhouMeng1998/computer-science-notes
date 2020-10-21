## Operating Systems: Three Easy Pieces

### Lecture 1

![image-20201021203447111](https://raw.githubusercontent.com/ZhouMeng1998/IMG/image-upload/20201021203448.png)

> virtualization

是操作系统制造出来的一种illusion，让每个process都感觉自己有一个独立的CPU和内存

virtualization要关注efficient和security，virtualization是应该提高效率而不是相反；各个进程之间应该是相互独立的，A进程不能随意获取B进程的数据。

实现的技术有time sharing和space sharing两种

![image-20201021204709730](https://raw.githubusercontent.com/ZhouMeng1998/IMG/image-upload/20201021204710.png)

> process

process有private memory和"address space"，内部有code，heap(堆空间)，stack（栈空间）I/O state和registers

其中**registers**又包含PC（program counter）,SP（stack pointer）,GP（general purpose register）-->想想CSAPP讲寄存器那一节

![image-20201021211749136](https://raw.githubusercontent.com/ZhouMeng1998/IMG/image-upload/20201021211750.png)

> Direct execution

Direct execution是原始的处理机运行方式，程序写在小卡片上，CPU fetch，decode，execute，但是这样会产生很多**问题**。

- 问题1：因为没有操作系统，如果A想要进行restricted系统操作怎么办？
- 问题2：如果想把A程序暂停，运行B程序，怎么办？
- 问题3：如果A处于I/O，CPU idle waiting，该怎么办？

> mode: user mode & kernel mode

kernel mode：OS can do anything

user mode： programs do limited things

正如问题1，如果programs想要进行一些restricted操作（如Disk I/O，修改host文件），那么就得有一个机制，让它能**暂时**获取一些重要的系统权限，即从user mode变为kernel

但这也会存在一个问题，如果这个program是病毒，直接给它这么大的权限（比如直接给它操作系统内核的地址），就可能产生一系列安全问题。

于是便有了trap指令，在讲到trap之前，我们先说一下boot

> boot time

计算机启动的时候，首先是kernel mode，然后大概你进入GUI图形界面的时候，就是user mode了，这也是为什么很多操作都要右键"以管理员身份运行"，因为默认情况下是user mode

> trap

![image-20201021221049398](https://raw.githubusercontent.com/ZhouMeng1998/IMG/image-upload/20201021221050.png)

当某个program想进行system calls时，操作系统为了解决可能的security隐患，**会用trap指令做三件事**

- **让它jump into kernel，but limited location**，也就是说它虽然进入了kernel，但是操作权限还是有限制的
- elevate ”privilege“ from user->kernel
- save register state，这样return的时候program才能回到system call之前的状态

![image-20201021221405237](https://raw.githubusercontent.com/ZhouMeng1998/IMG/image-upload/20201021221406.png)

trap指令是boot time的时候操作系统设置好的，它实际上是汇编代码，告诉hardware"如果你看到XXTrap指令，你就应该怎么做"。

save register也是hardware完成的。

> trap与procedure call

这两者的流程很像，都是执行完一切如初，就好像什么都没发生一样，但trap指令更复杂，涉及system calls

> timer interrupt 

![image-20201021221608399](C:\Users\Philip\AppData\Roaming\Typora\typora-user-images\image-20201021221608399.png)

如问题2，如果我们想暂时挂起某个程序，转而运行另一个程序，这该如何做到？

如上图，存在一个叫timer interrupt的trap指令，到了时间就会挂起程序A，把CPU控制权交给OS，OS这时候又可以do anything

trap与interrupt还是有区别的，interrupt不涉及system call