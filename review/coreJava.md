
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
   
     