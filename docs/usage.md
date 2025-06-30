# Kafka分布式消息中间件使用指南

# 一、商品链接

[Kafka分布式消息中间件](https://marketplace.huaweicloud.com/hidden/contents/92e0c0d9-6a15-41a3-b71f-caf3a8de0d81#productid=OFFI1129684662074359808)

# 二、商品说明

**Apache Kafka** 是一个分布式、支持分区（parition）、多副本（replica）的分布式消息系统，它由服务器和客户端组成，这些服务器和客户端通过 高性能 TCP 网络协议进行通信。Kafka可以部署在本地和云中的裸机硬件、虚拟机和容器 环境上，Kafka集群具有高度可扩展性和容错性。

# 三、商品购买

您可以在云商店搜索 **Kafka分布式消息中间件**。

其中，地域、规格、推荐配置使用默认，购买方式根据您的需求选择按需/按月/按年，短期使用推荐按需，长期使用推荐按月/按年，确认配置后点击“立即购买”。


## 3.1 使用 RFS 模板直接部署
![img.png](images/img1.png)
必填项填写后，点击 下一步
![img.png](images/img2.png)
![img.png](images/img3.png)
创建直接计划后，点击 确定
![img.png](images/img4.png)
![img.png](images/img5.png)
点击部署，执行计划
![img.png](images/img6.png)
如下图“Apply required resource success. ”即为资源创建完成
![img.png](images/img7.png)

##  3.2 ECS 控制台配置

### 准备工作

在使用ECS控制台配置前，需要您提前配置好 **安全组规则**。

> **安全组规则的配置如下：**
> - 入方向规则放通端口9092，源地址内必须包含您的客户端ip，否则无法访问
> - ZooKeeper 2181 Zookeeper 默认端口  
    ZooKeeper 2887、2888、2889 zk集群之间进行数据/心跳同步的端口  
    ZooKeeper 3887、3888、3889 zk集群之间进行领导者选举的端口  
> - 入方向规则放通 CloudShell 连接实例使用的端口 `22`，以便在控制台登录调试
> - 出方向规则一键放通

### 创建ECS

前提工作准备好后，选择 ECS 控制台配置跳转到[购买ECS](https://support.huaweicloud.com/qs-ecs/ecs_01_0103.html) 页面，ECS 资源的配置如下图所示：

选择CPU架构
![img.png](images/img8.png)
选择服务器规格
![img_1.png](images/img_1.png)
选择镜像
![img_2.png](images/img_2.png)
其他参数根据实际请客进行填写，填写完成之后，点击立即购买即可
![img_3.png](images/img_3.png)


> **值得注意的是：**
> - VPC 您可以自行创建
> - 安全组选择 [**准备工作**](#准备工作) 中配置的安全组；
> - 弹性公网IP选择现在购买，推荐选择“按流量计费”，带宽大小可设置为5Mbit/s；
> - 高级配置需要在高级选项支持注入自定义数据，所以登录凭证不能选择“密码”，选择创建后设置；
> - 其余默认或按规则填写即可。

# 四、商品使用

## 修改 /etc/hosts 域名
将 192.168.0.103 hadoop1 改成自己本机的私有 ip x.x.x.x hadoop1

## 执行/root 目录的 kafka.sh 命令，1.1.1.1 替换成自己使用的公网 ip
```bash
./kafka.sh 1.1.1.1
```
## jps查看服务是否启动成功
执行 kafka.sh 的命令有可能启动不了 zookeeper 或 kafka 服务，可以二次启动 kafka.sh脚本

## 手工启动 zookeeper 服务和 kafka 命令（如果服务没启动，根据以下命令手工启动）
zookeeper 服务停止和启动 (路径如有更改 换成本地实际使用路径)

/opt/software/zookeeper-3.5.7/bin/zkServer.sh stop  
/opt/software/zookeeper-3.5.7/bin/zkServer.sh start /opt/software/zookeeper3.5.7/conf/zoo.cfg #启动 zk

### kafka 服务停止和启动
停止 kafka 服务
/opt/software/kafka/bin/kafka-server-stop.sh  

后台启动kafka服务  
/opt/software/kafka/bin/kafka-server-start.sh -daemon /opt/software/kafka/config/server.properties

### 其它kafka相关命令参考:
#### Topic（主题）
创建 Topic  
bin/kafka-topics.sh --create --bootstrap-server hadoop01:9092 --replication-factor 3 --partitions 2 --topic test

查询所有 Topic 列表  
bin/kafka-topics.sh --list --bootstrap-server hadoop01:9092

删除 Topic  
bin/kafka-topics.sh --bootstrap-server hadoop01:9092 --delete --topic test

#### 单个 Topic 扩容
bin/kafka-topics.sh --bootstrap-server hadoop01:9092 --alter --topic test --partitions 3

#### Producer（生产者）
发送消息  
bin/kafka-console-producer.sh --broker-list hadoop01:9092 --topic test

发送消息，指定生产者参数 acks 为 -1，同时启用 LZ4 的压缩算法：  
bin/kafka-console-producer.sh --broker-list hadoop01:9092 --topic test --request-required-acks -1 --producer-property compression.type=lz4

#### Consumer（消费者）
消费消息 从头开始消费（--from-beginning 参数表示从该主题最早的位移开始消费）  
bin/kafka-console-consumer.sh --bootstrap-server hadoop01:9092 --topic test --frombeginning

指定消费者组    
bin/kafka-console-consumer.sh --bootstrap-server hadoop01:9092 --topic test --frombeginning --group group01

从头开始消费（--from-beginning 参数表示从该主题最早的位移开始消费）    
bin/kafka-console-consumer.sh --bootstrap-server hadoop01:9092 --topic test --frombeginning --max-messages 100  
说明：--max-messages 100 , 表示消费 100 条记录后，停止消费。

#### Consumer_groups（消费者组）
查看消费者组的消费情况  
bin/kafka-consumer-groups.sh --bootstrap-server hadoop01:9092 --describe --group group01

查看所有消费者组提交的位移数据  
对于 __consumer_offsets 而言，由于它保存了消费者组的位移数据，直接查看该主题消息是很方便的事情。下面的命令可以帮助我们直接查看消费者组提交的位移数据。   
bin/kafka-console-consumer.sh --bootstrap-server hadoop01:9092 --topic __consumer_offsets --formatter "kafka.coordinator.group.GroupMetadataManager$OffsetsMessageFormatter" --from-beginning 

除了查看位移提交数据，我们还可以直接读取该主题消息，查看消费者组的状态信息。  
bin/kafka-console-consumer.sh --bootstrap-server hadoop01:9092 --topic __consumer_offsets --formatter "kafka.coordinator.group.GroupMetadataManager$GroupMetadataMessageFormatter" --frombeginning

## 参考文档

[Kafka官网](https://kafka.apache.org/)
