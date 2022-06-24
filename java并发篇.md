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