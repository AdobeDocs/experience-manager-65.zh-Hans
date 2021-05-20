---
title: 监控AEM Forms部署
seo-title: 监控AEM Forms部署
description: 您可以从系统级别和内部级别监控AEM表单部署。 通过本文档了解有关监控AEM表单部署的更多信息。
seo-description: 您可以从系统级别和内部级别监控AEM表单部署。 通过本文档了解有关监控AEM表单部署的更多信息。
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
exl-id: 931e8095-5c7c-4c1f-b95b-75ac2827d4f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# 监控AEM表单部署{#monitoring-aem-forms-deployments}

您可以从系统级别和内部级别监控AEM表单部署。 您可以使用诸如HP OpenView、IBM Tivoli和CA UniCenter等专业管理工具以及名为&#x200B;*JConsole*&#x200B;的第三方JMX监视器来专门监视Java活动。 实施监控策略可提高AEM表单部署的可用性、可靠性和性能。

有关监控AEM表单部署的更多信息，请参阅[监控AEM表单部署的技术指南](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf)。

## 使用MBeans {#monitoring-using-mbeans}进行监控

AEM Forms提供两个注册的MBean，用于提供导航和统计信息。 以下是唯一支持集成和检查的MBean:

* **服务统计：** 此MBean提供有关服务名称及其版本的信息。
* **操作统计：** 此MBean提供每个表单服务器服务的统计信息。在这里，管理员可以获取有关特定服务的信息，如调用时间、错误数等。

### ServiceStatticMbean公共接口{#servicestatisticmbean-public-interfaces}

出于测试目的，可以访问ServiceStatistic MBean的以下公共接口：

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### OperationStatitucMbean公共接口{#operationstatisticmbean-public-interfaces}

可以访问OperationStatistic MBean的以下公共接口以进行测试：

```java
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### MBean树和操作统计数据{#mbean-tree-operation-statistics}

使用JMX控制台(JConsole)，可以获取OperationStatistic MBean中的统计信息。 这些统计信息是MBean的属性，可以在以下层次结构树下导航：

**MBean树**

**Adobe域名：** 取决于应用程序服务器。如果应用程序服务器未定义域，则默认为adobe.com。

**ServiceType:** AdobeService是用于列出所有服务的名称。

**AdobeServiceName:** 服务名称或服务ID。

**版本：** 服务的版本。

**操作统计**

**调用时间：** 执行方法所花费的时间。这不包括序列化请求、从客户端传输到服务器并反序列化请求的时间。

**调用计数：** 调用服务的次数。

**平均调用时间：** 自服务器启动以来已执行的所有调用的平均时间。

**最大调用时间：** 自服务器启动以来执行的最长调用的持续时间。

**最小调用时间：** 自服务器启动以来执行的最短调用的持续时间。

**例外计数：** 导致失败的调用次数。

**异常消息：** 上次发生异常的错误消息。

**上次采样日期时间：** 上次调用的日期。

**时间单位：** 默认值为毫秒。

要启用JMX监控，应用程序服务器通常需要一些配置。 有关具体信息，请参阅您的应用程序服务器文档。

### 如何设置开放JMX访问{#examples-of-how-to-set-up-open-jmx-access}的示例

**JBoss 4.0.3/4.2.0 — 配置JVM启动**

要从JConsole查看MBean，请配置JBoss应用程序服务器的JVM启动参数。 确保从run.bat/sh文件启动JBoss。

1. 编辑位于InstallJBoss/bin下的run.bat文件。
1. 找到JAVA_OPTS行并添加以下内容：

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 — 配置JVM启动**

1. 编辑位于`[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`下的startWebLogic.bat文件。
1. 找到JAVA_OPTS行并添加以下内容：

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. 重新启动WebLogic。

>[!NOTE]
>
>对于WebLogic，您可以使用远程或IIOP访问MBean。

**远程访问MBean**

1. 启动JConsole以进行新连接，然后单击远程选项卡。
1. 输入主机名和端口（9088，在JVM的启动选项期间指定的编号）。

**Websphere 6.1 — 配置JVM启动**

1. 在Admin Console(Application Server > server1 > Process Definition > JVM)中，将以下行添加到通用JVM参数的字段中：

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. 在/opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties文件(或&lt;Your Websphere JRE>/ lib/management/management.properties)中添加或取消注释以下三行：

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. 重新启动WebSphere。
