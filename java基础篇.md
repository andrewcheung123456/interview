# java基础篇

### JDK、JRE、JVM的区别
* JDK是java开发工具包，JDK包括JRE，类库，java工具
* JRE是java运行环境，JRE包括JVM，类库
* JVM是java虚拟机，java虚拟机在执行字节码

### java语言的特点
* 面向对象性
* 健壮性
* 跨平台性

### java的三大特性
* 封装
* 继承
* 多态

### 多态存在的条件
* 继承
* 重写
* 父类引用指向子类对象

### java中的关键字
* 定义数据类型：class interface enum byte short int long float double char boolean void
* 定义流程控制：if else switch case default while do for break continue return
* 定义访问权限：private protected public
* 定义修饰符：abstract final static synchronized
* 定义类之间的相关关系：extends implements
* 定义建立实例及引用实例，判断实例的关键字：new this super instanceof
* 异常处理的关键字：try catch finally throw throws
* 用于包的关键字：package import
* 其他修饰符关键字：native strictfp transient volatile assert

### final、finally和finalize区别
* final用来修饰类、方法、常量，修饰的类、方法、常量不可变
* finally用于try-catch,最终执行的代码，finally在return之前执行
* finalize回收垃圾方法，显示调用System的gc()方法时，垃圾回收器调用finalize()

### static关键词
* 修饰在变量上是静态变量
* 修饰在方法上是静态方法
* 修饰在代码块上是静态代码块

### java的8种基本类型
* byte,8位=1字节
* short,16位=2字节
* int,32位=4字节
* long,64位=8字节
* float,32位=4字节
* double,64位=8字节
* char,16位=2字节
* boolean,8位=1字节

### 对象的引用
* 强引用对象哪怕JVM内存溢出都不会被JVM回收
* 软引用对象会在内存不足时被回收
* 弱引用对象会在JVM垃圾回收时回收
* 虚引用不会决定对象的生命周期，如果一个对象仅持有虚引用，那么它就和没有任何引用一样，在任何时候都会被垃圾回收器回收

### new对象的过程
* 类的加载
* 类的初始化

### 类加载过程
* 加载
* 验证
* 准备
* 解析
* 初始化
* 使用
* 卸载

### 类的初始化
* 在堆区分配内存空间
* 实例变量赋默认值
* 设置对象头
* 实例初始化

### 实例初始化顺序
* 父类静态变量
* 父类静态代码块
* 子类静态变量
* 子类静态代码块
* 父类非静态变量
* 父类类非静态代码块
* 父类构造函数
* 子类非静态变量
* 子类非静态代码块
* 子类构造函数

### String、StringBuilder、StringBuffer区别
* String是不可变字符串，StringBuilder、StringBuffer是可变字符串
* 运行速度StringBuilder>StringBuffer>String
* StringBuilder非线程安全，StringBuffer线程安全

### String s = new String("xyz");创建了几个String Object
* 2个、常量池中有一个字符串对象，new的时候，在堆内存中创建了一个字符串对象

### Collection包括那些
* List
* Set

### List包括哪些
* ArrayList
* LinkedList
* Vector
* Stack

### Set包括哪些
* HashSet
* LinkedHashSet
* TreeSet

### Map包括哪些
* HashTable
* HashMap
* TreeMap
* Properties
* LinkedHashMap

### 注解
* @Retention定义在哪一级别可用，在源代码、class类文件或者运行时
* @Documented生成文档信息的时候保留注解
* @Target用于描述注解的使用范围
* @Repeatable表示注解可以重复使用

### HashMap为什么是线程不安全的
* 在JDK1.7中，当并发执行扩容操作时会造成环形链和数据丢失的问题
* 在JDK1.8中，在并发执行put操作时会发生数据覆盖的问题

### HashMap的put过程
* 判断数组table是否为空，若为空，进行初始化；不为空，利用hash方法计算key的HashCode，通过（n-1）&hashCode计算应当存放在数组中的下标index。
* 查看数组table[index]是否存在数据，若没有数据，构造一个Node<K,V>节点，存放在table[index]中；若存在数据，则发生哈希冲突，继续判断key是否相等
* 若key相等，用新的value替换原来的数据，若不相等，判断当前节点是否是TreeNode<k,v>树型节点
* 若是树型节点，创造树型节点插入红黑树中；若不是树型节点，创造普通的Node<K,V>加入链表尾部；
* 链表的长度大于阈值8并且数组长度大于64，则链表转红黑树，若不满足，进行数组扩容
* 插入完成后。判断当前节点是否大于实际存储空间大小，如果大于了，就要调用resize（）方法进行扩容，按数组原长度进行一倍扩容，如：原来数组长度为32，扩容后为64

### HashMap的get过程
