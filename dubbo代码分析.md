
## 1. RPC概述

### 1.1 RPC结构图

![RPC结构图](%E6%8E%A5%E5%8F%A3%E5%AE%9A%E4%B9%89%E8%AF%AD%E8%A8%80.jpg)

### 1.2. RPC的要素

* 接口层

  * IDL（Interface description language），在web service是wsdl，在grpc是protobuf，在dubbo是java interface + po（普通值对象）
  
  * 接口仓库，在web service是wsdl服务器，在grpc是gitlab + 文件，在dubbo一般是maven仓库（nexus）
  
* 代理层

  * Stub 客户端桩

  * Skeleton 服务端框架（[ˈskelɪtn]）
  
* 网络层

  * 注册表/目录服务，在web service是UDDI，在grpc是etcd，在dubbo是注册中心（zookeeper）
  
  * 集群策略，比如：负载均衡、集群容错

* 传输层

  * 序列化/反序列化

  * 数据传输

* 监控层

  * 监控
  
  * 访问日志
