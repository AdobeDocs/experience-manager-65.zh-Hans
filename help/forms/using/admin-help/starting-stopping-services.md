---
title: 启动和停止服务
description: 了解如何启动和停止与AEM Forms模块以及应用程序服务器和数据库关联的服务。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 启动和停止服务 {#starting-and-stopping-services}

AEM表单中包含两种类型的服务：

* 控制AEM表单应用程序服务器和数据库的服务。
* 控制AEM表单模块的服务

## 启动或停止与AEM表单模块关联的服务 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM表单模块(例如Forms、Rights Management、输出)作为服务运行。 有时，您可能需要停止或启动这些AEM表单模块的服务。 例如，在更改服务的设置后，必须停止并重新启动AEM表单服务。

>[!NOTE]
>
> 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java进程）重新启动AEM SDK可能会导致AEM开发环境不一致。

1. 在管理控制台中，单击&#x200B;**服务** > **应用程序和服务** > **服务管理**。
1. 在“服务管理”页上，选中要停止或启动的服务旁边的复选框，然后单击停止或启动。

## 启动或停止应用程序服务器和数据库的服务 {#start-or-stop-services-for-the-application-server-and-database}

AEM Forms的完整实施包括应用程序服务器和数据库服务：

* AEM表单的&#x200B;*`[application server]`*
* AEM表单的&#x200B;*`[database]`*

在Windows上，这些服务可通过&#x200B;**管理工具** > **服务面板**&#x200B;访问。 例如，如果您使用turnkey方法在JBoss上安装了AEM表单，则您的系统上可以使用以下服务：

* 适用于Adobe Experience Manager表单的JBoss
* 适用于Adobe Experience Manager的MySQL表单

通过从“服务”面板的列表中选择这些服务，然后单击面板上的相应操作按钮来启动或停止这些服务。

在UNIX®或Linux上，从命令行输入以下文本，其中&#x200B;*`[service name]`*&#x200B;是正在验证的服务的名称：

```java
     ps -A | grep [service name]
```
