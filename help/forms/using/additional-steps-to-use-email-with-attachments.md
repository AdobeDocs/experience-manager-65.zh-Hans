---
title: 获取带有附件的电子邮件的其他步骤
description: 了解如何在无法检索JEE平台上的AEM Forms的带附件的电子邮件时修复错误。
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 12%
---
# 无法获取JEE平台上AEM Forms的包含附件的电子邮件{#unable-to-get-email-with-attachments}

该问题适用于以下版本：

* Experience Manager 6.5 Forms

## 问题 {#issue}

用户无法执行操作，例如通过电子邮件发送PDF或通过提交配置包含附件。

## 解决办法 {#solution}

1. 将jar下载为[java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar)，然后解压缩下载的jar文件以获取清单文件。

1. 使用从步骤1检索到的`java.mail-1.0.jar`的清单文件创建自定义jar文件，如`java.mail-1.5.jar`。

1. 打开清单文件，并将`1.5.0`的所有匹配项替换为`1.5.6`，将`Bundle-Version: 1.0`替换为`Bundle-Version:1.5`

1. 使用以下命令在`C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin`文件夹中创建自定义jar (`java.mail-1.5.jar`)文件，如下所示：
   `jar -cfm java.mail-1.5.jar manifest.mf`

   在上述命令中，*manifest.mf*&#x200B;是清单文件的名称，*java.mail-1.5.jar*&#x200B;是在执行上述命令后创建的文件的名称。

1. 下载[javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1)。

1. 导航到`http://<server name>:<port>/lc/system/console/bundles`并删除名为`JavaMail API (com.sun.mail.javax.mail) version 1.6.2`的包。

1. 安装从步骤3获得的`java.mail-1.5.jar`。 此步骤将重新启动JEE部署的sling属性。 等待`http://<server name>:<port>/lc/system/console/bundles`处安装的包将状态显示为&#x200B;**活动**。

   >如果状态仍为&#x200B;**InActive**，请从&#x200B;**服务控制台**&#x200B;重新启动&#x200B;**JBoss®**。


1. 安装使用步骤5下载的`javax.mail-1.5.6.redhat-1.jar`文件。

1. 从&#x200B;**服务控制台**&#x200B;停止&#x200B;**JBoss®**，并将以下属性附加到&#x200B;**Sling.properties**&#x200B;文件：
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 重新启动&#x200B;**JBoss®**。

>[!NOTE]
>
> 建议使用 “Ctrl + C” 命令重新启动 SDK。 如果使用其他方式（例如停止 Java 进程）重新启动 AEM SDK，则可能会导致 AEM 开发环境出现不一致情况。
