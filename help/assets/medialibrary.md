---
title: 使用Media Library进行基本的数字资产管理
description: 用于资产管理的[!DNL Experience Manager Assets]和Media Library。
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---


# 使用Media Library进行基本资源管理 {#manage-assets-using-media-library}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager]平台提供了不同的功能来管理资源。 Media Library允许用户将少量资源上传到存储库，搜索并使用网页中的资源，以及完成关于资源的简单资源管理任务。

Media Library是一种轻量级数字资产管理(DAM)解决方案，附带[!DNL Adobe Experience Manager Sites]免费许可证。 [!DNL Sites]是Web内容管理(WCM)产品。 Media Library可与Experience Manager的所有功能配合使用。

[!DNL Adobe Experience Manager Assets]许可证可单独购买。 [!DNL Experience Manager Assets]允许通过企业用例、元数据、架构、搜索和用户界面的自定义以及Media Library提供的功能之外的许多其他功能来稳健处理资源。

## 许可要求 {#avail-media-library-license}

拥有[!DNL Sites]许可证的客户有权使用Media Library。 它适用于[!DNL Experience Manager]的所有组件。

Media Library将作为站点的一部分进行安装。 除Sites许可证和安装之外，不需要其他许可证或软件包。

## [!DNL Assets]与Media Library {#assets-and-media-library}

Experience Manager Assets提供企业级DAM功能。 Assets功能通过[!DNL Experience Manager]在一个包中提供。 但是，未购买Assets许可证的用户无权使用高级DAM功能。 如果没有Assets许可证，则只有[Media Library功能](#use-media-library)可用。

如果要防止未经许可的[!DNL Assets]功能被意外使用，请从[!DNL Experience Manager]中删除所有特定于[!DNL Assets]的工作流、组件、分类、选项和[!DNL Assets]管理员。 这样做可防止您的用户意外使用您未授权的[!DNL Assets]功能。

## 使用Media Library {#use-media-library}

Media Library为以下用例提供基本DAM功能：

* 使用[!DNL Adobe Experience Manager Sites]创建的网页。
* 使用[!DNL Adobe Experience Manager Forms]创建的自适应表单和通信。
* 使用[!DNL Adobe Experience Manager Screens]创建的数字屏幕体验。
* 用于Headless操作的[!DNL Assets] HTTP REST API。

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

要使用Media Library功能，您可以使用默认的[!DNL Experience Manager]用户界面。 Media Library是[!DNL Experience Manager Sites]安装的一部分，无需单独的界面或加载项。 使用现有界面，Media Library用户有权完成以下任务：

* 创建文件夹以组织资源。
* 上传资源。
* Publish资源。
* 编辑、移动和复制资产。
* 浏览、筛选和搜索（包括相似性搜索）资源。
* 向元数据字段中添加值并编辑这些值，但智能标记字段除外，这些字段在默认情况下位于资产的[!UICONTROL 属性]页面的[!UICONTROL 基本]选项卡中。
* 添加和删除静态呈现版本。
* 下载文件夹、资源和资源演绎版。
* 创建资源版本。
* 创建资产并执行审核任务。
* 为资源作批注。
* 通过内容查找器将资产添加到[!DNL Sites]页面。
* 使用[!DNL Content Fragments]。
* 在Sites许可证下，为[!DNL Content Fragments]和引用的媒体资产使用HTTP REST和GraphQL API。
* Marketing Cloud集成。
* 自定义和扩展资产管理用户界面。
* 访问查询生成器(API)以扩展搜索功能。
* 创建静态标记。
* 创作项目和任务。
* 活动流（时间线）。
* 注释和批注。

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>许多高级DAM用例已由[!DNL Experience Manager Assets]完成。 Media Library许可证授权您使用Media Library仅完成列出的用例。 如果未列出用例，请勿将其与Media Library许可证一起使用。 如有任何疑问，请联系Adobe客户支持。

请注意，在没有[!DNL Assets]许可证的情况下，您无法使用智能标记、[!DNL Asset]链接、[!DNL Asset]选择器、批量标记、修改资源工作流或标准[!DNL Adobe Experience Manager]用户界面来访问Media Library。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>*  [!DNL Experience Manager Assets][&#128279;](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html?lang=zh-Hans)中的DAM功能
>* [[!DNL Experience Manager] 6.5 Managed Services产品说明](https://helpx.adobe.com/cn/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5内部部署产品说明](https://helpx.adobe.com/cn/legal/product-descriptions/adobe-experience-manager-on-premise.html)
