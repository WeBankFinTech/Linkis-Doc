## 1. Brief Description
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;First of all, the Entrance and EngineConnManager (formerly EngineManager) services under the Linkis1.0 architecture are completely unrelated to the engine. That is, under the Linkis1.0 architecture, each engine does not need to be implemented and started the corresponding Entrance and EngineConnManager, and Linkis1.0’s Each Entrance and EngineConnManager can be shared by all engines.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Secondly, Linkis1.0 added the Linkis-Manager service to provide external AppManager (application management), ResourceManager (resource management, the original ResourceManager service) and LabelManager (label management) capabilities.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Then, in order to reduce the difficulty of implementing and deploying a new engine, Linkis 1.0 re-architects a module called EngineConnPlugin. Each new engine only needs to implement the EngineConnPlugin interface.Linkis EngineConnPluginServer supports dynamic loading of EngineConnPlugin (new engine) in the form of a plug-in. Once EngineConnPluginServer is successfully loaded, EngineConnManager can quickly start an instance of the engine for the user.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Finally, all the microservices of Linkis are summarized and classified, which are generally divided into three major levels: public enhancement services, computing governance services and microservice governance services, from the code hierarchy, microservice naming and installation directory structure, etc. To standardize the microservice system of Linkis1.0.  
##  2. Main Feature
1. **Strengthen computing governance**, Linkis 1.0 mainly strengthens the comprehensive management and control capabilities of computing governance from engine management, label management, ECM management, and resource management. It is based on the powerful management and control design concept of labeling. This makes Linkis 1.0 a solid step towards multi-IDC, multi-cluster, and multi-container.  
2. **Simplify user implementation of new engines**, EnginePlugin is used to integrate the related interfaces and classes that need to be implemented to implement a new engine, as well as the Entrance-EngineManager-Engine three-tier module system that needs to be split into one interface. , Simplify the process and code for users to implement the new engine, so that as long as one class is implemented, a new engine can be connected.  
3. **Full-stack computing storage engine support**, to achieve full coverage support for computing request scenarios (such as Spark), storage request scenarios (such as HBase), and resident cluster services (such as SparkStreaming).  
4. **Improved advanced computing strategy capability**, add Orchestrator to implement rich computing task management strategies, and support tag-based analysis and orchestration.  
## 3. Service Comparison
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Please refer to the following two pictures: 
<!--此链接已失效-->
![Linkis0.X Service List](https://github.com/WeBankFinTech/Linkis/blob/dev-1.0.0/images/zh_CN/Linkis1.0/installation/Linkis0.X-services-list.png)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The list of Linkis1.0 microservices is as follows:  
<!--此链接已失效-->
![Linkis1.0 Service List](https://github.com/WeBankFinTech/Linkis/blob/dev-1.0.0/images/zh_CN/Linkis1.0/installation/Linkis1.0-services-list.png)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;From the above two figures, Linkis1.0 divides services into three types of services: Computing Governance (CG)/Micro Service Governance (MG)/Public Enhanced Service (PS). among them:  
1. A major change in computing governance is that Entrance and EngineConnManager services are no longer related to engines. To implement a new engine, only the EngineConnPlugin plug-in needs to be implemented. EngineConnPluginServer will dynamically load the EngineConnPlugin plug-in to achieve engine hot-plug update;
2. Another major change in computing governance is that LinkisManager, as the management brain of Linkis, abstracts and defines AppManager (application management), ResourceManager (resource management) and LabelManager (label management);
3. Microservice management service, merged and unified the Eureka and Gateway services in the 0.X part, and enhanced the functions of the Gateway service to support routing and forwarding according to Label;
4. Public enhancement services, mainly to optimize and unify the BML services/context services/data source services/public services of the 0.X part, which is convenient for everyone to manage and view.  
## 4. Introduction To Linkis Manager
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;As the management brain of Linkis, Linkis Manager is mainly composed of AppManager, ResourceManager and LabelManager.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ResourceManager not only has Linkis0.X's resource management capabilities for Yarn and Linkis EngineManager, but also provides tag-based multi-level resource allocation and recycling capabilities, allowing ResourceManager to have full resource management capabilities across clusters and across computing resource types.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppManager will coordinate and manage all EngineConnManager and EngineConn, and the life cycle of EngineConn application, reuse, creation, switching, and destruction will be handed over to AppManager for management.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The LabelManager will provide cross-IDC and cross-cluster EngineConn and EngineConnManager routing and management capabilities based on multi-level combined tags.  
## 5. Introduction To Linkis EngineConnPlugin
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EngineConnPlugin is mainly used to reduce the cost of access and deployment of new computing storage. It truly enables users to “just need to implement a class to connect to a new computing storage engine; just execute a script to quickly deploy a new engine ".  
### 5.1 New Engine Implementation Comparison
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The following are the relevant interfaces and classes that the user Linkis0.X needs to implement to implement a new engine:  
<!--此链接已失效-->
![Linkis0.X How to implement a brand new engine](https://github.com/WeBankFinTech/Linkis/blob/dev-1.0.0/images/zh_CN/Linkis1.0/architecture/Linkis0.X-NewEngine-architecture.png)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The following is Linkis 1.0.0, which implements a new engine, the interfaces and classes that users need to implement:  
<!--此链接已失效-->
![Linkis1.0 How to implement a brand new engine](https://github.com/WeBankFinTech/Linkis/blob/dev-1.0.0/images/zh_CN/Linkis1.0/architecture/Linkis1.0-NewEngine-architecture.png)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Among them, EngineConnResourceFactory and EngineLaunchBuilder are not required to implement interfaces, and only EngineConnFactory is required to implement interfaces.  
### 5.2 New engine startup process
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EngineConnPlugin provides the Server service to start and load all engine plug-ins. The following is a new engine startup that accesses the entire process of EngineConnPlugin-Server:  
<!--此链接已失效-->
![Linkis Engine start process](https://github.com/WeBankFinTech/Linkis/blob/dev-1.0.0/images/zh_CN/Linkis1.0/architecture/Linkis1.0-newEngine-initialization.png)  
## 6. Introduction To Linkis EngineConn
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EngineConn, the original Engine module, is the actual unit for Linkis to connect and interact with the underlying computing storage engine, and is the basis for Linkis to provide computing and storage capabilities.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EngineConn of Linkis1.0 is mainly composed of EngineConn and Executor. among them:  

1. EngineConn is the connector, which contains the session information between the engine and the specific cluster. It only acts as a connection, a client, and does not actually perform calculations.  

2. Executor is the executor. As a real computing scene executor, it is the actual computing logic execution unit, and it also abstracts various specific capabilities of the engine, such as providing various services such as locking, access status, and log acquisition.

3. Executor is created by the session information in EngineConn. An engine type can support multiple different types of computing tasks, each corresponding to the implementation of an Executor, and the computing task will be submitted to the corresponding Executor for execution.  In this way, the same engine can provide different services according to different computing scenarios. For example, the permanent engine does not need to be locked after it is started, and the one-time engine does not need to support Receiver and access status after it is started.  

4. The advantage of using the separation of Executor and EngineConn is that it can avoid the Receiver coupling business logic, and only retains the RPC communication function. Distribute services in multiple Executor modules, and abstract them into several categories of engines: interactive computing engines, streaming engines, disposable engines, etc., which may be used, and build a unified engine framework for later expansion.
In this way, different types of engines can respectively load the required capabilities according to their needs, which greatly reduces the redundancy of engine implementation.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;As shown below:  
<!--此链接已失效-->   
![Linkis EngineConn Architecture diagram](https://github.com/WeBankFinTech/Linkis/blob/dev-1.0.0/images/zh_CN/Linkis1.0/architecture/Linkis1.0-EngineConn-architecture.png)
