---
title: 获取带有附件的电子邮件的其他步骤
description: 了解如何在无法检索JEE平台上的AEM Forms的带附件的电子邮件时修复错误。
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 无法获取JEE平台上AEM Forms的包含附件的电子邮件{#unable-to-get-email-with-attachments}

该问题适用于以下版本：

* Experience Manager6.5 Forms

## 问题 {#issue}

用户无法执行操作，例如通过电子邮件发送PDF或通过提交配置包含附件。

## 解决方案 {#solution}

1. 将jar下载为[java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar)，然后解压缩下载的jar文件以获取清单文件。

1. 使用从步骤1检索到的`java.mail-1.0.jar`的清单文件创建自定义jar文件，如`java.mail-1.5.jar`。

1. 打开清单文件，并将`1.5.0`的所有匹配项替换为`1.5.6`，将`Bundle-Version: 1.0`替换为`Bundle-Version:1.5`

1. 使用以下命令在`C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin`文件夹中创建自定义jar (`java.mail-1.5.jar`)文件，如下所示：
   `jar -cfm java.mail-1.5.jar manifest.mf`

   在上述命令中，*manifest.mf*&#x200B;是清单文件的名称，*java.mail-1.5.jar*&#x200B;是在执行上述命令后创建的文件的名称。

1. 下载[javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1)。

1. 导航到`http://<server name>:<port>/lc/system/console/bundles`并删除名为`JavaMail API (com.sun.mail.javax.mail) version 1.6.2`的包。

1. 安装从步骤3获得的`java.mail-1.5.jar`。 此步骤将重新启动JEE部署的sling属性。 等待`http://<server name>:<port>/lc/system/console/bundles`处安装的包将状态显示为&#x200B;**活动**。

   >如果状态仍为&#x200B;**InActive**，请重新启动   从&#x200B;**服务控制台**&#x200B;中的&#x200B;**JBoss®**。


1. 安装使用步骤5下载的`javax.mail-1.5.6.redhat-1.jar`文件。

1. 从&#x200B;**服务控制台**&#x200B;停止&#x200B;**JBoss®**，并将以下属性附加到&#x200B;**Sling.properties**&#x200B;文件：
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 重新启动&#x200B;**JBoss®**。

>[!NOTE]
>
> 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java进程）重新启动AEM SDK可能会导致AEM开发环境不一致。
