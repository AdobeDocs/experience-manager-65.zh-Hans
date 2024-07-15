---
title: 将 [!DNL Assets] 与活动流集成
description: 描述 [!DNL Experience Manager] 的记录功能以及如何将其配置为记录特定事件。
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# 将[!DNL Assets]与活动流集成 {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets]用户可执行许多操作，如创建、上传和删除Assets。 可以记录这些操作，以便您能够提供用户所做操作的历史记录。 本节介绍[!DNL Experience Manager]的记录功能以及如何配置[!DNL Experience Manager]以记录特定事件。

## 性能注意事项和默认行为 {#performance-considerations-and-default-behavior}

例如，在执行批量导入时，这种集成可能会耗用CPU和磁盘空间。 出于这些原因，默认情况下将禁用与活动流的[!DNL Assets]集成。

## 支持的操作事件 {#supported-action-events}

您可以配置要记录的以下事件：

* 许可证已接受（已接受）
* 已创建资产(ASSET_CREATED)
* 已移动资产(ASSET_MOVED)
* 已删除资产(ASSET_REMOVED)
* 许可证被拒绝（已拒绝）
* 已下载（已下载）资产
* 资产版本化（版本化）
* 已恢复资产版本（已恢复）
* 已更新资产元数据(METADATA_UPDATED)
* 资产已发布到外部系统(PUBLISHED_EXTERNAL)
* 资产的原始更新（原始更新）
* 已更新资产演绎版(RENDITION_UPDATED)
* 已删除资源呈现版本(RENDITION_REMOVED)
* 已更新子资产(SUBASSET_UPDATED)
* 已删除子资产(SUBASSET_REMOVED)

## 配置[!DNL Assets]事件记录 {#configuring-aem-assets-events-recording}

[Web控制台](/help/sites-deploying/configuring-osgi.md)提供对Assets事件记录器调整的访问权限。 要配置Assets事件记录器，请按照以下步骤操作：

1. 导航到&#x200B;**[!UICONTROL Web控制台]**

1. 单击&#x200B;**[!UICONTROL 配置]**。

1. 双击&#x200B;**[!UICONTROL Day CQ DAM事件记录器]**。

1. 选中&#x200B;**[!UICONTROL 启用此服务]**。

1. 检查您希望在用户活动流中记录哪些&#x200B;**[!UICONTROL 事件类型]**。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 读取录制的事件 {#reading-recorded-events}

记录的事件将作为活动存储。 您可以使用[ActivityManager API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)以编程方式读取它们。
