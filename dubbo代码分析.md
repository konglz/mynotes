
## 1. RPC概述

### 1.1. 什么是RPC

RPC（Remote Procedure Call），远程过程调用，调远程机器上的方法与调本地的看起来一样，是微服务的基石

### 1.2. 常见的RPC

* corba

* web service

* grpc

* dubbo

### 1.3. RPC结构图

![RPC结构图](%E6%8E%A5%E5%8F%A3%E5%AE%9A%E4%B9%89%E8%AF%AD%E8%A8%80.jpg)

### 1.4. RPC的要素

#### 1.4.1. 接口层

> 主要解决方法映射问题，保证客户端调的方法，正好是服务端提供的方法

* IDL（Interface definition language），在web service是wsdl，在grpc是protobuf，在dubbo是java interface + po（普通值对象）
  
* 接口仓库，在web service是wsdl服务器，在grpc是gitlab + 文件，在dubbo一般是maven仓库（nexus）
  
#### 1.4.2. 代理层

* Stub 客户端桩

* Skeleton 服务端框架（[ˈskelɪtn]）
  
#### 1.4.3. 网络层

* 注册表/目录服务，在web service是UDDI，在grpc是etcd，在dubbo是注册中心（zookeeper）
  
* 集群策略，比如：负载均衡、集群容错

#### 1.4.4. 传输层

* 序列化/反序列化

* 数据传输

#### 1.4.5. 监控层

* 监控
  
* 访问日志

## 2. dubbo线程模型
