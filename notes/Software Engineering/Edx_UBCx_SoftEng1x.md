## 1 Introduction

### 1.1 Programming language introduction

interpreted language与complied language区别是：

前者interpret一行，运行一行，后者先由complier（如JVM）编译，再翻译成机器码。

- JAVA和JavaScript都属于complied language，所以m1()函数即便定义在main函数的后面也不影响执行，而interpreted language就不行。
- JAVA也可以被认为是interpreted language，因为.java文件经JVM编译后生成的字节码文件无法执行，要再次进行解释才能变成机器指令。
- JAVA现在引入了JIT(Just-In-Time)Compilation技术，可以把运行频率高的字节码直接译成机器指令，从这个角度来说JAVA是"半编译型"语言

**本门课用到的TypeScript是JavaScript的超集，后者是static，而它是static+dynamic**。

static:

```typescript
var a : number;
a = 100;
a = false;//报错
```

dynamic:

```typescript
var a : any;
a = 100;
a = false;//通过
```

**补充阅读**：语言的类型：https://www.zhihu.com/question/19918532/answer/58538334

弱类型：

```js
> "1"+2
'12'
```

强类型：

```python
>>> "1"+2
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: cannot concatenate 'str' and 'int' objects
```

动态(dynamic)类型：

```python
>>> a = 1
>>> type(a)
<type 'int'>
>>> a = "s"
>>> type(a)
<type 'str'>
```

静态(static)类型：

```haskell
Prelude> let a = "123" :: Int

<interactive>:2:9:
    Couldn't match expected type `Int' with actual type `[Char]'
    In the expression: "123" :: Int
    In an equation for `a': a = "123" :: Int
```

### 1.2 Introduction to Concurrency and Asynchronous Development: Part 1

**Concurrency**: concurrency会大大提高performance，但是也会带来security方面的问题，因为各种processes，threads都可能在操作同一块内存区域，这就可能导致OS里提到的dead lock等问题。

typescript没有concurrency，那是java里的概念

**Async**: async lib has steep learning curve(see the frustration level as the yellow line shown in the following graph). Once you get used to async style, your productivity will increase dramatically.

![1601710310666](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/153155-561364.png)

**Single Threaded, Non-Blocking, Asynchronous **: blocking是在single thread程序中应该竭力避免发生的问题，当某一处发生了blocking，如果没有asynchronous mechanism来处理，就会导致无意义的等待(sitting idle)，等one statement的时间是可以执行thousands of other statements的。

typescript和JavaScript虽然都是single threaded，但是它们可以**`offload`** blocking，把阻塞的地方隔离到另外一个platform运行，这个机制就是asynchronous。

### 1.3 Introduction to Concurrency and Asynchronous Development: Part 2

**callbacks(回调函数)**: callback function是被作为参数传递给另一个函数的函数，这属于**`函数式编程`**。比如函数setTimeOut(onDone, delay)，其中onDone函数作为参数传递到setTimeOut中，它就是callback：

```typescript
setTimeOut(display, 1000); //等待1000ms后，执行display函数
function display(){
	console.log('Hello World!')；   
}
```

上面的这个setTimeOut函数，编译器发现它的参数列表有函数display(callback)，它知道需要用asynchronous机制来处理。

**asynchronous原理**:

1. typescript普通函数是放在call stack中执行的，而callback则是放在Web APIs这个platform中执行(即1.2讲到的offload与隔离)
2. 1s等待结束后便开始执行display函数，执行后的结果放到callback queue中
3. 由于此时call stack为空(其他函数已经执行完毕), event loop会把callback queue中display的执行结果放到call stack中，程序结束

![1601712356285](https://raw.githubusercontent.com/ZhouMeng1998/computer-science-notes/main/IMG/202010/03/160556-510867.png)

