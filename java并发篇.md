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
* 轻量级锁状态，多个线程竞争
* 重量级锁状态，多个线程当自旋超过一定的次数，或者部分线程在持有锁，另一部分线程在自旋，又有其他线程来获取锁

### 对象包含哪些
* 对象头
* 实例数据
* 对齐填充

### 对象头包含哪些
* MarkWord，存储对象的hashCode、GC分代年龄、锁状态标志、线程持有的锁、偏向线程ID等
* Class Metadata Address，类型指针指向对象的元数据
* Array Length，数组长度(如果是数组)

### 