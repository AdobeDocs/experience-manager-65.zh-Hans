---
title: 使用表单
seo-title: 使用表单
description: 视图并更新与AEM Forms应用程序中的任务或起点关联的表单
seo-description: 视图并更新与AEM Forms应用程序中的任务或起点关联的表单
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---


# 使用表单{#working-with-a-form}

如果表单在表单应用程序中启用同步功能，则会下载表单，您可以直接使用它。

表单将下载到您的应用程序中，并可脱机使用。 例如，您运营的是一家银行，客户填写您网站上的一个应用程序。 该应用程序是一种自适应表单，可接受客户提供的信息并将其存储以供审阅。 管理员会查看表单，并在AEM作者实例中创建验证表单。 管理员启用表单与AEM Forms应用程序的同步。 如果验证表单在AEM Forms应用程序中可用，您的现场代理可以使用移动设备验证客户的详细信息。 移动设备与服务器同步，验证表单加载到应用程序中。 您的现场代理可以访问您的客户、验证详细信息、将数据保存为草稿或提交验证表单。 每次您的应用程序联机时，表单都与服务器同步。

要在AEM Forms应用程序中同步表单：

1. 在创作实例中，选择一个表单，然后单击&#x200B;**视图属性**。
1. 在属性页面中，单击&#x200B;**高级。**
1. 在“高级”下，启用选项：**与AEM FormsApp**&#x200B;同步，然后点按&#x200B;**保存**。

要同步多个表单，请在创作实例中，在表单管理器中选择多个表单，然后点按&#x200B;**与AEM FormsApp**&#x200B;同步。 发布表单时，AEM Forms应用程序可以连接到发布服务器并获取表单。

>[!NOTE]
>
>支持的表单：
>
>* 自适应表单（无延迟加载）
>* 移动表单

>
>
在与AEM FormsOSGi服务器同步的AEM Forms应用程序中获取的自适应表单中，不支持表单级别附件。 如果作者在创作表单时启用了字段级附件，则用户可以附加字段中的文件。

**打开和更新表单**

1. 要打开表单，请点击主屏幕中的表单。
1. 您可以更新表单的字段、添加附件、另存为草稿并提交它。
