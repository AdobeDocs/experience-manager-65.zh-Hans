---
title: 通过Dynamic Media Classic使内容交付网络缓存失效
description: 使CDN（内容分发网络）缓存的内容失效可让您快速更新Dynamic Media Classic交付的资源，而不是等待缓存过期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: CDN Cache,Dynamic Media Classic
role: User, Admin
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 13%

---

# 通过Dynamic Media Classic使内容交付网络缓存失效 {#invalidating-your-cdn-cached-content}

Dynamic Media资源由CDN（内容分发网络）缓存，以便快速交付。 但是，当您更新资产时，希望这些更改立即生效。 使CDN缓存内容失效可让您快速更新Dynamic Media交付的资源，而不是等待缓存过期。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media捆绑在一起的现成CDN。 此功能不支持任何其他自定义CDN。

>[!IMPORTANT]
>
>以下步骤仅适用于Adobe Experience Manager 6.5、Service Pack 5(Experience Manager6.5.5)或更早版本中的Dynamic Media。<br>如果您在Experience Manager6.5、Service Pack 6 (Experience Manager6.5.6)或更高版本中使用Dynamic Media，请按照[通过Dynamic Media使CDN缓存失效](/help/assets/invalidate-cdn-cache-dynamic-media.md)中提供的步骤操作。

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**通过Dynamic Media Classic使CDN缓存失效：**

1. 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=zh-Hans#system-requirements-dmc-app)，然后登录到您的帐户。

   在设置时，Adobe提供了您的凭据和登录。 如果您没有此信息，请联系Adobe客户支持。

1. 在页面的右上角附近，导航到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**。
1. 在“应用程序常规设置”页面的“服务器”组标题下，找到&#x200B;**[!UICONTROL CDN失效模板]**&#x200B;文本框。

1. 指定用于使CDN（内容分发网络）缓存失效的模板。

   例如，假设您输入引用`<ID>`的图像URL（包括图像预设或修饰符），而不是如下例所示输入特定的图像ID：

   `https://server.com/is/image/Company/<ID>?$product$`

   如果模板仅包含`<ID>`，则Dynamic Media将填充`https://<server>/is/image`，其中`<server>`是在“常规设置”中定义的Publish服务器名称，&lt;ID>是选定要失效的资源。

1. 在页面的右下角，选择&#x200B;**[!UICONTROL 关闭]**。
1. 在Dynamic Media Classic用户界面中，选择一个或多个资源，然后转到&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 使CDN失效]**。 您将看到一个列表，其中包含从您创建的模板和您选择的资源生成的一个或多个URL。 它使用“应用程序常规设置”下“已发布的服务器名称”下列出的服务器URL。

   例如，在上一步中设置CDN失效模板，假设您选择了名为`Backpack_B`的单个图像资产图像。 当您转到&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 使CDN无效]**&#x200B;时，它将导致在CDN无效用户界面中生成以下的URL：

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 在URL列表框中，选择&#x200B;**[!UICONTROL 继续]**&#x200B;以清除每个特定URL的缓存。 您可以编辑URL，也可以通过键入或粘贴到URL列表框来添加URL；您无需事先设置CDN失效模板。

   选择&#x200B;**[!UICONTROL 继续]**&#x200B;后，将显示一个指示器，为您提供清除缓存所需的估计时间。

   如果您选择了多个资产，然后转到&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 使CDN无效]**，则每个资产都会在保存的&#x200B;**[!UICONTROL 模板URL]**&#x200B;中引用。 因此，您可以定义&#x200B;**[!UICONTROL CDN无效模板]**，以引用网站上引用的每个URL图像预设（如产品详细信息和搜索结果）。 然后，当您从缓存中选择一个或多个要失效的图像时，URL 会自动填充该界面。

   >[!NOTE]
   >
   >当您选择资源，然后转到&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 使CDN无效]**&#x200B;时，Dynamic Media会使用无效CDN模板从内容交付网络(CDN)自动创建要无效的URL。 如果 **[!UICONTROL CDN 无效模板]**&#x200B;文本框中没有任何内容，则会显示空白 URL 列表。CDN 上的缓存不是基于资产，而是基于 URL。因此，必须了解您网站上的完整 URL。确定这些 URL 后，可以将其添加到步骤前面的&#x200B;**[!UICONTROL 无效 CDN 模板]**。然后，您可以选择这些资产，并在一个步骤中使 URL 失效。
   >
   >另一个选项是将完整的URL添加到&#x200B;**[!UICONTROL 使CDN]**&#x200B;无效。 如果遵循这种方法，则无需在转到&#x200B;**[!UICONTROL 文件>使CDN无效]**&#x200B;选项之前在Dynamic Media Classic中选择资源。
