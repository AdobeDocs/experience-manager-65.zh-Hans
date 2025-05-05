---
title: 多语言资源
description: 了解如何自动执行工作流以将资源（包括二进制文件、元数据和标记）翻译成多种语言。
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: edccf23c-087e-4253-babb-dd4c6610517d
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---

# 多语言资源 {#multilingual-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

通过[!DNL Adobe Experience Manager Assets]可自动执行资产（包括二进制文件、元数据和标记）的翻译工作流，以生成其他语言的资产以用于多语言项目。

要自动化翻译工作流，请将翻译服务提供商与[!DNL Experience Manager]集成并创建项目以将资产翻译成多种语言。 [!DNL Experience Manager]支持人工翻译工作流和机器翻译工作流。

人工翻译：已翻译的资产将返回并导入到[!DNL Experience Manager]中。 当您的翻译提供商与[!DNL Experience Manager]集成时，资产会在[!DNL Experience Manager]和翻译提供商之间自动发送。

机器翻译：机器翻译服务将立即翻译资产的元数据和标记。

翻译资产包括以下各项：

1. [将Experience Manager连接到翻译服务提供商](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [创建翻译集成框架配置](/help/sites-administering/tc-tic.md)
1. [准备要翻译的资产](preparing-assets-for-translation.md)
1. [将翻译云服务应用到文件夹](transition-cloud-services.md)
1. [创建翻译项目](translation-projects.md)

如果您的翻译服务提供商不提供连接器来与[!DNL Experience Manager]集成，请使用[替代流程](/help/sites-administering/tc-manage.md#exporting-a-translation-job)。

另请参阅[为内容片段创建翻译项目](creating-translation-projects-for-content-fragments.md)。
