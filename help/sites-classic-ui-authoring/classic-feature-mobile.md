---
title: 为移动设备创作页面
description: 在创作移动页面时，页面会以模拟移动设备的方式显示。在创作页面时，您可以在多个模拟器之间切换，以查看最终用户在访问页面时看到的内容。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 52%

---

# 创作适用于移动设备的页面{#authoring-a-page-for-mobile-devices}

在创作移动页面时，页面会以模拟移动设备的方式显示。在创作页面时，您可以在多个模拟器之间切换，以查看最终用户在访问页面时看到的内容。

根据设备呈现页面的功能，设备分为功能、智能和触控三个类别。当最终用户访问移动页面时，AEM 会检测设备并发送与其设备组对应的演绎版。

>[!NOTE]
>
>要创建基于现有标准站点的移动站点，请创建标准站点的 Live Copy。(请参阅 [为不同渠道创建Live Copy](/help/sites-administering/msm-livecopy.md).)
>
>AEM 开发人员可以创建新设备组。(请参阅 [正在创建设备组筛选器。](/help/sites-developing/groupfilters.md))

请使用以下过程来创作移动页面：

1. 在浏览器中，转到 **Siteadmin** 控制台。
1. 打开 **产品** 页面如下 **网站** >> **GeometrixxMobile演示站点** >> **英语**.

1. 切换到其他模拟器。 为此，您可以：

   * 单击页面顶部的设备图标。
   * 单击 **编辑** 中的按钮 **Sidekick** ，然后在下拉菜单中选择设备。

1. 拖放 **文本和图像** 组件从页面的“移动”选项卡移至Sidekick。
1. 编辑组件并添加一些文本。 单击 **确定** 以保存更改。

该页面看起来与以下内容相同：

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>从移动设备请求创作实例上的页面时，将禁用模拟器。 然后，可以使用支持触摸的UI进行创作。
