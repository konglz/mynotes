
## 1. RPC概述

### 1.1 RPC结构图

![RPC结构图](%E6%8E%A5%E5%8F%A3%E5%AE%9A%E4%B9%89%E8%AF%AD%E8%A8%80.jpg)

### 1.2. RPC的要素

* 接口层

  * IDL（Interface description language），在web service是wsdl，在grpc是protobuf，在dubbo是java interface + po（普通值对象）
  
* 代理层

  * Stub 客户端桩

  * Skeleton 服务端框架（[ˈskelɪtn]）
  
* 链路层

  * 注册表/目录服务，在web service是UDDI，在grpc是etcd，在dubbo是注册中心（zookeeper）

* 传输层

  * 序列化/反序列化
  
  * 集群策略，比如：负载均衡、集群容错

  * 网络传输

* 运维支撑层

  * 监控
