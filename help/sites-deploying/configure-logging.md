---
title: 日志记录
description: 了解如何为中央日志记录服务配置全局参数、各个服务的特定设置以及如何请求数据记录。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: b32001a1-0078-43f6-89d6-781d6d2e9c94
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# 日志记录{#logging}

通过AEM，您可以配置：

* 中央日志记录服务的全局参数
* 请求数据记录；请求信息的专用记录配置
* 各个服务的特定设置；例如，单个日志文件以及日志消息的格式

这些都是[OSGi配置](/help/sites-deploying/configuring-osgi.md)。

>[!NOTE]
>
>AEM中的日志记录基于Sling原则。 有关详细信息，请参阅[Sling日志记录](https://sling.apache.org/site/logging.html)。

## 全局日志记录 {#global-logging}

[Apache Sling日志记录配置](/help/sites-deploying/osgi-configuration-settings.md)用于配置根日志程序。 这会定义用于登录AEM的全局设置：

* 日志记录级别
* 中央日志文件的位置
* 要保留的版本数
* 版本轮换；最大大小或时间间隔
* 写入日志消息时要使用的格式

## 适用于单个服务的记录器和写入程序 {#loggers-and-writers-for-individual-services}

除了全局日志记录设置之外，AEM还允许您为单个服务配置特定设置：

* 特定的日志记录级别
* 单个日志文件的位置
* 要保留的版本数
* 版本轮换；最大大小或时间间隔
* 写入日志消息时要使用的格式
* 日志程序（提供日志消息的OSGi服务）

这使您可以将单个服务的日志消息通道到一个单独的文件中。 这在开发或测试期间可能特别有用；例如，当您需要提高特定服务的日志级别时。

AEM使用以下功能将日志消息写入文件：

1. **OSGi服务** （记录器）写入日志消息。
1. **日志记录器**&#x200B;会根据您的规范接收此消息并将其格式化。
1. **日志记录写入程序**&#x200B;将所有消息写入您定义的物理文件。

这些元素由相应元素的以下参数链接：

* **日志记录器（日志记录器）**

  定义生成消息的服务。

* **日志文件（日志记录器）**

  定义用于存储日志消息的物理文件。

  用于将日志记录器与日志编写器相关联。 该值必须与日志记录编写器配置中的相同参数相同，才能建立连接。

* **日志文件（日志写入程序）**

  定义日志消息将写入到的物理文件。

  这必须与日志记录编写器配置中的相同参数相同，否则将无法进行匹配。 如果没有匹配项，将使用默认配置（每日日志轮换）创建隐式的Writer。

### 标准记录器和写入程序 {#standard-loggers-and-writers}

标准AEM安装中包含某些记录器和写入程序。

第一个是特殊情况，因为它同时控制`request.log`和`access.log`文件：

* 记录器：

   * Apache Sling可自定义请求数据记录器

     (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 将有关请求内容的消息写入`request.log`。

* 链接到：

   * Apache Sling请求记录器

     (org.apache.sling.engine.impl.log.RequestLogger)

   * 将消息写入`request.log`或`access.log`。

如有必要，可以自定义这些选项，但标准配置适用于大多数安装。

其他对将遵循标准配置：

* 记录器：

   * Apache Sling日志记录器配置

     (org.apache.sling.commons.log.LogManager.factory.config)

   * 将`Information`条消息写入`logs/error.log`。

* 指向作者的链接：

   * Apache Sling日志记录编写器配置

     (org.apache.sling.commons.log.LogManager.factory.writer)

* 记录器：

   * Apache Sling日志记录器配置
(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * 将服务`org.apache.pdfbox`的`Warning`消息写入`../logs/error.log`。

* 未链接到特定的Writer，因此将创建并使用具有默认配置（每日日志轮换）的隐式Writer。

### 创建自己的日志记录器和作者 {#creating-your-own-loggers-and-writers}

您可以定义自己的记录器/写入器对：

1. 创建工厂配置[Apache Sling日志记录器配置](/help/sites-deploying/osgi-configuration-settings.md)的实例。

   1. 指定日志文件。
   1. 指定日志程序。
   1. 根据需要配置其他参数。

1. 创建工厂配置[Apache Sling日志记录编写器配置](/help/sites-deploying/osgi-configuration-settings.md)的实例。

   1. 指定日志文件 — 该文件必须与为记录器指定的日志文件匹配。
   1. 根据需要配置其他参数。

>[!NOTE]
>
>在某些情况下，您可能希望创建[自定义日志文件](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)。
