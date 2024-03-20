---
title: 与ExactTarget集成
description: 了解如何将Adobe Experience Manager与ExactTarget集成。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# 与ExactTarget集成{#integrating-with-exacttarget}

将Adobe Experience Manager (AEM)与Exact Target集成后，您可以通过Exact Target管理和发送在AEM中创建的电子邮件。 它还允许您通过AEM页面上的AEM表单来使用Exact Target的潜在客户管理功能。

该集成提供了以下功能：

* 能够在AEM中创建电子邮件并将其发布到Exact Target以供分发。
* 能够设置AEM表单的操作，以创建Exact Target订阅服务器。

配置ExactTarget后，您可以将新闻稿或电子邮件发布到ExactTarget。 请参阅 [将新闻稿发布到电子邮件服务](/help/sites-authoring/personalization.md).

## 创建ExactTarget配置 {#creating-an-exacttarget-configuration}

可以通过Cloudservices或Tools添加ExactTarget配置。 本节将介绍这两种方法。

### 通过Cloudservices配置ExactTarget {#configuring-exacttarget-via-cloudservices}

要在Cloud Service中创建ExactTarget配置，请执行以下操作：

1. 在欢迎页面上，单击 **Cloud Service**. (或直接访问 `https://<hostname>:<port>/etc/cloudservices.html`.)
1. 单击 **ExactTarget** 然后 **配置**. 将打开ExactTarget配置窗口。

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. 输入标题和（可选）名称，然后单击 **创建**. 此 **ExactTarget设置** 配置窗口将打开。

   ![chlimage_1](assets/chlimage_1.jpeg)

1. 输入用户名、密码，然后选择API端点(例如， **https://webservice.exacttarget.com/Service.asmx**)。
1. 单击 **连接到ExactTarget。** 成功连接后，您会看到成功对话框。 框点击 **确定** 以退出窗口。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 选择一个帐户（如果可用）。 该帐户适用于Enterprise 2.0客户。 单击&#x200B;**确定**。

   已配置ExactTarget。 您可以通过单击来编辑配置 **编辑**. 您可以通过单击转到ExactTarget **转到ExactTarget**.

1. AEM现在提供数据扩展功能。 您可以导入ExactTarget数据扩展列。 除了成功创建的ExactTarget配置以外，通过单击旁边显示的“+”号，可以对其进行配置。 可以从下拉列表中选择任何现有数据扩展。 有关如何配置数据扩展的更多信息，请参阅 [ExactTarget文档](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_relationships_classic.htm&amp;type=5).

   导入的数据扩展列以后可通过 **文本和个性化** 组件。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 通过工具配置ExactTarget {#configuring-exacttarget-via-tools}

要在工具中创建ExactTarget配置，请执行以下操作：

1. 在欢迎页面上，单击 **工具**. 或直接导航到此处，转到 `https://<hostname>:<port>/misadmin#/etc`.
1. 选择 **工具**，则 **Cloud Service配置，** 则 **ExactTarget**.
1. 单击 **新建** 打开**创建页面**窗口。

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. 输入 **标题** 和（可选） **名称**，然后单击 **创建**.
1. 按照上一过程中的步骤4输入配置信息。 按照该过程完成ExactTarget的配置。

### 添加多个配置 {#adding-multiple-configurations}

要添加多个配置，请执行以下操作：

1. 在欢迎页面上，单击 **Cloud Service** 并单击 **ExactTarget**. 单击 **显示配置** 如果有一个或多个ExactTarget配置可用，则会显示此字段。 列出了所有可用的配置。
1. 单击 **+** 在“Available configurations（可用配置）”旁边签名。 这将打开 **创建配置** 窗口。 按照之前的配置过程创建配置。
