# spring cloud篇

### 核心组件
* Gateway/Zuul
* Config
* Feign
* Eureka
* Hystrix
* Ribbon

### Ribbon负载均衡策略
* RandomRule随机策略
* RoundRobinRule轮询策略
* RetryRule重试策略
* BestAvailableRule最低并发策略
* AvailableFilteringRule可用过滤策略
* ResponseTimeWeightedRule响应时间加权重策略
* ZoneAvoidanceRule区域权重策略