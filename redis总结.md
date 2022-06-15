# redis总结

## redis支持的数据类型
* string
* list
* set
* sorted set
* hash

## redis集群方案
* 主从模式
* 哨兵模式
* 集群模式

## redis过期策略
* 定期删除
* 惰性删除

## redis内存淘汰策略
* no-eviction：当内存不足以容纳新写入数据时，新写入操作会报错
* allkeys-lru：当内存不足以容纳新写入数据时，在键空间中，移除最近最少使用的key（这个是最常用的）
* allkeys-random：当内存不足以容纳新写入数据时，在键空间中，随机移除某个key，这个一般没人用吧
* volatile-lru：当内存不足以容纳新写入数据时，在设置了过期时间的键空间中，移除最近最少使用的key（这个一般不太合适）
* volatile-random：当内存不足以容纳新写入数据时，在设置了过期时间的键空间中，随机移除某个key
* volatile-ttl：当内存不足以容纳新写入数据时，在设置了过期时间的键空间中，有更早过期时间的key优先移除

## redis持久化方式
* aof
* rdb

## redis缓存击穿概念和解决方案
* 概念：缓存的一条热点key瞬间失效，请求到数据库
* 解决方案：使用互斥锁、热点数据永不过期

## redis缓存穿透概念和解决方案
* 概念：key在缓存和数据库都没有，每次请求都会到数据库
* 解决方案：布隆过滤器、缓存不存在的key

## redis缓存雪崩概念和解决方案
* 概念：缓存中大批量不同key数据过期，请求到数据库
* 解决方案：均匀过期、使用互斥锁、缓存永不过期、双层缓存策略(主备缓存切换) 

## redis为什么快
* 纯内存操作
* 单线程
* I/O多路复用
* reactor设计模式
* 多个socket->I/O多路复用程序->文件事件分派器->事件处理器(连接应答处理器、命令请求处理器、命令回复处理器)

## redis常用命令
* ping: 查看redis服务状态
* dbsize: key数量
* select db: 切换redis库
* flushdb: 删除当前库数据
* exit/quit: 退出
* keys *: 显示所有key
* exists: 存在
* expire: 设置过期事件
* type: key的类型
* del: 删除key
* setnx: 设置key
