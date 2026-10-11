---
title: 为移动设备创作页面
description: 在创作移动页面时，页面会以模拟移动设备的方式显示。 在创作页面时，您可以在多个模拟器之间切换，以查看最终用户在访问页面时看到的内容。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 58%
---
# 创作适用于移动设备的页面{#authoring-a-page-for-mobile-devices}

在创作移动页面时，页面会以模拟移动设备的方式显示。 在创作页面时，您可以在多个模拟器之间切换，以查看最终用户在访问页面时看到的内容。

根据设备呈现页面的功能，设备分为功能、智能和触控三个类别。 当最终用户访问移动页面时，AEM 会检测设备并发送与其设备组对应的演绎版。

>[!NOTE]
>
>要创建基于现有标准站点的移动站点，请创建标准站点的 Live Copy。 （请参阅[为不同的渠道创建Live Copy](/help/sites-administering/msm-livecopy.md)。）
>
>AEM 开发人员可以创建新设备组。 （请参阅[创建设备组筛选器。](/help/sites-developing/groupfilters.md)）

请使用以下过程来创作移动页面：

1. 在浏览器中，转到&#x200B;**Siteadmin**&#x200B;控制台。
1. 打开&#x200B;**网站** >> **Geometrixx Mobile演示站点** >> **英语**&#x200B;下的&#x200B;**产品**&#x200B;页面。

1. 切换到其他模拟器。 为此，您可以：

   * 单击页面顶部的设备图标。
   * 单击&#x200B;**Sidekick**&#x200B;中的&#x200B;**编辑**&#x200B;按钮，然后在下拉菜单中选择设备。

1. 将&#x200B;**文本和图像**&#x200B;组件从Sidekick的“移动设备”选项卡拖放到页面上。
1. 编辑组件并添加一些文本。 单击&#x200B;**确定**&#x200B;以保存更改。

该页面看起来与以下内容相同：

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>从移动设备中请求创作实例上的页面时，会禁用模拟器。 然后，可以使用支持触摸的UI进行创作。
