# java并发篇

### 线程池的创建方式
* 通过ThreadPoolExecutor方式
* 通过Executors方式

### ThreadPoolExecutor参数说明
* corePoolSize核心线程数
* maxPoolSize最大线程数
* keepAliveTime线程空闲时间
* timeUnit线程空闲时间单位
* threadFactory线程工厂用来创建线程
* workQueue阻塞队列
* rejectedExecutionHandler任务拒绝处理器

### ThreadPoolExecutor队列策略
* 直接队列SynchronousQueue
* 有界队列ArrayBlockingQueue
* 无界队列LinkedBlockingQueue
* 优先级的队列PriorityBlockingQueue
* 延时队列DelayQueue

### ThreadPoolExecutor拒绝策略
* AbortPolicy直接抛出异常
* CallerRunsPolicy由调用者处理该任务
* DiscardPolicy直接丢弃任务
* DiscardOldestPolicy丢弃最早的任务，再尝试提交任务，失败重试

### Executors方式创建线程池有哪些
* newCachedThreadPool可缓存线程池
* newFixedThreadPool固定大小线程池
* newScheduledThreadPool定时线程池
* newSingleThreadExecutor单线程线程池
* newSingleThreadScheduledExecutor单线程定时线程池
* newWorkStealingPool抢占式线程池

### 线程池工作原理(任务提交过程)
* 如果正在运行的线程数小于核心线程数，创建核心线程去执行任务
* 如果正在运行的线程数大于核心线程数，任务就放入阻塞队列
* 如果阻塞队列已满且小于最大线程数，创建非核心线程去执行
* 如果阻塞队列已满且大于等于最大线程数，执行拒绝策略

### 线程池状态
* RUNNING线程池初始化状态，可以添加执行任务
* SHUTDOWN线程池处于待关闭状态，不接收新任务处理已接收任务
* STOP线程池立即关闭，放弃缓存队列的任务并且终止正在处理的任务
* TIDYING线程池处理整理状态，SHUTDOWN->TIDYING，STOP->TIDYING
* TERMINATED线程终止状态

### synchronized实现同步
* 对于普通同步方法，锁是当前实例对象，基于ACC_SYNCHRONIZED实现，本质还是monitor监视器同步
* 对于静态同步方法，锁是当前类的class对象，基于ACC_SYNCHRONIZED实现，本质还是monitor监视器同步
* 对于同步方法块，锁是synchronized括号里配置的对象，基于monitorenter和monitorexit实现

### synchronized锁状态升级过程
* 无锁状态
* 偏向锁状态，一个线程竞争
* 轻量级锁状态，两个线程竞争
* 重量级锁状态，自旋超过一定的次数，或者一个线程在持有锁，一个在自旋，又有第三个来访时

### 对象包含哪些
* 对象头
* 实例数据
* 对齐填充

### 对象头包含哪些
* MarkWord，存储对象的hashCode、GC分代年龄、锁状态标志、线程持有的锁、偏向线程ID等
* Klass Pointer，类型指针指向对象的元数据
* Array Length，数组长度(如果是数组)

### 线程的5种状态
* New新建状态
* Runnable就绪状态
* Running运行状态
* Blocked阻塞状态
* Dead死亡状态

### synchronized的对象锁的指针指向monitor对象的起始地址，monitor是由ObjectMonitor实现，ObjectMonitor包含哪些变量
* _count = 0; 记录数
* _recursions = 0; 锁的重入次数
* _owner = NULL; 指向持有ObjectMonitor对象的线程
* _WaitSet = NULL; 调用wait后，线程会被加入到_WaitSet
* _EntryList = NULL ; 等待获取锁的线程，会被加入到该列表

### JMM模型
* 线程
* 工作内存
* 主内存

### JMM并发相关的三个特性
* 原子性
* 可见性
* 有序性

### 缓存一致性解决方案
* 总线加lock锁
* 缓存一致性协议

### 缓存一致性协议
多个cpu从主内存读取同一个数据到各自的高速缓存中，其中当某个cpu修改了缓存里的数据，该数据马上同步回主内存，其他cpu通过总线嗅探机制，可以感知到数据的变化从而将自己缓存的数据失效。

### volatile的特性
* 可见性
* 不保证原子性
* 禁止指令重排序

### happen-before原则
* 单线程happen-before原则：在同一个线程中，书写在前面的操作happen-before后面的操作。
* 锁的happen-before原则：同一个锁的unlock操作happen-before此锁的lock操作。
* volatile的happen-before原则： 对一个volatile变量的写操作happen-before对此变量的任意操作。
* happen-before的传递性原则： 如果A操作 happen-before B操作，B操作happen-before C操作，那么A操作happen-before C操作。
* 线程启动的happen-before原则：同一个线程的start方法happen-before此线程的其它方法。
* 线程中断的happen-before原则：对线程interrupt方法的调用happen-before被中断线程的检测到中断发送的代码。
* 线程终结的happen-before原则：线程中的所有操作都happen-before线程的终止检测。
* 对象创建的happen-before原则：一个对象的初始化完成先于他的finalize方法调用。

