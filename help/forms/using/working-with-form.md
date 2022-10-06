---
title: 使用表单
seo-title: Working with a Form
description: 查看并更新与AEM Forms应用程序中的任务或起点关联的表单
seo-description: View and update the form associated with a task or Startpoint in the AEM Forms app
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 使用表单 {#working-with-a-form}

如果某个表单在表单应用程序中启用了同步功能，则会下载该表单，您可以直接使用该表单。

表单将在您的应用程序上下载，并且可脱机使用。 例如，您运营着一家银行，客户在您的网站上填写应用程序。 该应用程序是一种自适应表单，可接受客户提供的信息并将其存储以供审阅。 管理员会审阅表单，并在AEM创作实例中创建验证表单。 管理员支持将表单与AEM Forms应用程序同步。 如果验证表单在AEM Forms应用程序中可用，则您的现场代理可以使用移动设备来验证客户的详细信息。 移动设备与服务器同步，并且验证表单已加载到应用程序中。 您的现场代理可以访问您的客户、验证详细信息、将数据保存为草稿或提交验证表。 每次您的应用程序联机时，表单都会与服务器同步。

要在AEM Forms应用程序中同步您的表单，请执行以下操作：

1. 在创作实例中，选择一个表单，然后单击 **查看属性**.
1. 在属性页面中，单击 **高级。**
1. 在高级下，启用选项： **与AEM Forms应用程序同步**，然后点按 **保存**.

要同步多个表单，请在创作实例中，在表单管理器中选择多个表单，然后点按 **与AEM Forms应用程序同步**. 发布表单后，AEM Forms应用程序可以连接到发布服务器并获取表单。

>[!NOTE]
>
>支持的表单：
>
>* 自适应表单（不延迟加载）
>* 移动设备表单
>
>在与AEM Forms OSGi服务器同步的AEM Forms应用程序中获取的自适应表单中，不支持表单级别附件。 如果作者在创作表单时启用了字段级附件，则用户可以在字段中附加文件。

**打开和更新表单**

1. 要打开表单，请点按主屏幕中的表单。
1. 您可以更新表单的字段、添加附件、另存为草稿并提交它。
