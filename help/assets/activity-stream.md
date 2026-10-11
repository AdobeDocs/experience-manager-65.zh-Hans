---
title: 时间轴视图中数字资产的活动流
description: 本文介绍了如何在时间轴上显示资产的活动日志。
contentOwner: AG
feature: Asset Management
role: User, Admin
exl-id: 28dc0aa5-f2be-4e27-b7d8-415569b7ecd4
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 26%
---
# 时间线中的活动流 {#activity-stream-in-timeline}

此功能在时间轴上显示资源的活动日志。 如果在[!DNL Adobe Experience Manager Assets]中执行以下任何与资产相关的操作，则活动流功能会更新时间线以反映该活动。

以下操作记录在活动流中：

* 创建
* 删除
* 下载（包括演绎版）
* 发布
* 取消发布
* 批准
* 拒绝
* 移动

时间轴中显示的活动日志是从 CRX 中的 `/var/audit/com.day.cq.dam/content/dam` 位置获取的，日志文件就存储在该位置。 此外，当上传新资产或通过[Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html)或[Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html)修改现有资产并签入[!DNL Experience Manager]时，将记录时间轴活动。

>[!NOTE]
>
>临时工作流不会显示在时间轴中，因为不会保存这些工作流的历史记录信息。

要查看活动流，请对资产执行一个或多个操作，选择资产，然后从GlobalNav列表中选择&#x200B;**[!UICONTROL 时间轴]**。

![时间线–2](assets/timeline-2.png)

时间轴显示您对资产执行的操作的活动流。

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>**[!UICONTROL 发布]**&#x200B;和&#x200B;**[!UICONTROL 取消发布]**&#x200B;任务的默认日志存储位置为 `/var/audit/com.day.cq.replication/content`。 对于&#x200B;**[!UICONTROL 移动]**&#x200B;任务，默认位置为 `/var/audit/com.day.cq.wcm.core.page`。
