 > This article briefly introduces the precautions for upgrading Linkis from 0.X to 1.0. Linkis 1.0 has adjusted several Linkis services with major changes. This article will introduce the precautions for upgrading from 0.X to 1.X.

## 1.Precautions

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**If you are using Linkis for the first time, you can ignore this chapter; if you are already a user of Linkis, it is recommended to read it before installing or upgrading：[Brief description of the difference between Linkis1.0 and Linkis0.X](https://github.com/WeBankFinTech/Linkis/wiki/Linkis1.0%E4%B8%8ELinkis0.X%E7%9A%84%E5%8C%BA%E5%88%AB%E7%AE%80%E8%BF%B0)**.
<!--链接跳转到了中文文档-->
## 2. Service upgrade installation

&nbsp;&nbsp;&nbsp;&nbsp;  Because linkis 1.0 basically upgraded all services, including service names, all services need to be reinstalled when upgrading from 0.X to 1.X.

&nbsp;&nbsp;&nbsp;&nbsp;  If you need to keep 0.X data during the upgrade, you must select 1 to skip the table building statement (see the code below).

&nbsp;&nbsp;&nbsp;&nbsp;  For the installation of Linkis1.0, please refer to [Quick Deployment Linkis1.0](../Deployment_Documents/Quick_Deployment_Linkis1.0.md)<!--链接失效-->

```
Do you want to clear Linkis table information in the database?
1: Do not execute table-building statements
2: Dangerous! Clear all data and rebuild the tables
other: exit

Please input the choice: ## choice 1
```
## 3. Database upgrade

&nbsp;&nbsp;&nbsp;&nbsp;  After the service is installed, the database structure needs to be modified, including table structure changes and new tables and data:

### 3.1 Table structure modification part:

&nbsp;&nbsp;&nbsp;&nbsp;  linkis_task: The submit_user and label_json fields are added to the table. The update statement is：

```mysql-sql
ALTER TABLE linkis_task ADD submit_user varchar(50) DEFAULT NULL COMMENT 'submitUser name';
ALTER TABLE linkis_task ADD `label_json` varchar(200) DEFAULT NULL COMMENT 'label json';
```

### 3.2 Need newly executed sql：

```mysql-sql
cd db/module
## Add the tables that the enginePlugin service depends on：
source linkis_ecp.sql
## Add a table that the public service-instanceLabel service depends on
source linkis_instance_label.sql
## Added tables that the linkis-manager service depends on
source linkis_manager.sql
```

### 3.3 Publicservice-Configuration table modification

&nbsp;&nbsp;&nbsp;&nbsp;  In order to support the full labeling capability of Linkis 1.X, all the data tables related to the configuration module have been upgraded to labeling, which is completely different from the 0.X Configuration table. It is necessary to re-execute the table creation statement and the initialization statement.

&nbsp;&nbsp;&nbsp;&nbsp;  This means that **Linkis0.X users' existing engine configuration parameters can no longer be migrated to Linkis1.0** (it is recommended that users reconfigure the engine parameters once).

&nbsp;&nbsp;&nbsp;&nbsp;  The execution of the table building statement is as follows:

```mysql-sql
source linkis_configuration.sql
```

&nbsp;&nbsp;&nbsp;&nbsp;  Because Linkis 1.0 supports multiple versions of the engine, it is necessary to modify the version of the engine when executing the initialization statement, as shown below:

```mysql-sql
vim linkis_configuration_dml.sql
## Modify the default version of the corresponding engine
SET @SPARK_LABEL="spark-2.4.3";
SET @HIVE_LABEL="hive-1.2.1";
## Execute the initialization statement
source linkis_configuration_dml.sql
```

## 4. Installation and startup Linkis1.0

&nbsp;&nbsp;&nbsp;&nbsp;  Start Linkis 1.0  to verify whether the service has been started normally and provide external services. For details, please refer to: [Quick Deployment Linkis1.0](../Deployment_Documents/Quick_Deployment_Linkis1.0.md)<!--链接失效-->
