# Python 引擎使用文档

本文主要介绍在Linkis1.0中，Python引擎的配置、部署和使用。

## 1.Spark引擎使用前的环境配置

如果您希望在您的服务器上使用python引擎，您需要保证用户的PATH中是有python的执行目录和执行权限。

| 环境变量名 | 环境变量内容    | 备注                           |
|------------|-----------------|--------------------------------|
| python     | python执行环境  | 建议使用anaconda的python执行器 |

表1-1 环境配置清单

## 2.Python引擎的配置和部署

### 2.1 Python版本的选择和编译

Python是支持python2 和
python3的，您可以简单更改配置就可以完成Python版本的切换，不需要重新编译python的引擎版本。

### 2.2 python engineConn部署和加载

此处可以使用默认的加载方式即可正常使用。

### 2.3 python引擎的标签

此处可以使用默认的dml.sql进行插入即可正常使用。

## 3.Python引擎的使用

### 准备操作

在linkis上提交python之前，您只需要保证您的用户的\$PATH中有python的路径即可。

### 3.1 Scriptis的使用方式

Scriptis的使用方式是最简单的，您可以直接进入Scriptis，右键目录然后新建python脚本并编写python代码并点击执行。

python的执行逻辑是通过 Py4j的方式，启动一个的python
的gateway，然后Python引擎将代码提交到python的执行器进行执行。

![](../Images/EngineUsage/python-run.png)

图3-1 python的执行效果截图
<!--此图片页面显示不出来-->
### 3.2工作流的使用方式

DSS工作流也有python的节点，您可以拖入工作流节点，然后双击进入然后进行编辑代码，然后以工作流的形式进行执行。

### 3.3 Linkis Client的使用方式

Linkis也提供了client的方式进行调用spark的任务，调用的方式是通过LinkisClient提供的SDK的方式。我们提供了java和scala两种方式进行调用，具体的使用方式可以参考<https://github.com/WeBankFinTech/Linkis/wiki/Linkis1.0%E7%94%A8%E6%88%B7%E4%BD%BF%E7%94%A8%E6%96%87%E6%A1%A3>。

## 4.Python引擎的用户设置

除了以上引擎配置，用户还可以进行自定义的设置，比如python的版本和以及python需要加载的一些module等。

![](../Images/EngineUsage/jdbc-conf.png)

图4-1 python的用户自定义配置管理台
<!--此图片页面显示不了-->