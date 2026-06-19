---
title: 缓解AEM Forms JEE中的序列化问题 |Adobe Experience Manager
description: 了解如何在JDK 8上运行的AEM Forms JEE中减轻Java反序列化问题。
solution: Experience Manager, Experience Manager Forms
feature: Security
version: Experience Manager 6.5
type: Documentation
role: Admin
source-git-commit: ec3941675081255879065c3be9d5af77474b2072
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---


# 缓解AEM Forms JEE中的序列化问题 {#mitigating-serialization-issues-in-aem-forms-jee}

AEM Forms JEE包含一个反序列化防火墙，该防火墙在尝试反序列化对象之前添加预检检查。 此检查针对防火墙样式的允许列表和/或序列化测试类名，并拒绝已知可通过Java™反序列化攻击攻击的类。 基础代理是Adobe修改的开源[NotSoSerial](https://github.com/kantega/notsoserial)项目分发，根据[Apache 2许可证](https://www.apache.org/licenses/LICENSE-2.0)授予许可。

在运行&#x200B;**JDK 11或更高版本**&#x200B;的安装中，此保护由平台的本机序列化过滤激活，无需手动步骤。 在运行&#x200B;**JDK 8**&#x200B;的安装上，本机序列化筛选无效，因此代理必须在启动时显式附加到JVM。 本文介绍了如何这样做。

>[!NOTE]
>
>如果反序列化筛选器运行状况检查已报告您的服务器上处于活动状态（请参阅[验证代理的激活](#verifying-the-agents-activation)），则您的应用程序服务器已受保护，您可以跳过本文档中的其余步骤。

## 开始之前 {#before-you-begin}

确认应用程序服务器用于运行的Java™版本：

```shell
java -version
```

如果报告的版本为`1.8.x` (JDK 8)，则应用本文中的步骤。 如果是11或更高版本，则无需手动操作；请使用[验证代理的激活](#verifying-the-agents-activation)中所述的运行状况检查来验证保护。

在接下来的步骤中，`<jee-installation-directory>`将引用AEM Forms JEE安装的根目录。

## 应用代理 {#applying-the-agent}

>[!IMPORTANT]
>
>这些步骤需要重新启动应用程序服务器。 将它们应用于每个受影响的实例。

1. **验证当前状态。** 浏览到反序列化过滤器运行状况检查：

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   如果检查报告为活动，则实例已受保护，无需执行进一步操作。 如果失败，请继续执行以下步骤。

1. **验证代理JAR是否已存在。** 检查以下位置中的`notsoserial.jar`：

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/
   ```

1. **如果缺少JAR，请添加它。** 下载[`notsoserial.jar`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/notsoserial.jar)并将其复制到每个实例上的上述文件夹中：

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >在发布之前，请将此步骤替换为代理的Forms JEE分发的官方Adobe下载位置。

1. **更新应用服务器的JVM启动参数**&#x200B;以附加代理。 将以下选项添加到Java™运行行：

   ```shell
   -javaagent:<jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   Java™运行行的确切位置取决于您的应用程序服务器（例如，JBoss、WebLogic或WebSphere®）。 将选项添加到用于启动AEM Forms JEE应用程序服务器的JVM选项。

1. **重新启动JEE服务器**，以便在JVM启动时加载代理。

1. **重新验证。** 再次浏览运行状况检查：

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   运行状况检查现在应报告为正常。

## 验证代理的激活 {#verifying-the-agents-activation}

您可以随时通过浏览到以下URL来验证反序列化代理的配置：

```text
https://<server>:<port>/system/console/healthcheck?tags=deserialization
```

将显示与代理相关的运行状况检查列表。 如果检查通过，则代理将被正确激活。 如果它们在JDK 8实例上失败，则代理尚未加载，您必须使用[应用代理](#applying-the-agent)中的步骤手动附加该代理。

## 配置代理 {#configuring-the-agent}

如果应用程序服务器的Java™版本使用JDK 8运行，则以下步骤适用。 在附加代理后可以使用[应用代理](#applying-the-agent)中的步骤对其进行配置。

对于大多数安装，默认配置已足够。 它包括已知可远程攻击的类的阻止列表以及可安全反序列化受信任数据的包的序列。 阻止列表在任何条目之前应用。

防火墙配置是动态的，可以随时更改：

1. 转到位于`https://<server>:<port>/system/console/configMgr`的Web控制台。

1. 搜索并单击&#x200B;**反序列化防火墙配置**。

此配置包含允许列表、阻止列表和诊断日志记录选项：

* **允许列表** — 允许反序列化的类或包前缀。 如果您反序列化自己的类，请在此处添加相关的类或包。
* **阻止列表** — 不允许反序列化的类。 初始集仅限于发现易受远程执行攻击的类。
* **诊断日志记录** — 进行反序列化时要记录的选项。 默认&#x200B;**class-name-only**&#x200B;报告正在反序列化的类。 **全栈栈**&#x200B;选项记录第一次反序列化尝试的Java™栈栈，这有助于在您的使用中查找和删除不受信任的反序列化。 这些选项仅在首次使用时记录。

## 其他注意事项 {#other-considerations}

* 该代理用于缓解当前已知的易受攻击的类。 如果项目反序列化不受信任的数据，则它仍可能会遭受拒绝服务、内存不足或未知的未来反序列化攻击。
* 如果在JRE （Java™运行时环境）而不是JDK （Java™开发工具包）上运行，则动态代理加载所需的工具不可用，并且必须在启动时手动附加代理，如[应用代理](#applying-the-agent)中所述。
* 如果您在® JVM上运行，请查看有关Java™附加API支持的文档。
