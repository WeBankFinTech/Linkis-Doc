> Linkis0.x版本在微众银行生产上稳定运行，并支撑着各种业务，Linkis1.0作为0.x的优化版本，相关调优逻辑并没有改变，所以本文档会介绍几个生产上Linkis部署调优的建议，由于篇幅有限，本文并不能覆盖到所有的优化场景，相关调优指南也会补充更新，当然也希望社区用户为Linkis1.0的调优文档提出建议。  

## 1. 概述
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本文档将会按照生产的经验，介绍几个调优的手段，分别是生产上部署时Jvm堆大小选取，任务提交的并发量设置，任务运行资源申请参数介绍。文档中叙述的参数设置，并不是建议设置的参数值，用户需要根据自己真实地生产环境，对参数进行选取。


## 2. Jvm堆大小调优
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在安装Linkis时，可以在linkis-env.sh中找到以下变量：
```shell
SERVER_HEAP_SIZE="512M"
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;设置该变量，在安装后，会加入到每个微服务的java启动参数中，用来控制Jvm启动堆大小，虽然在java启动时，需要设置xms和xmx两个参数，但是通常会设置成一样的值，在生产上，随着使用人数的增多，该参数需要调整大一些才能满足生产的需求。当然设置更大的堆栈内存，需要更大的服务器配置，当然，单机部署存在局限性，在生产上，可以采用分布式部署的方式，用多台服务器分别部署不同的Linkis和DSS微服务，同时调整堆栈大小，达到满足生产的需求。

## 3. 任务提交的并发量调优
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Linkis的一些任务并发参数都会有一个默认值，大多数场景下默认值都可以满足需求，但是有时，默认值并不能满足需求，所以需要通过改变参数的大小进行调整，本文会介绍几个调整任务并发的参数。方便用户对生产上的并发任务进行优化。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;因为任务的提交都是采用RPC的方式，在linkis-common/linkis-rpc模块中，可以通过配置如下几个参数提高rpc的并发数量：
```shell
wds.linkis.rpc.receiver.asyn.consumer.thread.max=400
wds.linkis.rpc.receiver.asyn.queue.size.max=5000
wds.linkis.rpc.sender.asyn.consumer.thread.max=100
wds.linkis.rpc.sender.asyn.queue.size.max=2000
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在Linkis源码中，我们对提交任务的并发数设置了一个默认值，该值在绝大多数场景下都能很好的满足需求，但是在有些场景出现大量并发任务提交执行时，比如用Qualitis（微众银行另一款开源项目）进行大批量数据校验时，这个参数在目前的版本中并没有提升为可配置项，分别是initCapacity，maxCapacity两个参数，需要用户进行改造，提高这两个参数，可以提高并发数，当然也需要更高的服务器配置。
```java
  private val groupNameToGroups = new JMap[String, Group]
  private val labelBuilderFactory = LabelBuilderFactoryContext.getLabelBuilderFactory

  override def getOrCreateGroup(groupName: String): Group = {
    if (!groupNameToGroups.containsKey(groupName)) synchronized {
      val initCapacity = 100
      val maxCapacity = 100
      // 其它代码...
        }
      }
```

## 4. 任务运行时资源设置
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在提交任务运行在Yarn上时，Yarn提供了可配置的接口，Linkis作为一个可拓展性强的框架，同样也可以通过Linkis的配置来设置资源配置。  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Spark的相关配置和Hive的相关配置如下：  
在linkis-engineconn-plugins/engineconn-plugins里的Spark的部分配置，可以调整该配置改变提交到Yarn上的任务运行时环境，由于篇幅有限，如更多有关Hive，Yarn配置需要用户参考源码和参数文档:
```shell
"spark.driver.memory" = 2 //单位为G
"wds.linkis.driver.cores" = 1
"spark.executor.memory" = 4 //单位为G
"spark.executor.cores" = 2
"spark.executor.instances" = 3
"wds.linkis.rm.yarnqueue" = "default"
```