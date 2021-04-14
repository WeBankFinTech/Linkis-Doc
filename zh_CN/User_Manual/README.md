## 1. 概述
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Linkis项目是微众银行大数据平台自研的一项大数据作业提交方案及可扩展框架。Linkis可以对接多种计算引擎，并向外提供统一的接口来实现作业提交与执行，降低运维和学习成本。  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Linkis作为一款计算中间件，用户可以搭配DataSphereStudio（微众银行另一项开源项目）直接使用，也可以根据的前端接口定制化开发并接入。Linkis作为一个可扩展性强的框架，也提供了客户端的实现，用户可以通过使用Linkis的SDK进行接入，定制化开发并接入其它应用。同时，Linkis1.0在0.x版本的的基础上，在配置管理的功能上进行了优化和增强，通过剥离DataSphereStudio控制台功能，接入1.0版本，使得配置管理Linkis变得更加简单。
## 2. 文档说明
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Linkis在设计之初就考虑接入方式的拓展性问题，针对不同的接入场景，Linkis提供了前端接入和SDK接入的方式，在前端接口上又提供了HTTP和WebSocket两种方式，如果对接入并使用Linkis感兴趣，可以参考以下文档：  
[如何使用Links](How_To_Use_Linkis.md)
[Linkis管理台使用手册](Linkis_Console_User_Manual.md)
[Linkis1.0用户使用文档](Linkis1.0用户使用文档.md)