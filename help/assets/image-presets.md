---
title: 应用 Dynamic Media 图像预设
description: 了解如何在Dynamic Media中应用图像预设
uuid: 8bafcbd0-6df0-4d5b-b2f7-116ddb4ec060
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5c1f60ac-3741-4002-9c5d-c128f118342b
feature: Image Presets
role: User,Admin
exl-id: 98d88b59-eb8f-42db-abb8-04506a5b8c30
source-git-commit: 4b8369de9e6a10b73115d53358ce98729d92ed44
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 33%

---

# 应用Dynamic Media图像预设 {#applying-image-presets}

图像预设使资产能够动态地传送不同大小、不同格式或具有其他动态生成的图像属性的图像。在导出图像时，您可以选择预设。 预设会按照管理员指定的规范重新设置图像的格式。

此外，您可以选择响应式图像预设（选择图像预设后，通过 **[!UICONTROL RESS]** 按钮指定）。

本节介绍如何使用图像预设。[管理员可以创建并配置图像预设](managing-image-presets.md)。

>[!NOTE]
>
>智能成像可与您现有的图像预设配合使用，并在交付的最后一毫秒内使用智能功能，根据浏览器或网络连接速度进一步减小图像文件大小。 请参阅 [智能成像](imaging-faq.md) 以了解更多信息。

无论您何时预览图像，都可以对图像应用图像预设。

>[!NOTE]
>
>在Dynamic Media - Scene7模式下，图像预设仅受图像资产支持。

**要应用Dynamic Media图像预设，请执行以下操作：**

1. 打开资产，在左边栏中，选择下拉菜单，然后选择 **[!UICONTROL 演绎版]**.

   >[!NOTE]
   >
   >* 静态演绎版显示在窗格的上半部分。 动态演绎版显示在下半部分。您只能对动态演绎版使用 URL 来显示图像。**[!UICONTROL URL]** 按钮仅在选择动态演绎版的情况下才会显示。而 **[!UICONTROL RESS]** 按钮则仅在选择响应式图像预设的情况下才会显示。
   >
   >* 当您选择 **[!UICONTROL 演绎版]** 的“详细信息”视图。 您可以增加可查看的预设数。请参阅 [增加显示的图像预设数](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).


   ![chlimage_1-208](assets/chlimage_1-208.png)

1. 执行以下操作之一：

   * 选择动态演绎版，以便预览图像预设。
   * 要显示弹出窗口，请选择 **[!UICONTROL URL]**, **[!UICONTROL 嵌入]**&#x200B;或 **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >如果资产 *和* 图像预设尚未发布， **[!UICONTROL URL]** 按钮（或） **[!UICONTROL URL]** 和 **[!UICONTROL RESS]** 按钮（如果适用）不可用。
   >
   >另请注意，图像预设会自动发布在Dynamic Media服务器上。
