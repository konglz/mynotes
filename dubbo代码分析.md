
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

## 3. netty 线程模型

### 3.1. boss线程

#### 3.1.1. 作用：

* accept客户端的连接；

* 将接收到的连接注册到一个worker线程上

#### 3.1.2. 个数：

* 通常情况下，服务端每绑定一个端口，开启一个boss线程

### 3.2. worker线程

#### 3.2.1. 作用：

* 处理注册在其身上的连接connection上的各种io事件

#### 3.2.2. 个数：

* 默认是：核数+1

## 3.3. 注意：

* 一个worker线程可以注册多个connection

* 一个connection只能注册在一个worker线程上
