> Linkis1.0在0.x的基础上做了大量优化，在结构上减少了微服务的数量，当然Linkis1.0的各个微服务的高可配有点，也被继承了下来，不过1.0在0.x配置的基础上进行了简化，在安装后提供了一个公共配置的文件，避免出现同一个配置出现在多个地方的情况。本文档将会把Linkis1.0的参数分模块列举出来。

## 1. Linkis参数列表
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;为了叙述的方便，在以下配置参数中，括号右边为key值，左边为value。可以在对应的微服务中properties文件中进行配置，当配置时，会覆盖默认参数。当然，本文档的参数仅仅只做参考，因为部署的环境差异，为了您更好的使用Linkis，强烈建议在配置相关参数，同时结合源码进行适配。一般在配置时，如果参数值为字符串，需要在配置时带上引号，除字符串类型之外的参数，则不需要。

---
linkis-commons/linkis-common：
```shell
 ("wds.linkis.encoding", "utf-8")
 ("wds.linkis.date.pattern", "yyyy-MM-dd'T'HH:mm:ssZ")
 ("wds.linkis.field.split", "hadoop")
 ("wds.linkis.test.mode", false)
 ("wds.linkis.home",  ("LINKIS_HOME", "/appcom/Install/LinkisInstall"))
 ("wds.linkis.gateway.url", "http://127.0.0.1:9001/")
 ("wds.linkis.ldap.proxy.url", "")
 ("wds.linkis.ldap.proxy.baseDN", "")
 ("wds.linkis.ldap.proxy.userNameFormat", "")
```

linkis-commons/linkis-hadoop-common：
```shell
 ("wds.linkis.hadoop.root.user", "hadoop")
 ("wds.linkis.keytab.enable", false)
 ("wds.linkis.keytab.file", "/appcom/keytab/")
 ("wds.linkis.keytab.host", "127.0.0.1")
 ("wds.linkis.keytab.host.enabled", false)
 ("hadoop.config.dir",  ("HADOOP_CONF_DIR", ""))
 ("wds.linkis.hadoop.external.conf.dir.prefix", "/appcom/config/external-conf/hadoop")
 ```

 linkis-commons/linkis-httpclient：
 ```shell
 ("wds.linkis.httpclient.default.connect.timeOut", 50000)
 ```

 linkis-commons/linkis-message-scheduler：
 ```shell
("wds.linkis.ms.service.scan.package", "com.webank.wedatasphere")
("wds.linkis.ms.rpc.sync.timeout", 60 * 1000 * 5L)
```

linkis-commons/linkis-module：
```shell
 ("wds.linkis.data.operate", "false")
 ("wds.linkis.server.component.exclude.packages", "")
 ("wds.linkis.server.component.exclude.classes", "")
 ("wds.linkis.server.component.exclude.annotation", "")
 ("wds.linkis.server.spring.application.listeners", "")
 ("wds.linkis.server.version", "")
 ("wds.linkis.crypt.key", "bdp-for-server"
 ("wds.linkis.ticket.header", "bfs_")
 ("wds.linkis.test.user", "")
 ("wds.linkis.server.home",  ("BDP_SERVER_HOME", ""))
 ("wds.linkis.server.distinct.mode", new Boolean(true))
 ("wds.linkis.server.socket.mode", new Boolean(false))
 ("wds.linkis.server.ident.string", "true")
 ("wds.linkis.server.jetty.name", "")
 ("wds.linkis.server.address", Utils.getLocalHostname)
 ("wds.linkis.server.port", 20303)
 ("wds.linkis.server.security.filter", "com.webank.wedatasphere.linkis.server.security.SecurityFilter")
 ("wds.linkis.server.security.referer.validate", false)
 ("wds.linkis.server.security.ssl", false)
 ("wds.linkis.server.security.ssl.excludeProtocols", "SSLv2,SSLv3")
 ("wds.linkis.server.security.ssl.keystore.path",
 ("wds.linkis.server.security.ssl.keystore.type", "JKS")
 ("wds.linkis.server.security.ssl.keystore.password", "")
 ("wds.linkis.server.security.ssl.key.manager.password", "")
 ("wds.linkis.server.security.ssl.cipher.suites",
 ("wds.linkis.server.context.path", "/")
 ("wds.linkis.server.restful.uri", "/api/rest_j/" + BDP_SERVER_VERSION)
 ("wds.linkis.server.user.restful.uri", "/api/rest_j/" + BDP_SERVER_VERSION + "/user")
 ("wds.linkis.server.user.restful.login.uri", new File(BDP_SERVER_USER_URI.getValue, "login").getPath)
 ("wds.linkis.server.user.security.ssl.uri", new File(BDP_SERVER_USER_URI.getValue, "publicKey").getPath)
 ("wds.linkis.server.socket.uri", "/ws")
 ("wds.linkis.server.socket.login.uri", "/ws/user/login")
 ("wds.linkis.server.war", new File(BDP_SERVER_HOME.getValue, "web/dist").getPath)
 ("wds.linkis.server.war.tempdir", new File(BDP_SERVER_HOME.getValue, "web/webapps").getPath)
 ("wds.linkis.server.default.dir.allowed", "false")
 ("wds.linkis.server.web.session.timeout", new TimeType("2h"))
 ("wds.linkis.server.event.queue.size", 5000)
 ("wds.linkis.server.event.consumer.thread", 10)
 ("wds.linkis.server.event.consumer.thread.max.free", new TimeType("2m"))
 ("wds.linkis.server.socket.queue.size", BDP_SERVER_EVENT_CONSUMER_THREAD_SIZE.getValue * 20)
 ("wds.linkis.server.socket.text.message.size.max", "1024000")
 ("wds.linkis.server.restful.scan.packages", "")
 ("wds.linkis.server.restful.register.classes", "")
 ("wds.linkis.server.socket.service.scan.packages", BDP_SERVER_RESTFUL_SCAN_PACKAGES.getValue)
 ("wds.linkis.is.gateway", "false")
```

linkis-commons/linkis-mybatis：
```shell
 ("wds.linkis.server.mybatis.mapperLocations", "")
 ("wds.linkis.server.mybatis.typeAliasesPackage", "")
 ("wds.linkis.server.mybatis.configLocation", "classpath:/mybatis-config.xml")
 ("wds.linkis.server.mybatis.BasePackage", "")
 ("wds.linkis.server.mybatis.datasource.url", "")
 ("wds.linkis.server.mybatis.datasource.username", "")
 ("wds.linkis.server.mybatis.datasource.password", "")
 ("wds.linkis.server.mybatis.datasource.driver-class-name", "com.mysql.jdbc.Driver")
 ("wds.linkis.server.mybatis.datasource.initialSize", new Integer(1))
 ("wds.linkis.server.mybatis.datasource.minIdle", new Integer(1))
 ("wds.linkis.server.mybatis.datasource.maxActive", new Integer(20))
 ("wds.linkis.server.mybatis.datasource.maxWait", new Integer(6000))
 ("wds.linkis.server.mybatis.datasource.timeBetweenEvictionRunsMillis", new Integer(60000))
 ("wds.linkis.server.mybatis.datasource.minEvictableIdleTimeMillis", new Integer(300000))
 ("wds.linkis.server.mybatis.datasource.validationQuery", "SELECT 1")
 ("wds.linkis.server.mybatis.datasource.testWhileIdle", new Boolean(true))
 ("wds.linkis.server.mybatis.datasource.testOnBorrow", new Boolean(false))
 ("wds.linkis.server.mybatis.datasource.testOnReturn", new Boolean(false))
 ("wds.linkis.server.mybatis.datasource.poolPreparedStatements", new Boolean(true))
 ```
 
 
linkis-commons/linkis-protocol：
```shell
 ("wds.linkis.service.suffix","engineManager,entrance,engine")
 ```


linkis-commons/linkis-rpc：
```shell
 ("wds.linkis.rpc.broadcast.thread.num", new Integer(10))
 ("wds.linkis.rpc.eureka.client.refresh.interval", new TimeType("1s"))
 ("wds.linkis.rpc.eureka.client.refresh.wait.time.max", new TimeType("1m"))
 ("wds.linkis.rpc.receiver.asyn.consumer.thread.max", 10)
 ("wds.linkis.rpc.receiver.asyn.consumer.freeTime.max", new TimeType("2m"))
 ("wds.linkis.rpc.receiver.asyn.queue.size.max", 1000)
 ("wds.linkis.rpc.sender.asyn.consumer.thread.max", 5)
 ("wds.linkis.rpc.sender.asyn.consumer.freeTime.max", new TimeType("2m"))
 ("wds.linkis.rpc.sender.asyn.queue.size.max", 300)
 ("wds.linkis.gateway.conf.enable.publicservice", true)
 ("wds.linkis.gateway.conf.publicservice.name", "publicservice")
 ("wds.linkis.gateway.conf.publicservice.list", "query,jobhistory,application,configuration,filesystem,udf,variable").getValue.split(",")) #用逗号隔开
 ("wds.linkis.rpc.instancealias.refresh.interval", new TimeType("3s"))
 ("wds.linkis.gateway.conf.contextservice.name", "linkis-ps-contextservice")
 ```
 
linkis-commons/linkis-scheduler：
```shell
 ("wds.linkis.fifo.consumer.auto.clear.enabled", true)
 ("wds.linkis.fifo.consumer.max.idle.time", new TimeType("2h"))
 ("wds.linkis.fifo.consumer.idle.scan.interval", new TimeType("6h"))
 ("wds.linkis.fifo.consumer.idle.scan.init.time", new TimeType("1s"))
 ```
 
 
linkis-computation-governance/linkis-computation-governance-common:
 ```shell
 ("wds.linkis.spark.engine.version", "2.4.3")
 ("wds.linkis.hive.engine.version", "1.2.1") 
 ("wds.linkis.python.engine.version", "python2")
 ("wds.linkis.engineconn.name", "EngineConn")
 ("wds.linkis.engineconn.manager.name", "linkis-cg-engineconnmanager")
 ("wds.linkis.engineconn.manager.name", "linkis-cg-linkismanager")
 ("wds.linkis.entrance.name", "linkis-cg-entrance")
```

linkis-computation-governance/linkis-engineconn/linkis-computation-engineconn:
```shell
 ("wds.linkis.engineconn.resultSet.default.store.path", "hdfs:///tmp")
 ("wds.linkis.engine.resultSet.cache.max", new ByteType("0k"))
 ("wds.linkis.engine.default.limit", 5000)
 ("wds.linkis.engine.lock.expire.time", 2 * 60 * 1000)
```

linkis-computation-governance/linkis-engineconn/linkis-engineconn-common:
```shell
 ("wds.linkis.engine.connector.executions", "com.webank.wedatasphere.linkis.engineconn.computation.executor.execute.ComputationEngineConnExecution")
 ("wds.linkis.engine.connector.hooks", "com.webank.wedatasphere.linkis.engineconn.computation.executor.hook.ComputationEngineConnHook")
 ("wds.linkis.engine.launch.cmd.params.user.key", "user")
 ("wds.linkis.engine.parallelism.support.enabled", false)
 ("wds.linkis.engine.push.log.enable", true)
 ("wds.linkis.engineconn.plugin.default.clazz", "com.webank.wedatasphere.linkis.engineplugin.hive.HiveEngineConnPlugin")
 ("wds.linkis.engine.task.expire.time", 1000 * 3600 * 24)
 ("wds.linkis.engine.lock.refresh.time", 1000 * 60 * 3)
 ("wds.linkis.engine.localpath.pwd.key", "PWD")
 ("wds.linkis.engine.logs.dir.key", "LOG_DIRS")
 ```


linkis-computation-governance/linkis-engineconn/linkis-engineconn-executor/accessible-executor:
```shell
 ("wds.linkis.engineconn.log.cache.default", 500)
 ("wds.linkis.engineconn.ignore.words", "org.apache.spark.deploy.yarn.Client")
 ("wds.linkis.engineconn.pass.words", "org.apache.hadoop.hive.ql.exec.Task")
 ("wds.linkis.engineconn.log.send.once", 100)
 ("wds.linkis.engineconn.log.send.time.interval", 3)
 ("wds.linkis.engineconn.max.free.time", new TimeType("1h"))
 ("wds.linkis.engineconn.support.parallelism", false)
 ("wds.linkis.engineconn.heartbeat.time", new TimeType("3m"))
```

linkis-computation-governance/linkis-engineconn/linkis-engineconn-executor/executor-core:
```shell
 ("wds.linkis.dataworkclod.engine.tmp.path", "file:///tmp/")
 ("wds.linkis.engine.application.name", "")
 ("wds.linkis.log4j2.prefix", "/appcom/logs/linkis/" + ENGINE_SPRING_APPLICATION_NAME.getValue)
 ("wds.linkis.log.clear", false)
 ("wds.linkis.engine.ignore.words", "org.apache.spark.deploy.yarn.Client")
 ("wds.linkis.engine.pass.words", "org.apache.hadoop.hive.ql.exec.Task")
 ("wds.linkis.entrance.application.name", "linkis-cg-entrance")
 ("wds.linkis.engine.listener.async.queue.size.max", 300)
 ("wds.linkis.engine.listener.async.consumer.thread.max", 5)
 ("wds.linkis.engine.listener.async.consumer.freetime.max", new TimeType("5000ms"))
 ("wds.linkis.engineconn.executor.manager.service.clazz", "com.webank.wedatasphere.linkis.engineconn.acessible.executor.service.DefaultManagerService")
 ("wds.linkis.engineconn.executor.default.name", "ComputationExecutor")
 ```

linkis-computation-governance/linkis-engineconn-manager/linkis-engineconn-manager-server:
```shell
 ("wds.linkis.ecm.async.bus.capacity", 500)
 ("wds.linkis.ecm.async.bus.name", "em_async_bus")
 ("wds.linkis.ecm.async.bus.consumer.size", 30)
 ("wds.linkis.ecm.async.bus.max.free.time", ByteTimeUtils.timeStringAsMs("2m"))
 ("wds.linkis.ecm.async.bus.waittoempty.time", 5000L)
 ("wds.linkis.ecm.memory.max", ByteTimeUtils.byteStringAsBytes("80g"))
 ("wds.linkis.ecm.cores.max", 50)
 ("wds.linkis.ecm.engineconn.instances.max", 50)
 ("wds.linkis.ecm.protected.memory", ByteTimeUtils.byteStringAsBytes("4g"))
 ("wds.linkis.ecm.protected.cores.max", 2)
 ("wds.linkis.ecm.protected.engine.instances", 2)
 ("wds.linkis.ecm.health.report.period", 5)
 ("wds.linkis.ecm.health.report.delay", 10)
 ("wds.linkis.engineconn.spring.name", "linkis-cg-engineplugin")
 ("wds.linkis.ecm.home.dir", this.getClass.getResource("/").getPath)
 ("wds.linkis.engineconn.root.dir", s"${ECM_HOME_DIR}engineConnRootDir")
 ("wds.linkis.engineconn.public.dir", s"$ENGINECONN_ROOT_DIR${File.separator}engineConnPublickDir")
 ("wds.linkis.ecm.launch.max.thread.size", 100)
 ("wds.linkis.eureka.defaultZone", "http://127.0.0.1:20303/eureka/")
 ("wds.linkis.ecm.engineconn.create.duration", 0) # TimeUnit.MILLISECONDS
 ("wds.linkis.engineconn.wait.callback.pid", new TimeType("3s"))
 ```


linkis-computation-governance/linkis-entrance:
```shell
 ("wds.linkis.entrance.scheduler.maxParallelismUsers", new Integer(1000))
 ("wds.linkis.entrance.listenerBus.queue.capacity", new Integer(5000))
 ("wds.linkis.entrance.job.persist.wait.max", new TimeType("5m"))
 ("wds.linkis.entrance.multi.entrance.flag", true)
 ("wds.linkis.resultSet.store.path",  ("wds.linkis.filesystem.hdfs.root.path").getValue)
 ("wds.linkis.query.application.name", "linkis-ps-publicservice")
 ("wds.linkis.entrance.config.log.path",  ("wds.linkis.filesystem.hdfs.root.path").getValue)
 ("wds.linkis.entrance.log.cacheMax", 500)
 ("wds.linkis.entrance.log.defaultCharSet", "utf-8")
 ("wds.linkis.console.configuration.application.name", "linkis-ps-publicservice")
 ("wds.linkis.console.variable.application.name", "linkis-ps-publicservice")
 ("wds.linkis.console.config.logPath", "wds.linkis.config.logPath")
 ("wds.linkis.default.requestApplication.name", "IDE")
 ("wds.linkis.default.runType", "sql")
 ("wds.linkis.default.create.service", "dss")
 ("wds.linkis.warn.log.exclude", "org.apache,hive.ql,hive.metastore,com.netflix,com.webank.wedatasphere")
 ("wds.linkis.log.clear", false)
 ("wds.linkis.log.exclude", "org.apache,hive.ql,hive.metastore,com.netflix,com.webank.wedatasphere,com.webank")
 ("wds.linkis.instance", 3)
 ("wds.linkis.log.exclude.all", "com.netflix")
 ("wds.linkis.max.ask.executor.time", new TimeType("5m"))
 ("wds.linkis.errorcode.file.dir", "")
 ("wds.linkis.entrance.user", "")
 ("wds.linkis.errorcode.file", "")
 ("wds.linkis.hive.special.log.include", "org.apache.hadoop.hive.ql.exec.Task")
 ("wds.linkis.share.file.prefix", "")
 ("wds.linkis.hive.thread.name", "[Thread")
 ("wds.linkis.hive.stage.name", "Stage-")
 ("wds.linkis.spark.special.log.include", "com.webank.wedatasphere.linkis.engine.spark.utils.JobProgressUtil")
 ("wds.linkis.spark.progress.name", "com.webank.wedatasphere.linkis.engine.spark.utils.JobProgressUtil$")
 ("bdp.dataworkcloud.entrance.end.flag", "info -")
 ("wds.linkis.hive.create.table.log", "numFiles")
 ("wds.linkis.hive.printinfo.log", "printInfo -")
 ("wds.linkis.entrance.datawmap.appid", "75116e6f690e6d222fb55f2dd6f9cb5a")
 ("wds.linkis.entrance.datamap.apptoken",
 ("wds.linkis.entrance.datamap.ip", "")
 ("wds.linkis.entrance.datamap.port", "9001")
 ("wds.linkis.entrance.bdp.env", "true")
 ("wds.linkis.entrance.shell.danger.check.enabled", false)
 ("wds.linkis.shell.danger.usage", "rm,sh,find,kill,python,for,source,hdfs,hadoop,spark-sql,spark-submit,pyspark,spark-shell,hive,yarn")
 ("wds.linkis.shell.white.usage", "cd,ls")
 ("wds.linkis.entrance.flow.creator", "nodeexecution")
 ("wds.linkis.entrance.scheduler.creator", "scheduler")
 ("wds.linkis.entrance.is.qml", false)
 ("wds.linkis.entrance.push.progress", "false")
 ("wds.linkis.concurrent.group.factory.capacity", 1000)
 ("wds.linkis.concurrent.group.factory.running.jobs", 30)
 ("wds.linkis.concurrent.group.factory.executor.time", 5 * 60 * 1000)
 ("wds.linkis.enginemanager.application.name", "linkis-cg-engineconnmanager")
 ("wds.linkis.entrance.engine.lastupdate.timeout", new TimeType("5s"))
 ("wds.linkis.entrance.engine.timeout", new TimeType("10s"))
 ("wds.linkis.entrance.engine.activity_monitor.interval", new TimeType("3s"))
 ("wds.linkis.sql.default.limit", 5000)
 ```


linkis-computation-governance/linkis-entrance-client:
```shell
 ("wds.linkis.client.enginemanager.application.name.default", "IOEngineManager")
 ("wds.linkis.client.engine.application.name.default", "IOEngine")
 ("wds.linkis.client.name.default", "storageClient")
 ("wds.linkis.client.parallelism.users.max", new Integer(100))
 ("wds.linkis.client.rpc.receiver.asyn.queue.size.max", new Integer(3000))
 ("wds.linkis.client.rpc.receiver.asyn.consumer.thread.max", new Integer(120))
 ("wds.linkis.client.engine.maxParallelismJobs", new Integer(25))
 ```


linkis-computation-governance/linkis-jdbc-driver:
```shell
 ("wds.linkis.jdbc.pre.hook.class", "com.webank.wedatasphere.linkis.ujes.jdbc.hook.impl.TableauPreExecutionHook")
```

linkis-computation-governance/linkis-manager/label-common:
```shell
 ("wds.linkis.label.label.com.webank.wedatasphere.linkis.entrance.factory.clazz", "");
 ("wds.linkis.label.scorer.base.core", 1.0d)
 ("wds.linkis.label.scorer.relate.limit", 2)
 ("wds.linkis.label.entity.packages", "")
 ("wds.linkis.spark.engine.version", "2.4.3")
 ("wds.linkis.hive.engine.version", "1.2.1")
 ("wds.linkis.python.engine.version", "python2")
 ("wds.linkis.file.engine.version", "1.0")
 ("wds.linkis.file.engine.version", "1.0")
 ("wds.linkis.jdbc.engine.version", "4")
 ("wds.linkis.pipeline.engine.version", "1")
 ("wds.linkis.shell.engine.version", "1")
 ("wds.linkis.appconn.engine.version", "v1")
 ```


linkis-computation-governance/linkis-manager/linkis-application-manager:
```shell
 ("wds.linkis.manager.am.engine.start.max.time", new TimeType("10m"))
 ("wds.linkis.manager.am.engine.reuse.max.time", new TimeType("5m"))
 ("wds.linkis.manager.am.engine.reuse.count.limit", 10)
 ("wds.linkis.manager.am.node.heartbeat", new TimeType("3m"))
 ("wds.linkis.manager.am.node.heartbeat", new TimeType("5m"))
 ("wds.linkis.manager.am.default.node.owner", "hadoop")
 ("wds.linkis.manager.am.stop.engine.wait", new TimeType("5m"))
 ("wds.linkis.manager.am.stop.em.wait", new TimeType("5m"))
 ("wds.linkis.manager.am.em.label.init.wait", new TimeType("5m"))
 ("wds.linkis.console.config.application.name", "linkis-ps-publicservice")
 ("wds.linkis.engineconn.application.name", "linkis-cg-engineplugin")
 ("wds.linkis.engineconn.debug.mode.enable", false)
 ("wds.linkis.multi.user.engine.types", "jdbc,es,presto")
 ```


linkis-computation-governance/linkis-manager/linkis-manager-commons/linkis-manager-common:
```shell
 ("wds.linkis.default.engine.type", "spark")
 ("wds.linkis.default.engine.type", "2.4.3")
 ("wds.linkis.manager.admin", "hadoop")
```

linkis-computation-governance/linkis-manager/linkis-manager-commons/linkis-resource-manager-common:
```shell
 ("wds.linkis.rm.application.name", "ResourceManager")
 ("wds.linkis.rm.wait.event.time.out", 1000 * 60 * 10L)
 ("wds.linkis.rm.register.interval.time", 1000 * 60 * 2L)
 ("wds.linkis.manager.am.node.heartbeat", new TimeType("3m"))
 ("wds.linkis.manager.am.node.heartbeat", new TimeType("5m"))
 ("wds.linkis.rm.client.core.max", 10)
 ("wds.linkis.rm.client.memory.max", new ByteType("20g"))
 ("wds.linkis.rm.instance", 10)
 ("wds.linkis.rm.yarnqueue.cores.max", 150)
 ("wds.linkis.rm.yarnqueue.memory.max", new ByteType("450g"))
 ("wds.linkis.rm.yarnqueue.instance.max", 30)
 ("wds.linkis.rm.yarnqueue", "default")
 ("wds.linkis.rm.cluster", "sit")
 ("wds.linkis.rm.user.module.wait.used", 60 * 10L)
 ("wds.linkis.rm.user.module.wait.used", -1L)
 ("wds.linkis.rm.module.completed.scan.interval", 10000L)
 ("wds.linkis.rm.engine.scan.interval", 120000L)
 ("wds.linkis.rm.engine.release.threshold", 120000L)
 ("wds.linkis.rm.conf.application.name", "linkis-ps-publicservice")
 ("wds.linkis.rm.alert.system.id", "5136")
 ("wds.linkis.rm.alert.default.um", "enjoyyin,johnnwang,shanhuang")
 ("wds.linkis.rm.alert.ims.url", "127.0.0.1")
 ("wds.linkis.rm.alert.duplication.interval", 1200L)
 ("wds.linkis.rm.alert.contact.group", "q01/cooperyang johnnwang,q02/shanhuang")
 ("wds.linkis.rm.alert.default.contact", "shanhuang")
 ("wds.linkis.rm.alert.enabled", false)
 ("wds.linkis.rm.publicservice.name", "linkis-ps-publicservice")
 ("wds.linkis.hive.maintain.time.key", "wds.linkis.hive.maintain.time")
 ("wds.linkis.rm.default.yarn.cluster.name", "sit")
 ("wds.linkis.rm.default.yarn.cluster.type", "Yarn")
 ```


linkis-computation-governance/linkis-manager/linkis-manager-monitor:
```shell
 ("wds.linkis.manager.am.node.heartbeat", new TimeType("5m"))
 ("wds.linkis.manager.am.engine.kill.timeout", new TimeType("2m"))
 ("wds.linkis.manager.am.em.kill.timeout", new TimeType("2m"))
 ("wds.linkis.manager.monitor.async.poll.size", 5)
 ```


linkis-computation-governance/linkis-manager/linkis-resource-manager:
```shell
 ("wds.linkis.manager.rm.kill.engine.wait", new TimeType("30s"))
```


linkis-engineconn-plugins/engineconn-plugins/io_file:
```shell
 ("wds.linkis.engine.io.opts", " -Dfile.encoding=UTF-8 ")
 ("wds.linkis.storage.io.fs.num", 5)
 ("wds.linkis.storage.io.fs.clear.time", 1000L)
 ("wds.linkis.storage.io.fs.id.limit", Long.MaxValue/3*2)
 ("wds.linkis.engineconn.io.output.limit", Int.MaxValue)
 ("wds.linkis.engineconn.io.version", "*")
 ("wds.linkis.engineconn.io_file.concurrent.limit", 100)
 ```


linkis-engineconn-plugins/engineconn-plugins/jdbc:
```shell
 ("wds.linkis.resultSet.cache.max", new ByteType("0k"))
 ("wds.linkis.jdbc.default.limit", 5000)
 ("wds.linkis.jdbc.query.timeout", 1800)
 ("wds.linkis.jdbc.support.dbs", "mysql=>com.mysql.jdbc.Driver,postgresql=>org.postgresql.Driver,oracle=>oracle.jdbc.driver.OracleDriver,hive2=>org.apache.hive.jdbc.HiveDriver,presto=>com.facebook.presto.jdbc.PrestoDriver")
 [Int]("wds.linkis.engineconn.jdbc.concurrent.limit", 100)
 ```


linkis-engineconn-plugins/engineconn-plugins/pipeline:
```shell
 ("wds.linkis.engine.pipeline.output.isoverwtite", true)
 ("wds.linkis.engine.pipeline.output.charset", "UTF-8")
 ("wds.linkis.engine.pipeline.field.split", " ")
```


linkis-engineconn-plugins/engineconn-plugins/python:
```shell
 ("wds.linkis.python.line.limit", 10)
 ("wds.linkis.python.py4j.home", this.getClass.getResource("/conf").getPath)
 ("pythonVersion", "/appcom/Install/anaconda3/bin/python")
 ("python.path", "", "Specify Python's extra path, which only accepts shared storage paths（指定Python额外的path，该路径只接受共享存储的路径）.")
 ```


linkis-engineconn-plugins/engineconn-plugins/spark:
```shell
 ("query.session.log.hold", 500).getValue
 ("wds.linkis.spark.engine.hooks.enable",true).getValue
 ("wds.linkis.process.threadpool.max", 100)
 ("wds.linkis.engine.spark.session.hook", "")
 ("wds.linkis.engine.spark.spark-loop.init.time", new TimeType("120s"))
 ("wds.linkis.engine.spark.language-repl.init.time", new TimeType("30s"))
 ("spark.repl.classdir", "", "默认master")
 ("spark.proxy.user", "${UM}")
 ("spark.submit.deployMode", "client")
 ("spark.jars", "", "Additional jar package, Driver and Executor take effect（额外的jar包，Driver和Executor生效）")
 ("wds.linkis.spark.sparksubmit.path", "spark-submit")
 ("mapred.output.compress", "true", "Whether the map output is compressed（map输出结果是否压缩）")
 ("mapred.output.compression.codec", "org.apache.hadoop.io.compress.GzipCodec", "Map output compression method（map输出结果压缩方式）")
 ("spark.master", "yarn", "Default master（默认master）")
 ("wds.linkis.spark.output.line.limit", 10)
 ("wds.linkis.spark.useHiveContext", true)
 ("wds.linkis.enginemanager.core.jar", getMainJarName)
 ("wds.linkis.ecp.spark.default.jar", "linkis-engineconn-launch-dev-1.0.0.jar")
 ("wds.linkis.spark.driver.extra.class.path", "")
 ("spark.driver.extraJavaOptions", "\"-Dwds.linkis.configuration=linkis-engine.properties " + "\"")
 ("spark.external.default.jars", "")
 ("spark.config.dir",  ("SPARK_CONF_DIR", "/appcom/config/spark-config").getValue)
 ("spark.home",  ("SPARK_HOME", "/appcom/Install/spark").getValue)
 ("wds.linkis.dws.ujes.spark.extension.timeout", 3000L)
 ("wds.linkis.engine.spark.fraction.length", 30)
 ("wds.linkis.show.df.max.res", Int.MaxValue)
 ("wds.linkis.mdq.application.name", "linkis-ps-metadata")
 ("wds.linkis.dolphin.limit.len", 5000)
 ("spark.driver.memory", 2) #单位为G
 LINKIS_SPARK_DRIVER_CORES = 1 //Fixed to 1（固定为1） ("wds.linkis.driver.cores", 1)
 ("spark.executor.memory", 4) #单位为G
 ("spark.executor.cores", 2)
 ("spark.executor.instances", 3)
 ("wds.linkis.rm.yarnqueue", "default")
 ("PYSPARK_DRIVER_PYTHON", sparkPythonVersion)
 ("python.script.path", "python/mix_pyspark.py")
 ("java.class.path", "")
 ("wds.linkis.dws.ujes.spark.extension.max.pool",5)
 ("spark.yarn.dist.files", ""))
 ("wedatasphere.linkis.bgservice.store.prefix", "hdfs:///tmp/bdp-ide/")
 ("wedatasphere.linkis.bgservice.store.suffix", "")
 ("PYSPARK_DRIVER_PYTHON", "python")
 ("wds.linkis.server.spark-submit", "spark-submit")
 ```


linkis-engineconn-plugins/linkis-engineconn-plugin-framework/linkis-engineconn-plugin-cache:
```shell
 ("linkis.engineConn.plugin.cache.size", 1000)
 ("linkis.engineConn.plugin.cache.expire-in-seconds", 30 * 60 * 60 * 1000L)
 ("linkis.engineConn.plugin.cache.refresh.workers", 5)
 ```


linkis-engineconn-plugins/linkis-engineconn-plugin-framework/linkis-engineconn-plugin-core:
```shell
 ("wds.linkis.engineconn.java.driver.memory", new ByteType("1g"))
 ("wds.linkis.engineconn.java.driver.cores", 2)
 ("wds.linkis.engineconn.java.driver.instannce", 1)
 ("wds.linkis.engineconn.type.name", "python")
 ("hive.config.dir",  ("HIVE_CONF_DIR", "/appcom/config/hive-config").getValue)
 ("linkis.hadoop.lib.native", "/appcom/Install/hadoop/lib/native")
 ("hadoop.config.dir",  ("HADOOP_CONF_DIR", "/appcom/config/hadoop-config").getValue)
 ("wds.linkis.engineConn.jars", "", "engineConn额外的Jars")
 ("wds.linkis.engineConn.files", "", "engineConn额外的配置文件")
 ("wds.linkis.engineConn.javaOpts.default", s"-XX:+UseG1GC -XX:MaxPermSize=250m -XX:PermSize=128m " +
 ("wds.linkis.engineConn.memory", new ByteType("2g"), "Specify the memory size of the java client(指定java进程的内存大小)")
 ("wds.linkis.engineConn.java.extraOpts", "",
 ("wds.linkis.engineConn.extra.classpath", "", "Specify the full path of the java classpath")
 ("wds.linkis.engineconn.retries.max", 3)
 ("wds.linkis.engineconn.debug.enable", false)
 ("wds.linkis.engineconn.log4j2.xml.file", "log4j2-engineconn.xml")
 ("wds.linkis.public_module.path", Configuration.LINKIS_HOME.getValue + "/lib/linkis-commons/public-module")
 ```


linkis-engineconn-plugins/linkis-engineconn-plugin-framework/linkis-engineconn-plugin-loader:
```shell
 ("wds.linkis.engineconn.plugin.loader.classname", "")
 ("wds.linkis.engineconn.plugin.loader.defaultUser", "hadoop")
 ("wds.linkis.engineconn.plugin.loader.store.path", "")
 ("wds.linkis.engineconn.plugin.loader.properties.name", "plugins.properties")
 ("wds.linkis.engineconn.plugin.loader.cache.refresh-interval", "300")
 ("wds.linkis.engineconn.plugin.loader.download.tmpdir.prefix", ".BML_TMP_")
 ```


inkis-engineconn-plugins/linkis-engineconn-plugin-framework/linkis-engineconn-plugin-server:
```shell
 ("wds.linkis.engineconn.home", ("ENGINE_CONN_HOME", "").getValue)
 ("wds.linkis.engineconn.dist.load.enable", true)
 ```

linkis-orchestrator/plugin/linkis-orchestrator-ecm-plugin：
```shell
 ("wds.linkis.orchestrator.ecm.engine.parallelism", 1)
 ("wds.linkis.orchestrator.ecm.mark.apply.attempts", 2)
 ("wds.linkis.orchestrator.ecm.mark.apply.time", new TimeType("5m"))
```

linkis-public-enhancements/linkis-bml/linkis-bml-client：
```shell
 ("wds.linkis.bml.dws.version", "v1")
 ("wds.linkis.bml.url.prefix", "/api/rest_j/v1/bml", "bml服务的url前缀")
 ("wds.linkis.bml.upload.url","upload")
 ("wds.linkis.bml.updateVersion.url", "updateVersion","更新版本的url")
 ("wds.linkis.bml.updateBasic.url", "updateBasic","更新基本信息的url")
 ("wds.linkis.bml.relateHdfs.url", "relateHdfs", "关联hdfs资源的url")
 ("wds.linkis.bml.relateStorage.url", "relateStorage", "关联共享存储的url")
 ("wds.linkis.bml.getResourceMsg.url","getResourceMsg", "获取资源的信息")
 ("wds.linkis.bml.download.url", "download")
 ("wds.linkis.bml.delete.url", "delete")
 ("wds.linkis.bml.getVersions.url", "getVersions")
 ("wds.linkis.bml.getBasic.url","getBasic")
 ("wds.linkis.bml.auth.token.key", "Validation-Code")
 ("wds.linkis.bml.auth.token.value", "BML-AUTH")
 ```

linkis-public-enhancements/linkis-bml/linkis-bml-engine-hook：
```shell
 ("wds.linkis.bml.work.dir", "user.dir")
```


linkis-public-enhancements/linkis-bml/linkis-bml-server：
```shell
 ("wds.linkis.bml.hdfs.prefix", "/tmp/linkis")
 ("wds.linkis.bml.cleanExpired.time", 100)
 ("wds.linkis.bml.clean.time.type", TimeUnit.HOURS)
 ("wds.linkis.server.maxThreadSize", 30)
 ```



linkis-public-enhancements/linkis-context-service/linkis-cs-cache：
```shell
("wds.linkis.cs.keyword.scan.package","com.webank.wedatasphere.linkis.cs")
("wds.linkis.cs.keyword.split",",")
```



linkis-public-enhancements/linkis-context-service：
```shell
("wds.linkis.web.version", "v1")
("wds.linkis.context.client.auth.key", "Token-Code")
("wds.linkis.context.client.auth.value", "BML-AUTH")
("wds.linkis.cs.url.prefix", "/api/rest_j/v1/contextservice", "cs服务的url前缀")
("wds.linkis.cs.createcontext.url", "createContextID")
("wds.linkis.cs.setvaluebykey.url", "setValueByKey")
("wds.linkis.cs.setkeyvalue.url", "setValue")
("wds.linkis.cs.resetkeyvalue.url", "resetValue")
("wds.linkis.cs.removeValue.url", "removeValue")
("wds.linkis.cs.reset.contextid.url", "removeAllValue")
("wds.linkis.cs.heartbeat.enabled", "true")
```



linkis-public-enhancements/linkis-context-service/linkis-cs-common：
```shell
("wds.linkis.dev.contextID.env", "BDP_DEV")
("wds.linkis.production.contextID.env", "BDP_PRODUCTION")
```


linkis-public-enhancements/linkis-context-service/linkis-cs-highavailable：
```shell
("wds.linkis.cs.haid.strict_check.enable", false)
```

linkis-public-enhancements/linkis-context-service/linkis-cs-listener：
 ```shell
 ("wds.linkis.cs.listener.asyn.consumer.thread.max","5")
 ("wds.linkis.cs.listener.asyn.consumer.freeTime.max","5000")
 ("wds.linkis.cs.listener.asyn.queue.size.max","300")
 ```

linkis-public-enhancements/linkis-context-service/linkis-cs-persistence：
 ```shell
 ("wds.linkis.cs.ha.class", "com.webank.wedatasphere.linkis.cs.highavailable.DefaultContextHAManager")
 ("wds.linkis.cs.ha.proxymethod", "getContextHAProxy")
 ````


linkis-public-enhancements/linkis-context-service/linkis-cs-server：
```shell
 ("wds.linkis.cs.keyword.scan.package","com.webank.wedatasphere.linkis.cs")
```

linkis-public-enhancements/linkis-datasource/datasourcemanager/common：
```shell
 ("wds.linkis.server.dsm.admin.users", "")
 ("wds.linkis.server.dsm.error-code.transform", 99987)
 ("wds.linkis.server.dsm.error-code.bml", 99982)
 ("wds.linkis.server.dsm.error-code.metadata", 99983)
 ("wds.linkis.server.dsm.error-code.param-validate", 99986)
```

linkis-public-enhancements/linkis-datasource/linkis-metadata：
```shell
 ("hadoop.config.dir",  ("HADOOP_CONF_DIR", "/appcom/config/hadoop-config").getValue())
 ("hive.config.dir",   ("HIVE_CONF_DIR", "/appcom/config/hadoop-config").getValue())
 ("hive.meta.url", "")
 ("hive.meta.user", "")
 ("hive.meta.password", "")
 ("wds.linkis.server.mybatis.mapperLocations", "")
 ("wds.linkis.server.mybatis.typeAliasesPackage", "")
 ("wds.linkis.server.mybatis.configLocation", "classpath:/mybatis-config.xml")
 ("wds.linkis.server.mybatis.BasePackage", "")
 ("wds.linkis.server.mybatis.datasource.url", "")
 ("wds.linkis.server.mybatis.datasource.username", "")
 ("wds.linkis.server.mybatis.datasource.password", "")
 ("wds.linkis.server.mybatis.datasource.driver-class-name", "com.mysql.jdbc.Driver")
 ("wds.linkis.server.mybatis.datasource.initialSize", new Integer(1))
 ("wds.linkis.server.mybatis.datasource.minIdle", new Integer(1))
 ("wds.linkis.server.mybatis.datasource.maxActive", new Integer(20))
 ("wds.linkis.server.mybatis.datasource.maxWait", new Integer(6000))
 ("wds.linkis.server.mybatis.datasource.timeBetweenEvictionRunsMillis", new Integer(60000))
 ("wds.linkis.server.mybatis.datasource.minEvictableIdleTimeMillis", new Integer(300000));
 ("wds.linkis.server.mybatis.datasource.validationQuery", "SELECT 1")
 ("wds.linkis.server.mybatis.datasource.testWhileIdle", new Boolean(true))
 ("wds.linkis.server.mybatis.datasource.testOnBorrow", new Boolean(false))
 ("wds.linkis.server.mybatis.datasource.testOnReturn", new Boolean(false))
 ("wds.linkis.server.mybatis.datasource.poolPreparedStatements", new Boolean(true))
 ("wds.linkis.metadata.hive.encode.enabled", new Boolean(false))
 ("bdp.dataworkcloud.datasource.store.type", "orc")
 ("bdp.dataworkcloud.datasource.default.par.name", "ds")
 ("bdp.dataworkcloud.datasource.default.par.name", "ds")
 ```


linkis-public-enhancements/linkis-datasource/metadatamanager/common：
```shell
 ("wds.linkis.server.mdm.service.cache.size", 1000L)
 ("wds.linkis.server.mdm.service.cache.expire", 600L)
 ("wds.linkis.server.mdm.service.app.name", "linkis-ps-metadatamanagerservice")
 ("wds.linkis.server.dsm.app.name", "linkis-ps-datasourcemanager")
```


linkis-public-enhancements/linkis-datasource/metadatamanager/service/elasticsearch：
```shell
 ("wds.linkis.server.mdm.service.es.urls", "elasticUrls")
 ("wds.linkis.server.mdm.service.es.username", "username")
 ("wds.linkis.server.mdm.service.es.password", "password")
```


linkis-public-enhancements/linkis-datasource/metadatamanager/service/hive：
```shell
 ("wds.linkis.server.mdm.service.kerberos.principle", "hadoop/_HOST@EXAMPLE.COM")
 ("wds.linkis.server.mdm.service.user", "hadoop")
 ("wds.linkis.server.mdm.service.kerberos.krb5.path", "")
 ("wds.linkis.server.mdm.service.temp.location", "classpath:/tmp")
 ("wds.linkis.server.mdm.service.hive.principle", "principle")
 ("wds.linkis.server.mdm.service.hive.uris", "uris")
 ("wds.linkis.server.mdm.service.hive.keytab", "keytab")
```


linkis-public-enhancements/linkis-datasource/metadatamanager/service/mysql：
```shell
 ("wds.linkis.server.mdm.service.sql.driver", "com.mysql.jdbc.Driver")
 ("wds.linkis.server.mdm.service.sql.url", "jdbc:mysql://%s:%s/%s")
 ("wds.linkis.server.mdm.service.sql.host", "host")
 ("wds.linkis.server.mdm.service.sql.port", "port")
 ("wds.linkis.server.mdm.service.sql.username", "username")
 ("wds.linkis.server.mdm.service.sql.password", "password")
 ("wds.linkis.server.mdm.service.sql.params", "params")
 ```


linkis-public-enhancements/linkis-publicservice/linkis-configuration：
```shell
 ("wds.linkis.configuration.copykey.token","e8724-e")
```

linkis-public-enhancements/linkis-publicservice/linkis-instance-label/client：
```shell
("wds.linkis.instance.label.server.name", "linkis-ps-publicservice")
```


linkis-public-enhancements/linkis-publicservice/linkis-instance-label：
```shell
 ("wds.linkis.instance.label.persist.batch.size", 100)
 ("wds.linkis.instance.label.async.queue.capacity", 1000)
 ("wds.linkis.instance.label.async.queue.batch.size", 100)
 ("wds.linkis.instance.label.async.queue.interval-in-seconds", 10L)
 ("wds.linkis.instance.label.cache.expire.time-in-seconds", 10)
 ("wds.linkis.instance.label.cache.maximum.size", 1000)
 ("wds.linkis.instance.label.cache.names", "instance,label")
 ```


linkis-public-enhancements/linkis-publicservice/linkis-jobhistory：
```shell
 ("wds.linkis.jobhistory.admin", "hadoop,tom,jerry")
 ("wds.linkis.jobhistory.safe.trigger", true)
 ("wds.linkis.query.cache.max.expire.hour", 1L)
 ("wds.linkis.query.cache.daily.expire.enabled", true)
 ("wds.linkis.query.cache.max.size", 10000L)
 ("wds.linkis.query.cache.cleaning.interval.minute", 30)
 ("bdp.dataworkcloud.query.store.prefix", "hdfs:///tmp/bdp-ide/")
 ("bdp.dataworkcloud.query.store.suffix", "")
 ```



linkis-public-enhancements/linkis-publicservice/linkis-script-dev/linkis-storage-script-dev-client:
 ```shell
 ("wds.linkis.gateway.address", "")
 ("wds.linkis.filesystem.prefixutl", "/api/rest_j/v1/filesystem")
 ("wds.linkis.filesystem.scriptFromBML", "/openScriptFromBML")
 ("wds.linkis.bml.dws.version", "v1")
 ("wds.linkis.filesystem.token.key", "Validation-Code")
 ("wds.linkis.filesystem.token.value", "WS-AUTH")
```

linkis-public-enhancements/linkis-publicservice/linkis-script-dev/linkis-storage-script-dev-server:
 ```shell
 ("wds.linkis.filesystem.root.path", "file:///tmp/linkis/")
 ("wds.linkis.filesystem.hdfs.root.path", "hdfs:///tmp/")
 ("wds.linkis.workspace.filesystem.hdfsuserrootpath.suffix", "/linkis/")
 ("wds.linkis.workspace.resultset.download.is.limit", true)
 ("wds.linkis.workspace.resultset.download.maxsize.csv", 5000)
 ("wds.linkis.workspace.resultset.download.maxsize.excel", 5000)
 ("wds.linkis.workspace.filesystem.get.timeout", 2000L)
 ("wds.linkis.workspace.filesystem.thread.num", 10)
 ("wds.linkis.workspace.filesystem.thread.cache", 1000)
 ("wds.linkis.workspace.filesystem.path.check", false)
 ("wds.linkis.workspace.filesystem.admin", "hadoop,tom,jerry")
 ```


linkis-public-enhancements/linkis-publicservice/linkis-udf：
```shell
 ("wds.linkis.udf.hive.exec.path", "/appcom/Install/DataWorkCloudInstall/linkis-linkis-Udf-0.0.3-SNAPSHOT/lib/hive-exec-1.2.1.jar")
 ("wds.linkis.udf.tmp.path", "/tmp/udf/")
 ```


linkis-spring-cloud-services/linkis-service-gateway/linkis-gateway-core：
```shell
 ("wds.linkis.gateway.conf.enable.proxy.user", false)
 ("wds.linkis.gateway.conf.proxy.user.config", "proxy.properties")
 ("wds.linkis.gateway.conf.proxy.user.scan.interval", 1000 * 60 * 10)
 ("wds.linkis.gateway.conf.enable.token.auth", false)
 ("wds.linkis.gateway.conf.token.auth.config", "token.properties")
 ("wds.linkis.gateway.conf.token.auth.scan.interval", 1000 * 60 * 10)
 ("wds.linkis.gateway.conf.url.pass.auth", "/dws/").getValue.split(",")
 ("wds.linkis.gateway.conf.enable.sso", false)
 ("wds.linkis.gateway.conf.sso.interceptor", "")
 ("wds.linkis.admin.user", "hadoop")
 ("wds.linkis.gateway.usercontrol_switch_on", false)
 ("wds.linkis.gateway.conf.proxy.user.list", "").getValue.split(",")
 ("wds.linkis.usercontrol.application.name", "cloud-usercontrol")
 ("wds.linkis.login_encrypt.enable", false)
 ("wds.linkis.entrance.name", "linkis-cg-entrance")
 ("wds.linkis.enable.gateway.auth", false)
 ("wds.linkis.gateway.auth.file", "auth.txt")
 ```

linkis-spring-cloud-services/linkis-service-gateway/linkis-spring-cloud-gateway：
```shell
 ("wds.linkis.gateway.max.buffer.size", 128 * 1024 * 1024)
 ("wds.linkis.gateway.conf.max.frame.length", 655350)
 ("wds.linkis.gateway.websocket.heartbeat", new TimeType("5s"))
```

linkis-commons/linkis-storage：
```shell
 ("wds.linkis.storage.proxy.user", "${UM}")
 ("wds.linkis.storage.root.user", "hadoop")
 ("wds.linkis.storage.hdfs.root.user", "hadoop")
 ("wds.linkis.storage.local.root.user", "root")
 ("wds.linkis.storage.fileSystem.group", "bdap")
 ("wds.linkis.storage.rs.file.type", "utf-8")
 ("wds.linkis.storage.rs.file.suffix", ".dolphin")
 ("wds.linkis.storage.result.set.package", "com.webank.wedatasphere.linkis.storage.resultset")
 ("wds.linkis.storage.result.set.classes", "txt.TextResultSet,table.TableResultSet,io.IOResultSet,html.HtmlResultSet,picture.PictureResultSet")
 ("wds.linkis.storage.build.fs.classes", "com.webank.wedatasphere.linkis.storage.factory.impl.BuildHDFSFileSystem,com.webank.wedatasphere.linkis.storage.factory.impl.BuildLocalFileSystem")
 ("wds.linkis.storage.is.share.node", true)
 ("wds.linkis.storage.io.user", "root")
 ("wds.linkis.storage.io.fs.num", 1000*60*10)
 ("wds.linkis.storage.io.read.fetch.size", new ByteType("100k"))
 ("wds.linkis.storage.io.write.cache.size", new ByteType("64k"))
 ("wds.linkis.storage.io.default.creator", "ujes")
 ("wds.linkis.storage.io.fs.re.init", "re-init")
 ("wds.linkis.storage.io.init.retry.limit", 10)
 ("wds.linkis.storage.fileSystem.hdfs.group", "hadoop")
 ("wds.linkis.double.fraction.length", 30)
 ("wds.linkis.storage.hdfs.prefix_check.enable", true)
 ("wds.linkis.storage.hdfs.prefxi.remove", true)
 ```
