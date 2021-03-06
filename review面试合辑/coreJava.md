
# CoreJava 基础面试题

*  int 和 Integer 有什么区别 ？
   > int 是java 基本的数据类型。 
   > Integer 是一个引用对象  Integer 是一个引用对象，提供了对引用对象本身进行
   >操作的方法。  。对象引用实例变量的缺省值为 null，而原 始类型实例变量的缺省值与它们的类型有关。 
   
*  String 和StringBuffer的区别
   > JAVA平台提供了两个类：String和StringBuffer，它们可以储存和操作字符串，即包含多个字符的 字符数据。这个String类提供了数值不可改变的字符串。而这个StringBuffer类提供的字符串进行修改。当你知道字符数据要改变的时候你就可以使用StringBuffer。典型地，你可以使用 StringBuffers来动态构造字符数据。 
   
* 说出ArrayList,Vector, LinkedList的存储性能和特性 
   >ArrayList和Vector都是使用数组方式存储数据，此数组元素数大于实际存储的数据以便增加和插 入元素，它们都允许直接按序号索引元素，但是插入元素要涉及数组元素移动等内存操作，所以 索引数据快而插入数据慢，Vector由于使用了synchronized方法（线程安全），通常性能上较 ArrayList差，而LinkedList使用双向链表实现存储，按序号索引数据需要进行前向或后向遍历， 但是插入数据时只需要记录本项的前后项即可，所以插入速度较快。 
   
* final, finally, finalize的区别。
    <table>
    <tr>
    <td>final</td><td>finally</td><td>finalize</td>
    </tr>
    <tr><td>final 一般作用与修饰变量与方法属性不可变，方法不可覆盖，类不可继承。 </td><td>finally是异常处理语句结构的一部分，表示总是执行</td><td>finalize在垃圾收集器执行的时候会调用被回收对象的此方法，</td></tr>
    </table>
 *  abstract class和interface有什么区别? (面试遇到过)
     <tr><td>声明方法的存在而不去实现它的类被叫做抽象类; 但是 抽象类不能创建实例 不能有 抽象构造函数或抽象静态方法。</td><td></td><td>。接口中的所有方法都是抽象的，没有一个有程序体。，instanceof 运算符可以用来决定某对 象的类是否实现了接口。 接口同样是不能够创建对象的。</td></tr>   
     
 * heap和stack有什么区别。 √
   >栈是一种线形集合，其添加和删除元素的操作应在同一段完成。栈按照后进先出的方式进行处 理。 堆是栈的一个组成元素 
   
 * short s1 = 1; s1 = s1 + 1;有什么错? short s1 = 1; s1 += 1;有什么错?  (基本类型 数据运算后 类型转换问题)
   > s1=s1+1; 当short 类型 与 整形运算后，结果结果类型就变为 int 类型 所以需要强制 类型转换成 short 类型。  s1+= 1; 没错。 _+=_ 运算作用是：两个部分，一是“+”，就是通常所说的直接相加，二是改变结果的类型：将计算结果的类型转换为“+=”符号左边的对象的类型
   
* 、启动一个线程是用run()还是start()? 
    > run() 创建线程    start()启动线程。
* 、接口是否可继承接口? 抽象类是否可实现(implements)接口? 抽象类是否可继承实体类 (concrete class)? 
    > 接口 是可以被接口 继承的。  | 抽象类 可以实现接口的。 |抽象类是否可继承实体类，但前提是实 体类必须有明确的构造函数。 
* 当一个线程进入一个对象的一个synchronized方法后，其它线程是否可进入此对象的其它 方法? 
   >不能(锁住整个对象，以及对象内的方法。)，一个对象的一个synchronized方法只能由一个线程访问。? 无论synchronized关键字加在 方法上还是对象上，它取得的锁都是对象，而不是把一段代码或函数当作锁――而且同步方法很 可能还会被其他线程的对象访问,每个对象只有一个锁（lock）与之相关联.
 * 简述synchronized和java.util.concurrent.locks.Lock的异同 ？ 
   > 主要相同点：Lock能完成synchronized所实现的所有功能 主要不同点：Lock有比synchronized更精确的线程语义和更好的性能。synchronized会自动释放 锁，而 Lock一定要求程序员手工释放，并且必须在finally从句中释放。
 * JAVA语言如何进行异常处理
   > 在java运行程序中，异常分为 两类 一类是 虚拟机 错误。另外是运行异常。我们一般只对 异常进行处理。 处理异常有两种方式。 一种是直接抛出异常。让调用该方法的父方法进行处理。另外一种通过 try ... catch.. 的方式 进行 对异常 进行 铺货，与处理。
 * 什么是java序列化，如何实现java序列化？ 
   > 序列化就是一种用来处理对象流的机制，所谓对象流也就是将对象的内容进行流化。可以对流化 后的对象进行读写操作，也可将流化后的对象传输于网络之间。序列化是为了解决在对对象流进 行读写操作时所引发的问题。 序列化的实现：将需要被序列化的类实现Serializable接口，该接口没有需要实现的方法， implements Serializable只是为了标注该对象是可被序列化的，然后使用一个输出流(如： FileOutputStream)来构造一个ObjectOutputStream(对象流)对象，接着，使用 ObjectOutputStream对象的writeObject(Object obj)方法就可以将参数为obj的对象写出(即保存其 状态)，要恢复的话则用输入流。 
* java 创建对象有几种方式？√
   >  java 共有 5创建对象的方式。 1. 通过关键字 “new ”, 2 通过反射 方法 newInstance()创建 3 通过反射 获取类的构造方法，然后在通过构造方法调用newInstance() 4 clone()方法直接克隆对象。5 通过反序列化        
* Integer f1 = 100;        Integer f2 = 100;        Integer f3 = 150;        Integer f4 = 150;        System.out.println(f1 == f2);　　//true        System.out.println(f3 == f4);　　//false  
  >  将int赋值给Integer时,若int的值在[-128,127]内,则会直接引用Intefer缓存池中的对象;不在,则创建新的Integer对象。
* String、 StringBuffer,StringBuilder 类
  > 当对字符串进行修改的时候，需要使用 StringBuffer 和 StringBuilder 类。StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象。String 是被 final 修饰的，他的长度是不可变的。就算调用 String 的
    concat 方法，那也是把字符串拼接起来并重新创建一个对象，把拼接后的 String 的值赋给新创建的对象
 * 两个相同的对象会有不同的的 hashcode 吗？
  >不能，根据 hash code 的规定，这是不可能的。
  * 有没有可能两个不相等的对象有有相同的 hashcode？
  >有可能，两个不相等的对象可能会有相同的 hashcode 值，这就是为什么在 hashmap 中会有冲突。
 * java 当一个对象被当作参数传递到一个方法后，此方法可改变这个对象的属性，并可返回变化后的结果，那么这里到底是值传递还是引用传递？
 > 是值传递。Java语言的方法调用只支持参数的值传递。当一个对象实例作为一个参数被传递到方法中时，参数的值就是对该对象的引用。对象的属性可以在被调用过程中被改变，但对对象引用的改变是不会影响到调用者的。C++和C#中可以通过传引用或传输出参数来改变传入的参数的值。在C#中可以编写如下所示的代码，但是在Java中却做不到
 * 描述一下JVM加载class文件的原理机制？
 > 类的加载是由类加载器完成的，类加载器包括：根加载器（BootStrap）、扩展加载器（Extension）、系统加载器（System）和用户自定义类加载器（java.lang.ClassLoader的子类）。从Java 2（JDK 1.2）开始，类加载过程采取了父亲委托机制（PDM）。PDM更好的保证了Java平台的安全性，在该机制中，JVM自带的Bootstrap是根加载器，其他的加载器都有且仅有一个父类加载器。类的加载首先请求父类加载器加载，父类加载器无能为力时才由其子类加载器自行加载。
*  为什么要 引用事务机制？
  > 事物的特性 ： 原子性 即要么事物内全部成功，要么失败全部回滚。一致性; 隔离性； 永久性
 
  
 * 在进行数据库编程时，连接池有什么作用？
 >由于创建连接和释放连接都有很大的开销（尤其是数据库服务器不在本地时，每次建立连接都需要进行TCP的三次握手，释放连接需要进行TCP四次握手，造成的开销是不可忽视的），为了提升系统访问数据库的性能，可以事先创建若干连接置于连接池中，需要时直接从连接池获取，使用结束时归还连接池而不必关闭连接，从而避免频繁创建和释放连接所造成的开销，这是典型的用空间换取时间的策略（浪费了空间存储连接，但节省了创建和释放连接的时间）。池化技术在Java开发中是很常见的，在使用线程时创建线程池的道理与此相同。基于Java的开源数据库连接池主要有：C3P0、Proxool、DBCP、BoneCP、Druid等。
 * 字符串 中 “==” 与“equals()”的区别。
 <table>
 <tr><td>==</td><td>equals()</td></tr>
 <tr><td>"==" 主要比较的是 两个字符串的引用地址 是否一致（类似与比较 指针）</td><td>equals()则是比较这两个对象的值 是否相等。</td></tr>
 <tr>tips:  String s1="he";
                    s1=s1+"llo";
                    String s2="hello";
                    System.out.println(s1=="hello");               //false 比较的是地址 引用地址
                    System.out.println(s2=="hello");               //true  字符串常量值                  
  </tr>
 </table>
 
 * 字符串 创建的两种方式
 <table>
 <tr><td>"new" 创建对象</td><td>声明式创建对象 String a="hello";</td></tr>
 <tr><td>"new " 关键字是直接 在Java堆中创建两个对象，这两个对象 引用地址是不相等的  即创建两个对象 他们的引用地址是两个不一样的。</td>
 <td>声明式创建 字符串的对象 是放在 字符串 常量池内的。 即当声明这样的一个字符串后，JVM会在常量池中先查找有有没有一个值为"abcd"的对象,如果有,就会把它赋给当前引用.即原来那个引用和现在这个引用指点向了同一对象,如果没有,则在常量池中新创建一个"abcd",下一次如果有String s1 = "abcd";又会将s1指向"abcd"这个对象,即以这形式声明的字符串,只要值相等,任何多个引用都指向同一对象.</td></tr>
 </table>
  
  * jvm 内存模型
  <table>
  <tr><th>内存模型</th><th>模型说明</th></tr>
  <tr><td>java 堆(Heap)</td><td>java 堆模型是Java虚拟机中最大的一块区域。被线程共享。几乎所有的Java对象都存放在 Java堆中</td></tr>
  <tr><td>方法区(Method Area)</td><td>方法区又称为 永久代 同样被线程共享，该区主要保存 类信息、静态变量、静态常量等 </td></tr>
  <tr><td>程序计数器(Program counter register)</td><td>程序计数器 是用来标识 当前线程执行字节码文件行号指示器 ；多线程情况下，每个线程都具有各自独立的程序计数器，所以该区域是非线程共享的内存区域 </td></tr>
  <tr><td>java栈(java stack)</td><td>java栈 是线程 私有的内存区域； 作用对象是 java 方法。 存储单位是 栈帧。 每个栈帧存放的是对应Java方法所必须的信息。</td></tr>
    <tr><td>本地方法栈(native method stack)</td><td>和Java栈相似 也是线程私有的。不同的是该区域 存放的是Native </td></tr>
  </table>
  *  计算机网络 OSI七层模型
   <table>
   <tr><td>应用层</td><td rowspan="3">应用层是最接近每个具体的应用，主要负责进程之间的交互。应用层交互的数据单元成为 报文。常见协议： HTTP协议、ftp协议  <td></tr>
   <tr><td>表示层</td></tr>
   <tr><td>会话层</td></tr>
   <tr><td>运输层</td><td>提供两个进程间通讯 提供通用的数据传输服务。常见的协议： TCP、UDP协议<td></tr>
   <tr><td>网络层</td><td>网络层使用的是IP协议。分组时也叫IP数据报。 IP 端口 <td></tr>
   <tr><td>数据链路层</td><td>将 网络层封装的数据报 分解成帧。<td></tr>
   <tr><td>物理层</td><td>电缆、光缆 等硬件 <td></tr>
   </table>
  
  <h2>数据库</h2> 
 * 数据库常用索引是什么？
  > 数据库 索引是对表 内 一列或多列 进行 快速查询的数据结构。 常用的索引有 主键索引、唯一索引、复合索引（创建在两个列或者多个列上）索引数据结构一般是 B+ 树、或者是HASH 实现的查询。
  
  * 数据库连接池 是什么意思？
  > 因为 程序每次 获取和关闭 数据库连接 是一个耗时的操作。尤其是当客户端数量增加的时候，会消耗大量的资源，成本是非常高的。数据库 连接池 可以在应用服务器启动的时候建立很多个数据库连接并维护在一个池中。连接请求由池中的连接提供。在连接使用完毕以后，把连接归还到池中，以用于满足将来更多的请求。 
  
  * 解释下驱动(Driver)在JDBC中的角色。
  > JDBC驱动提供了特定厂商对JDBC API接口类的实现，驱动必须要提供java.sql包下面这些类的实现：Connection, Statement, PreparedStatement,CallableStatement, ResultSet和Driver。
 
 
  <h2>框架部分</h2>
  
  * 使用 Spring 框架好处是什么？
  <li> 控制反转: 实现了代码的松散耦合。对象不需要 创建 他们所 依赖的对象。</li>
  <li> 面向切面编程（AOP） : spring 支持 面向切面编程。</li>
  <li> 容器 ：spring 管理应用中对象 的生命周期与配置。</li>
  <li>事务管理：spring 事务传播属性 默认 是 required </li>
  
  * spring 创建对象的三种方式
  > 依据XML 配置文件 、 基于注解的配置(@Autoware) 、基于java的配置（@Configuration）
  