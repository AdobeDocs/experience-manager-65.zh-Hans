---
title: 云配置
description: 将按需应用程序关联到云配置可允许Adobe Experience Manager (AEM)通过建立双向链接直接与Mobile On-Demand托管项目通信。 关注此页面以了解更多信息。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---

# 云配置{#cloud-configuration}

{{ue-over-mobile}}

将按需应用程序关联到云配置可允许Adobe Experience Manager (AEM)通过建立双向链接直接与Mobile On-Demand托管项目通信。 通过将您的应用程序关联到Mobile On-Demand项目，您将能够在AEM中执行内容创建（例如文章、横幅和收藏集），还可以将该内容提供给Mobile On-Demand。

从那里，可以发布、预览和管理内容。 您还可以将现有Mobile On-Demand内容导入AEM并执行内容编辑。

## 设置云配置 {#setting-up-cloud-configuration}

>[!CAUTION]
>
>在开始为On-Demand应用程序配置云配置之前，您必须熟悉AEM Mobile配置和配置AEM Mobile On-demand Services客户端。
>
>有关详细信息，请参阅管理部分中的[设置AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md)。

要配置Mobile On-DemandCloud Service，请单击应用程序仪表板中&#x200B;**管理连接**&#x200B;图块右上角的顶部齿轮。

您应该熟悉应用程序功能板和可用的磁贴。 有关更多详细信息，请参阅[AEM Mobile应用程序功能板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

### 设置指向云配置的链接 {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>确保您具有现有的按需客户端和云配置。
>
>有关详细信息，请参阅管理部分中的[设置AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md)。

以下步骤描述了如何设置指向云配置的链接：

1. 从&#x200B;**Mobile**&#x200B;中选择&#x200B;**应用**，然后从目录中选择您的Mobile On-Demand应用。
1. 单击&#x200B;**管理连接**&#x200B;拼贴上的齿轮图标。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 输入现有的配置，或通过输入&#x200B;**配置标题**、**设备ID**&#x200B;和&#x200B;**设备令牌**&#x200B;创建配置。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 验证您的&#x200B;**设备ID**&#x200B;和&#x200B;**设备令牌**&#x200B;后，从列表中选择您的按需项目。

   单击&#x200B;**“提交”。**

   ![chlimage_1-67](assets/chlimage_1-67.png)

   **管理连接**&#x200B;图块显示您的云配置。

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >如果您尝试更改此应用程序与哪个项目相关联，则在功能板中切换项目时，您将会收到内容完整性问题警告，如下图所示：

   ![chlimage_1-69](assets/chlimage_1-69.png)

### 后续步骤 {#the-next-steps}

为应用程序配置云配置后，请参阅以下用于管理内容的资源：

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理横幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理收藏集](/help/mobile/mobile-on-demand-managing-collections.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布/取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用Preflight预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
