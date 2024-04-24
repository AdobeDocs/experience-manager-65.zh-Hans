---
title: 访问设备功能
description: 按照本页了解如何构建可访问设备功能的Adobe Experience Manager (AEM)组件。 AEM PhoneGap Kitchen Sink GitHub存储库为开发人员提供了一个功能强大的AEM应用程序，该应用程序展示了几个核心Cordova API的使用。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 385f7924-e8ab-4dcb-83f0-7b81bead3dda
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# 访问设备功能{#access-device-features}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

## 构建访问设备功能的Adobe Experience Manager (AEM)组件 {#building-aem-components-that-access-device-features}

此 [AEM PhoneGap厨房水槽](https://github.com/blefebvre/aem-phonegap-kitchen-sink) GitHub存储库为开发人员提供了一个功能强大的AEM应用程序，该应用程序展示了几个核心Cordova API的使用。 在通过PhoneGap CLI在iOS或Android™上运行时，该应用程序会打开到以下页面，其中包括到它演示的每个设备API的链接：

![chlimage_1-107](assets/chlimage_1-107.png)

每个设备API组件的源代码都是 [在GitHub上可用](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/apps/brucelefebvre/kitchen-sink/components).

有关每个API用法的更多详细信息，请参阅Cordova插件文档(`https://docs.phonegap.com/en/4.0.0/cordova_plugins_pluginapis.md.html`)。

## 后续步骤 {#the-next-steps}

请参阅 [使用AdobeMobile Analytics跟踪应用程序性能](/help/mobile/phonegap-intro-to-app-analytics.md).
