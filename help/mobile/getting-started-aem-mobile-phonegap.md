---
title: AEM Adobe PhoneGap
description: AEM与PhoneGap集成，因此您可以使用AEM页面轻松创建应用程序。 关注本页，以开始使用Adobe PhoneGap Enterprise。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

AEM与PhoneGap集成，因此您可以使用AEM页面轻松创建应用程序。 PhoneGap允许用户创建实用工具应用程序，以便用户处理内容。 内容同步允许您创建页面的版本化存档，以便与应用程序捆绑在一起。

通常，***AEM管理员***&#x200B;负责通过使用创建向导创建应用程序或导入现有应用程序来向AEM Mobile目录添加新应用程序。

从此处，***AEM作者***（或&#x200B;*营销人员*）现在可以使用现成的模板和组件从DAM添加和编辑页面、拖放组件以及添加所有类型的媒体，包括图像、视频和文本片段（内容片段）。

AEM Mobile的真正优势在于&#x200B;*精通* ***AEM Developer***&#x200B;可以扩展和创建自定义Web模板和组件，以使&#x200B;*AEM Author*&#x200B;能够创建美观且引人入胜的移动体验。 这些模板和组件不仅针对移动应用程序世界进行了优化，而且还与设备和AEM服务器（任何远程服务器）进行通信以连接全通道服务端点。

>[!NOTE]
>
>当&#x200B;*AEM作者*&#x200B;认为应用程序已就绪时，他们可以首先让利益相关者下载包含&#x200B;**[Adobe验证](/help/mobile/phonegap-mobile-quickstart.md)**&#x200B;的应用程序（在AppStore和PlayStore中均可用）以供审阅和批准。 收到绿灯后，他们可以通过AEM Mobile ContentSync内容发布管理功能板，直接向其用户发布这些新的或更新后的内容。 一个人可以担任任意数量的角色，具体取决于您和您的治理策略。

## 先决条件 {#prerequisites}

AEM Mobile只是构成整个AEM平台的支柱之一。

在使用AEM Mobile并按照本快速入门指南中的步骤操作之前，用户应该熟悉AEM和AEM Mobile控制中心。 请参阅：

[AEM快速入门](/help/sites-deploying/deploy.md)

[AEM Mobile控制中心演练](/help/mobile/phonegap-authoring-apps.md)

## 作者的快速链接 {#quicklinks-for-authors}

请参阅[在AEM中为Adobe PhoneGap Enterprise创作](/help/mobile/phonegap.md)，以了解作者的角色和职责。

## 面向开发人员的快速链接 {#quicklinks-for-developers}

有一些示例应用程序将与AEM Mobile集成并可由开发人员进行自定义。 单击[使用AEM](/help/mobile/developing-in-phonegap.md)开发Adobe PhoneGap Enterprise。

在后续章节中，您将了解高级概念，如白色标签设置、应用程序、本地化、国际化、内容同步、定位、分析等。

## 管理员快速链接 {#quicklinks-for-administrators}

请参阅[使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)，以设置和管理您的移动应用程序。

>[!NOTE]
>
>使用混合移动技术，您可以创建丰富的移动应用程序，这些应用程序通过AEM Mobile *离线和在线运行*，实际上，许多客户选择创建这样的应用程序：检查他们在在线或离线时的状态，并相应地执行操作。
