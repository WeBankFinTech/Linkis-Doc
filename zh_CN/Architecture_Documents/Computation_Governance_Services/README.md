## 1. 文档结构
Linkis 1.0 将所有微服务总体划分为三大类：公共增强服务、计算治理服务、微服务治理服务。

各大类的具体职责如下：

1. 公共增强服务为 Linkis 0.X 已经提供的物料库服务、上下文服务、数据源服务和公共服务等；
    
2. 微服务治理服务为 Linkis 0.X 已经提供的 Spring Cloud Gateway、Eureka 和 Open Feign，同时 Linkis1.0 还会提供对 Nacos 的支持；
    
3. 计算治理服务是 Linkis 1.0 的核心重点，从 提交 —> 准备 —> 执行三个阶段，来全面升级 Linkis 对 用户任务的执行管控能力。

以下是 Linkis1.0 架构文档的目录列表：

1. Linkis1.0在架构上的特点，请阅读[Linkis1.0与Linkis0.x的区别](Linkis1.0与Linkis0.X的区别简述.md)。

2. Linkis1.0公共增强服务相关文档，请阅读[公共增强服务](Public_Enhancement_Services\README.md)。

3. Linkis1.0微服务治理相关文档，请阅读[微服务治理](Microservice_Governance_Services\README.md)。

4. Linkis1.0提出的计算治理服务相关文档，请阅读 [计算治理服务](Computation_Governance_Services\README.md)。


