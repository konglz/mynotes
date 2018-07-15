
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

### 2.1. 服务端

#### 2.1.1. io线程池

> netty的boss和worker线程池，默认为cached线程池

* boss：建立connection

  * accept客户端的连接；

  * 将接收到的连接注册到一个worker线程上

  * 通常情况下，服务端每绑定一个端口，开启一个boss线程

* worker：处理注册在其身上的连接connection上的各种io事件

  * 默认是：核数+1

  * 一个worker线程可以注册多个connection
  
  * 一个connection只能注册在一个worker线程上

#### 2.1.2. 业务线程池

* 默认为 fixedThreadPool

* 默认线程名大概是这样 “DubboServerHandler-10.10.10.11:20880”，可以通过配置方式自定义

  * 与worker配合处理各种请求
  
### 2.2. 客户端

* io线程池：netty的boss和worker线程池

* 业务线程池

  * 默认为 cachedThreadPool
  
  * 默认线程名大概是这样 “DubboClientHandler-10.10.10.10:20880”，也可以自定义


## 3. dubbo事件分配

> 框架事件分配给业务线程池

#### 3.1. 事件类型

* connected 连接成功

* disconnected 连接断开

* sent 请求

* received 响应

* 心跳

### 3.2. 线程池类型

* fixed：固定大小线程池，启动时建立线程，不关闭，一直持有。(缺省)

  * coresize：200
  
  * maxsize：200
  
  * 队列：SynchronousQueue
  
  * 拒绝策略：AbortPolicyWithReport - 打印线程信息jstack，之后抛出异常
  
* cached：缓存线程池，空闲一分钟自动删除，需要时重建。

* limited：可伸缩线程池，但池中的线程数只会增长不会收缩。只增长不收缩的目的是为了避免收缩时突然来了大流量引起的性能问题。

### 3.3. 分配策略

* 默认是all：所有消息都派发到线程池，包括请求，响应，连接事件，断开事件，心跳等。 即worker线程接收到事件后，将该事件提交到业务线程池中，自己再去处理其他事

* direct：worker线程接收到事件后，由worker执行到底

* message：只有请求响应消息派发到线程池，其它连接断开事件，心跳等消息，直接在 IO线程上执行

* execution：只请求消息派发到线程池，不含响应（客户端线程池），响应和其它连接断开事件，心跳等消息，直接在 IO 线程上执行

* connection：在 IO 线程上，将连接断开事件放入队列，有序逐个执行，其它消息派发到线程池。
