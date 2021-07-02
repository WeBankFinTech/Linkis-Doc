## 1. 简述

&nbsp;&nbsp;&nbsp;&nbsp;  首先，Linkis1.0 架构下的 Entrance 和 EngineConnManager（原EngineManager）服务与 **引擎** 已完全无关，即：
                             在 Linkis1.0 架构下，每个引擎无需再配套实现并启动对应的 Entrance 和 EngineConnManager，Linkis1.0 的每个 Entrance 和 EngineConnManager 都可以给所有引擎共用。
                          
&nbsp;&nbsp;&nbsp;&nbsp;  其次，Linkis1.0 新增了Linkis-Manager服务用于对外提供 AppManager（应用管理）、ResourceManager（资源管理，原ResourceManager服务）和 LabelManager（标签管理）的能力。

&nbsp;&nbsp;&nbsp;&nbsp;  然后，为了降低大家实现和部署一个新引擎的难度，Linkis 1.0 重新架构了一个叫 EngineConnPlugin 的模块，每个新引擎只需要实现 EngineConnPlugin 接口即可，
Linkis EngineConnPluginServer 支持以插件的形式动态加载 EngineConnPlugin（新引擎），一旦 EngineConnPluginServer 加载成功，EngineConnManager 便可为用户快速启动一个该引擎实例。
                          
&nbsp;&nbsp;&nbsp;&nbsp;  最后，对Linkis的所有微服务进行了归纳分类，总体分为了三个大层次：公共增强服务、计算治理服务和微服务治理服务，从代码层级结构、微服务命名和安装目录结构等多个方面来规范Linkis1.0的微服务体系。


##  2. 主要特点

1.  **强化计算治理**，Linkis1.0主要从引擎管理、标签管理、ECM管理和资源管理等几个方面，全面强化了计算治理的综合管控能力，基于标签化的强大管控设计理念，使得Linkis1.0向多IDC化、多集群化、多容器化，迈出了坚实的一大步。

2.  **简化用户实现新引擎**，EnginePlugin用于将原本实现一个新引擎，需要实现的相关接口和类，以及需要拆分的Entrance-EngineManager-Engine三层模块体系，融合到了一个接口之中，简化用户实现新引擎的流程和代码，真正做到只要实现一个类，就能接入一个新引擎。

3.  **全栈计算存储引擎支持**，实现对计算请求场景（如Spark）、存储请求场景（如HBase）和常驻集群型服务（如SparkStreaming）的全面覆盖支持。

4.  **高级计算策略能力改进**，新增Orchestrator实现丰富计算任务管理策略，且支持基于标签的解析和编排。

5.  **安装部署改进**  优化一键安装脚本，支持容器化部署，简化用户配置。

## 3. 服务对比

&nbsp;&nbsp;&nbsp;&nbsp;  请参考以下两张图：

&nbsp;&nbsp;&nbsp;&nbsp;  Linkis0.X 微服务列表如下：

![Linkis0.X服务列表](https://github.com/WeBankFinTech/Linkis/blob/dev-1.0.0/images/zh_CN/Linkis1.0/installation/Linkis0.X-services-list.png)
<!--图片不存在-->
&nbsp;&nbsp;&nbsp;&nbsp;  Linkis1.0 微服务列表如下：

![Linkis1.0服务列表](https://github.com/WeBankFinTech/Linkis/blob/dev-1.0.0/images/zh_CN/Linkis1.0/installation/Linkis1.0-services-list.png)
<!--图片不存在-->
&nbsp;&nbsp;&nbsp;&nbsp;  从上面两个图中看，Linkis1.0 将服务分为了三类服务：计算治理（英文缩写CG）/微服务治理（MG）/公共增强服务(PS)。其中：

1. 计算治理的一大变化是，Entrance 和 EngineConnManager服务与引擎再不相关，实现一个新引擎只需实现 EngineConnPlugin插件即可，EngineConnPluginServer会动态加载 EngineConnPlugin 插件，做到引擎热插拔式更新；

2. 计算治理的另一大变化是，LinkisManager作为 Linkis 的管理大脑，抽象和定义了 AppManager（应用管理）、ResourceManager（资源管理）和LabelManager（标签管理）；

3. 微服务治理服务，将0.X部分的Eureka和Gateway服务进行了归并统一，并对Gateway服务进行了功能增强，支持按照Label进行路由转发；

4. 公共增强服务，主要将0.X部分的BML服务/上下文服务/数据源服务/公共服务进行了优化和归并统一，便于大家管理和查看。

## 4. Linkis Manager简介

&nbsp;&nbsp;&nbsp;&nbsp;  Linkis Manager 作为 Linkis 的管理大脑，主要由 AppManager、ResourceManager 和 LabelManager 组成。

&nbsp;&nbsp;&nbsp;&nbsp;  ResourceManager 不仅具备 Linkis0.X 对 Yarn 和 Linkis EngineManager 的资源管理能力，还将提供基于标签的多级资源分配和回收能力，让 ResourceManager 具备跨集群、跨计算资源类型的全资源管理能力；

&nbsp;&nbsp;&nbsp;&nbsp;  AppManager 将统筹管理所有的 EngineConnManager 和 EngineConn，EngineConn 的申请、复用、创建、切换、销毁等生命周期全交予 AppManager进行管理；

&nbsp;&nbsp;&nbsp;&nbsp;  而 LabelManager 将基于多级组合标签，提供跨IDC、跨集群的 EngineConn 和 EngineConnManager 路由和管控能力；

## 5. Linkis EngineConnPlugin简介

&nbsp;&nbsp;&nbsp;&nbsp;  EngineConnPlugin 主要用于降低新计算存储的接入和部署成本，真正做到让用户“只需实现一个类，就能接入一个全新计算存储引擎；只需执行一下脚本，即可快速部署一个全新引擎”。

### 5.1 新引擎实现对比

&nbsp;&nbsp;&nbsp;&nbsp;  以下是用户Linkis0.X实现一个新引擎需要实现的相关接口和类：

![Linkis0.X 如何实现一个全新引擎](https://github.com/WeBankFinTech/Linkis/blob/dev-1.0.0/images/zh_CN/Linkis1.0/architecture/Linkis0.X-NewEngine-architecture.png)
<!--链接不存在-->p;&nbsp;&nbsp;  以下为Linkis1.0.0，实现一个新引擎，用户需实现的接口和类：

![Linkis1.0 如何实现一个全新引擎](https://github.com/WeBankFinTech/Linkis/blob/dev-1.0.0/images/zh_CN/Linkis1.0/architecture/Linkis1.0-NewEngine-architecture.png)
<!--链接不存在-->
&nbsp;&nbsp;&nbsp;&nbsp;  其中EngineConnResourceFactory和EngineLaunchBuilder为非必需实现接口，只有EngineConnFactory为必需实现接口。

### 5.2 新引擎启动流程

&nbsp;&nbsp;&nbsp;&nbsp;  EngineConnPlugin 提供了 Server 服务，用于启动和加载所有的引擎插件，以下给出了一个新引擎启动，访问了 EngineConnPlugin-Server 的全部流程：

![Linkis 引擎启动流程](https://github.com/WeBankFinTech/Linkis/blob/dev-1.0.0/images/zh_CN/Linkis1.0/architecture/Linkis1.0-newEngine-initialization.png)
<!--链接不存在-->
## 6. Linkis EngineConn简介

&nbsp;&nbsp;&nbsp;&nbsp;  EngineConn，即原 Engine 模块，作为 Linkis 与底层计算存储引擎进行连接和交互的实际单元，是 Linkis 提供计算存储能力的基础。

&nbsp;&nbsp;&nbsp;&nbsp;  Linkis1.0 的 EngineConn 主要由 EngineConn 和 Executor构成。其中：

a)	EngineConn 为连接器，包含引擎与具体集群的会话信息。它只是起到一个连接，一个客户端的作用，并不真正的去执行计算。

b)	Executor 为执行器，作为真正的计算场景执行器，是实际的计算逻辑执行单元，也对引擎各种具体能力的抽象，例如提供加锁、访问状态、获取日志等多种不同的服务。

c)	Executor 通过 EngineConn 中的会话信息进行创建，一个引擎类型可以支持多种不同种类的计算任务，每种对应一个 Executor 的实现，计算任务将被提交到对应的 Executor 进行执行。
这样，同一个引擎能够根据不同的计算场景提供不同的服务。比如常驻式引擎启动后不需要加锁，一次性引擎启动后不需要支持 Receiver 和访问状态等。

d)	采用 Executor 和 EngineConn 分离的方式的好处是，可以避免 Receiver 耦合业务逻辑，本身只保留 RPC 通信功能。将服务分散在多个 Executor 模块中，并且抽象成几大类引擎：交互式计算引擎、流式引擎、一次性引擎等等可能用到的，构建成统一的引擎框架，便于后期的扩充。
这样不同类型引擎可以根据需要分别加载其中需要的能力，大大减少引擎实现的冗余。

&nbsp;&nbsp;&nbsp;&nbsp;  如下图所示：
<!--图片不存在-->
![Linkis EngineConn架构图](https://github.com/WeBankFinTech/Linkis/blob/dev-1.0.0/images/zh_CN/Linkis1.0/architecture/Linkis1.0-EngineConn-architecture.png)