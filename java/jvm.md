# jvm Java虚拟机 

## jvm 分为几部分
  > JVM 主要包含两个子系统和两个组件，两个子系统为 class loader （类装载）、execution engion (执行引擎)；两个组件为： runtime data area）（ 运行中数据区 ） ，native interface (本地接口)
- Class Loader(类装载) 根据给定的全限定类名（如 java.lang.Object）来装载class 文件到Runtime data area 中的method area(方法区).
- Execution engion (执行引擎) 执行 classes 中的指令
- Native Interface (本地接口) 与native libraries 交互，是其他编程语言交互的接口。
- Runtime data area (运行时数据区域) 这就是我们常说的JVM内存。

<img style="width:600px;" src='https://img-blog.csdnimg.cn/20200103213149526.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly90aGlua3dvbi5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70'>


# jvm 作用
> 首先通过编译器把java代码转换成字节码，类加载器（class loader） 再把字节码加载到内存中，将其放在运行中数据区（runtime data area）的方法区内，而字节码文件只是JVm的一套指令集 
> 规范，并不能直接交给底层操作系统去执行，因此需要特定的命令解析引擎（execution engion），将字节码翻译成底层系统指令，再交由CPU执行，而这个过程中需要调用其他语言
> 的本地库接口（native interface） 来实现整个程序的功能。

# java程序运行机制步骤
- 首先利用IDE集成开发工具编写java源代码，源代码文件后缀为：.java;
- 在利用编译器（javac命令）将源代码编译成字节码，字节码文件后缀名为.class;
- 运行字节码的工作是由解释器（java命令）完成的。

<img src='https://img-blog.csdnimg.cn/2020031416414486.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoaW5rV29u,size_16,color_FFFFFF,t_70'>

- 类的加载指的是将类的.class 文件中的二进制数据读入到内存中，将其放在运行时数据区的方法区内，然后在堆区创建一个java.lang.Class对象，用来封装类在方法区内的数据结构。

# 说一下jvm 运行时数据区
> java 虚拟机在执行Java程序过程中会把它所管理的内存区域划分为若干个不同的数据区域。这些区域都有各自的用途，以及创建销毁的时间，有些区域随着虚拟机进程的启动而存在，有些区域则是依赖线程的启动
> 和结束而建立和销毁，Java虚拟机锁管理的内存被划分为如下几个区域：

<img style='width:600px;' src='https://img-blog.csdnimg.cn/20200103213220764.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly90aGlua3dvbi5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70' />

- 程序计数器（program counter register）:当前线程所执行的字节码的行号指示器，字节码解析器的工作是通过改变这个计数器的值，来选取下一条需要执行的字节码指令，分支、循环、跳转、异常处理、线程恢复等基础功能，都需要依赖这个计数器来完成
- java虚拟机栈 （Java virtual machine stacks）：用于存储局部变量表、操作数栈、动态链接、方法出口等信息；
- 本地方法栈（native method stack ）：与虚拟机栈的作用是一样的，只不过虚拟机栈是服务 Java 方法的，而本地方法栈是为虚拟机调用 Native 方法服务的；
- Java 堆 （Java heap）：Java 虚拟机中内存最大的一块，是被所有线程共享的，几乎所有的对象实例都在这里分配内存；
- 方法区（method area）：用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译后的代码等数据。
# 说一下栈堆的区别？

- 物理地址
    > 堆的物理地址分配对对象是不连续的。因此性能慢些。在GC的时候也要考虑到不连续的分配，所以有各种算法。比如，标记-消除，复制，标记-压缩，分代（即新生代使用复制算法，老年代使用标记——压缩）
    > 栈使用的是数据结构中的栈，先进后出的原则，物理地址分配是连续的。所以性能快。
- 内存分别
    > 堆因为是不连续的，所以分配的内存是在运行期确认的，因此大小不固定。一般堆大小远远大于栈。
    > 栈是连续的，所以分配的内存大小要在编译期就确认，大小是固定的。
- 存放内容
    > 堆存放的是对象的实例和数组。因此该区更关注的是数据的存储
    > 栈存放：局部变量，操作数栈，返回结果。该区更关注的是程序方法的执行。
- ps
    > 静态变量放在方法区 </br>
    > 静态的对象还是放在堆。    
- 程序的可见度：
    > 堆对于整个应用程序都是共享、可见的。</BR>
    > 栈只对于线程是可见的。所以也是线程私有。他的生命周期和线程相同。     