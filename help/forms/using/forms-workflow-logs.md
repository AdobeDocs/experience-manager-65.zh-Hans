---
title: 登录 AEM Forms 工作流
description: 了解如何调试AEM Forms工作流问题并为AEM Forms工作流启用调试日志记录以查看日志。
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
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
source-wordcount: '293'
ht-degree: 8%
---
# 登录 AEM Forms 工作流{#logging-in-aem-forms-workflows}

Forms Workflow步骤提供详细的日志，可方便地调试与工作流相关的问题。 为AEM Forms工作流启用调试日志记录以查看日志。

默认情况下，**error.log**&#x200B;文件中所有日志记录信息在&#x200B;*/crx-repository/logs/*&#x200B;目录中可用。

表单工作流的调试日志包括：

* 输入每个工作流步骤。 例如：\
  `[DEBUG] "Executing Invoke DDX Process step"`

* 退出每个工作流步骤。 例如：\
  `[DEBUG] "Successfully finished Invoke DDX Process step"`

* 服务调用消息。 例如：\
  `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* 服务退出消息。 例如：\
  `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* 从元数据映射读取的变量。 例如：\
  `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* 变量写入JCR存储库。 例如：

  ```verilog
     [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
  ```

* 具有完整栈栈跟踪的异常消息。 例如：\
  `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 动态步骤元数据参数。 例如：

  ```verilog
  [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
   [DEBUG] Locale to be used for Document of Record is <locale>
  ```

以下示例说明了“签名文档”步骤的日志：

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

使用日志评估：

* 您使用的是正确的Adobe Sign配置。
* 成功创建协议后，Adobe Sign服务即会退出。
* 签名文档步骤退出并显示成功消息。

如果出现异常，可以查看完整的栈栈跟踪以评估错误的原因。

## 为AEM Forms工作流启用调试日志记录 {#enable-debug-logging-for-aem-forms-workflows}

执行以下操作，以便为AEM Forms工作流启用调试日志记录：

1. 转到以下地址的AEM Web控制台配置管理器：

   https://'[服务器]：[端口]'/system/console/configMgr

1. 选择&#x200B;**[!UICONTROL Sling]** > **[!UICONTROL 日志支持]**。
1. 选择&#x200B;**[!UICONTROL 添加新记录器。]**
1. 选择&#x200B;**[!UICONTROL 调试]**&#x200B;作为&#x200B;**[!UICONTROL 日志级别]**。
1. 指定日志文件的位置。 日志文件的默认位置为： *logs\error.log*
1. 在&#x200B;**[!UICONTROL 记录器]**&#x200B;列中指定包名称为&#x200B;**com.adobe.granite.workflow.core**。

   执行这些步骤可以存储&#x200B;**com.adobe.granite.workflow.core**&#x200B;包的调试日志。 选择&#x200B;**[!UICONTROL +]**&#x200B;并将以下包名称添加到列表：

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
