---
title: 连接到 Microsoft Translator
description: 了解如何将 AEM 连接到现成的 Microsoft Translator 以自动化您的翻译工作流。
feature: Language Copy
role: Admin
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
solution: Experience Manager, Experience Manager Sites
source-git-commit: 3bb516289dbff4fb3b94685b9e25360e7717776e
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 63%

---

# 连接到 Microsoft Translator {#connecting-to-microsoft-translator}

AEM为[Microsoft Translator](https://www.microsoft.com/en-us/translator/business/)提供内置连接器以翻译页面内容或资源。 从Microsoft获取使用Microsoft Translator的许可证后，请按照本页上的说明配置连接器。

| 属性 | 描述 |
|---|---|
| 翻译标签 | 翻译服务的显示名称 |
| 翻译属性 | （可选）对于用户生成的内容，为已翻译文本旁边显示的属性，例如`Translations by Microsoft` |
| 工作区 ID | （可选）要使用的自定义 Microsoft Translator 引擎的 ID |
| 订阅密钥 | 您的 Microsoft Translator 的 Microsoft 订阅密钥 |

以下过程将创建 Microsoft Translator 配置。

1. 在[导航面板中，](/help/sites-authoring/basic-handling.md#first-steps)单击&#x200B;**工具** > **Cloud Service** > **翻译Cloud Service**。
1. 导航到要创建配置的位置。通常它在您的站点根中，也可以是全局默认配置。
1. 单击&#x200B;**创建**&#x200B;按钮。
1. 定义您的配置。
   1. 在下拉列表中选择 **Microsoft Translator**。
   1. 为您的配置键入标题。标题在 Cloud Service 控制台中以及页面属性下拉列表中标识该配置。
   1. （可选）键入一个名称以用于存储该配置的存储库节点。

   ![创建翻译配置](assets/create-translation-config.png)

1. 单击&#x200B;**创建**。
1. 在&#x200B;**编辑配置**&#x200B;窗口中，提供上一个表中描述的翻译服务的值。

   ![编辑翻译配置](assets/msft-config-ui.png)

1. 单击&#x200B;**连接**&#x200B;以验证连接。
1. 单击&#x200B;**保存并关闭**。

## 发布Translator服务配置 {#publishing-the-translator-service-configurations}

作为最后一步，请使用[发布树](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree)操作发布Microsoft Translator配置以支持已发布的已翻译内容。
