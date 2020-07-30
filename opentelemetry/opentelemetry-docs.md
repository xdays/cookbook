# 基本概念

1. trace包含一个或者多个span，space表示在一次请求中，各个服务所做的任务
2. 每个请求都会有个trace id来标识，一次trace的每个span也有一个唯一标识

# Span的生命周期

1. 服务收到请求，如果存在，就从请求中提取 `span context` 
2. 一个新的span作为提取到的span的子span会被创建，如果没有提取到的话，一个root span会被创建
3. 服务处理请求，额外的属性或者事件会被添加到span中，以帮助用户理解当前请求的上下文，比如服务器主机名或者客户标识符之类的
4. 一些新的子span可能会被创建，来表示当前服务的子模块所完成的任务
5. 当服务向另一个服务发起调用时，当前的span会被序列化，然后发给另一个服务，使用的方法就是把span的上下文封装到请求header里
6. 当服务的任务完成时，span的状态会被更新，span被标记为完成

# Metrics定义

有三种类型的Metrics

1. counter
2. measure
3. observer

一些Metrics的应用场景

1. CPU使用率
2. 内存使用率
3. 当前活动连接数

# 使用OpenTelemetry

1. 导入OpenTelemetry的API和SDK
2. 配置OpenTelemetry API
3. 配置OpenTelemetry SDK
4. 创建Telemetry数据，trace或者metrics
5. 导出数据，直接导出或者用Collector，所有SDK都支持OTLP协议