# Spark 引擎使用文档

本文主要介绍在Linkis1.0中，spark引擎的配置、部署和使用。

## 1.Spark引擎使用前的环境配置

如果您希望在您的服务器上使用spark引擎，您需要保证以下的环境变量已经设置正确并且引擎的启动用户是有这些环境变量的。

强烈建议您在执行spark任务之前，检查下执行用户的这些环境变量。

| 环境变量名      | 环境变量内容   | 备注                                   |
|-----------------|----------------|----------------------------------------|
| JAVA_HOME       | JDK安装路径    | 必须                                   |
| HADOOP_HOME     | Hadoop安装路径 | 必须                                   |
| HADOOP_CONF_DIR | Hadoop配置路径 | 必须                                   |
| HIVE\_CONF_DIR  | Hive配置路径   | 必须                                   |
| SPARK_HOME      | Spark安装路径  | 必须                                   |
| SPARK_CONF_DIR  | Spark配置路径  | 必须                                   |
| python          | python         | 建议使用anaconda的python作为默认python |

表1-1 环境配置清单

## 2.Spark引擎的配置和部署

### 2.1 spark版本的选择和编译

理论上Linkis1.0支持的spark2.x以上的所有版本。默认支持的版本Spark2.4.3。如果您想使用您的spark版本，如spark2.1.0，则您仅仅需要将插件spark的版本进行修改，然后进行编译即可。具体的，您可以找到linkis-engineplugin-spark模块，将\<spark.version\>标签进行改成2.1.0，然后单独编译此模块即可。

### 2.2 spark engineConn部署和加载

如果您已经编译完了您的spark引擎的插件已经编译完成，那么您需要将新的插件放置到指定的位置中才能加载，具体可以参考下面这篇文章

https://github.com/WeBankFinTech/Linkis/wiki/EngineConnPlugin%E5%BC%95%E6%93%8E%E6%8F%92%E4%BB%B6%E5%AE%89%E8%A3%85%E6%96%87%E6%A1%A3

### 2.3 spark引擎的标签

Linkis1.0是通过标签来进行的，所以需要在我们数据库中插入数据，插入的方式如下文所示。

<!-- 此链接有问题 ->
https://github.com/WeBankFinTech/Linkis/wiki/EngineConnPlugin%E5%BC%95%E6%93%8E%E6%8F%92%E4%BB%B6%E5%AE%89%E8%A3%85%E6%96%87%E6%A1%A3\#22-%E7%AE%A1%E7%90%86%E5%8F%B0configuration%E9%85%8D%E7%BD%AE%E4%BF%AE%E6%94%B9%E5%8F%AF%E9%80%89

## 3.spark引擎的使用

### 准备操作，队列设置

因为spark的执行是需要队列的资源，所以用户在执行之前，必须要设置自己能够执行的队列。

![](../Images/EngineUsage/queue-set.png)

图3-1 队列设置

### 3.1 Scriptis的使用方式

Scriptis的使用方式是最简单的，您可以直接进入Scriptis，新建sql、scala或者pyspark脚本进行执行。

sql的方式是最简单的，您可以新建sql脚本然后编写进行执行，执行的时候，会有进度的显示。如果一开始用户是没有spark引擎的话，sql的执行会启动一个spark会话(这里可能会花一些时间)，
SparkSession初始化之后，就可以开始执行sql。

![](../Images/EngineUsage/sparksql-run.png)

图3-2 sparksql的执行效果截图

spark-scala的任务，我们已经初始化好了sqlContext等变量，用户可以直接使用这个sqlContext进行sql的执行。

![](../Images/EngineUsage/scala-run.png)

图3-3 spark-scala的执行效果图

类似的，pyspark的方式中，我们也已经初始化好了SparkSession，用户可以直接使用spark.sql的方式进行执行sql。

![](../Images/EngineUsage/pyspakr-run.png)
图3-4 pyspark的执行方式

### 3.2工作流的使用方式

DSS工作流也是有spark的三个节点，您可以拖入工作流节点，如sql、scala或者pyspark节点，然后双击进入然后进行编辑代码，然后以工作流的形式进行执行。

![](../Images/EngineUsage/workflow.png)

图3-5 工作流执行spark的节点

### 3.3 Linkis Client的使用方式

Linkis也提供了client的方式进行调用spark的任务，调用的方式是通过LinkisClient提供的SDK的方式。我们提供了java和scala两种方式进行调用，具体的使用方式可以参考<https://github.com/WeBankFinTech/Linkis/wiki/Linkis1.0%E7%94%A8%E6%88%B7%E4%BD%BF%E7%94%A8%E6%96%87%E6%A1%A3>。

## 4.spark引擎的用户设置

除了以上引擎配置，用户还可以进行自定义的设置，比如spark会话executor个数和executor的内存。这些参数是为了用户能够更加自由地设置自己的spark的参数，另外spark其他参数也可以进行修改，比如的pyspark的python版本等。

![](../Images/EngineUsage/spark-conf.png)

图4-1 spark的用户自定义配置管理台
