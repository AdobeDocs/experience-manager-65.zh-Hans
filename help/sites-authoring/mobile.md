---
title: 为移动设备创作内容页面
description: 为移动设备创作时，您可以在多个模拟器之间切换，以查看最终用户看到的内容。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 9c6c6386-5ffd-4fa6-9aa1-f5b0e31d1046
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 63%
---
# 创作适用于移动设备的页面{#authoring-a-page-for-mobile-devices}

在创作移动页面时，页面会以模拟移动设备的方式显示。 在创作页面时，您可以在多个模拟器之间切换，以查看最终用户在访问页面时看到的内容。

根据设备呈现页面的功能，设备分为功能、智能和触控三个类别。 当最终用户访问移动页面时，AEM 会检测设备并发送与其设备组对应的演绎版。

>[!NOTE]
>
>要创建基于现有标准站点的移动站点，请创建标准站点的 Live Copy。 （请参阅[为不同的渠道创建Live Copy](/help/sites-administering/msm-livecopy.md)。）
>
>AEM 开发人员可以创建新设备组。 （请参阅[创建设备组筛选器](/help/sites-developing/groupfilters.md)。）

请使用以下过程来创作移动页面：

1. 从全局导航中打开&#x200B;**Sites**&#x200B;控制台。
1. 打开页面&#x200B;**We.Retail** > **美国** > **英语**。

1. 切换到&#x200B;**预览**&#x200B;模式。
1. 单击页面顶部的设备图标以切换到所需的模拟器。
1. 将组件从组件浏览器拖放到页面。

该页面类似于以下内容：

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>从移动设备中请求创作实例上的页面时，会禁用模拟器。
