---
title: AEM Adobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: AEM与PhoneGap集成，以便您能够使用AEM页面轻松创建应用程序。 请阅读本页，以开始使用Adobe PhoneGap Enterprise。
seo-description: AEM integrates with PhoneGap so that you can easily create apps using AEM pages. Follow this page to get started with Adobe PhoneGap Enterprise.
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

AEM与PhoneGap集成，以便您能够使用AEM页面轻松创建应用程序。 PhoneGap允许用户创建实用工具应用程序，以便用户处理内容。 通过内容同步，您可以创建页面的版本控制存档以与应用程序捆绑在一起。

通常， ***AEM管理员*** 负责通过使用创建向导创建新应用程序或导入现有应用程序，将新应用程序添加到AEM Mobile目录。

从此处 ***AEM作者*** (或 *营销人员*)现在可以使用现成的模板和组件来添加和编辑页面、拖放组件以及添加DAM中所有类型的媒体，包括图像、视频和文本片段（内容片段）。

AEM Mobile的真正力量是 *精明* ***AEM开发人员*** 可以扩展和创建自定义web模板和组件，以启用 *AEM作者* 以创建美妙而引人入胜的移动体验。 这些模板和组件不仅针对移动设备应用程序领域进行了优化；但是，要与设备和AEM服务器（任何远程服务器）通信到全渠道服务端点。

>[!NOTE]
>
>当 *AEM作者* 相信应用程序已准备就绪，他们可以先让利益相关方通过 **[Adobe验证](/help/mobile/phonegap-mobile-quickstart.md)** （可在AppStore和PlayStore中使用）以供审核和批准。 他们收到绿灯后，便能够通过AEM Mobile ContentSync内容发布管理功能板，直接向用户发布此新内容或更新内容。 一个人可以承担任何数量的角色，这取决于您和您的治理政策。

## 前提条件 {#prerequisites}

AEM Mobile只是构成完整AEM平台的一个支柱。

在使用AEM Mobile并执行本快速入门指南中的步骤之前，用户应该熟悉AEM和AEM Mobile控制中心。 请参阅：

[AEM 快速入门](/help/sites-deploying/deploy.md)

[AEM Mobile管制中心的演练](/help/mobile/phonegap-authoring-apps.md)

## 适用于作者的快速链接 {#quicklinks-for-authors}

请参阅 [在AEM中为Adobe PhoneGap企业版创作](/help/mobile/phonegap.md) 了解作者的角色和职责。

## 面向开发人员的QuickLinks {#quicklinks-for-developers}

有一些示例应用程序将与AEM Mobile集成，并且可由开发人员自定义。 单击 [使用AEM开发Adobe PhoneGap企业](/help/mobile/developing-in-phonegap.md).

在后续的章节中，您将学习一些高级概念，如为您的应用程序设置白色标签、本地化、国际化、内容同步、定位、分析等。

## 面向管理员的快速链接 {#quicklinks-for-administrators}

请参阅 [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md) 来设置和管理移动应用程序。

>[!NOTE]
>
>使用混合移动技术，您可以创建丰富的移动应用程序， *脱机运行和联机运行* 事实上，使用AEM Mobile，许多客户会选择创建一些应用程序，以检查他们在线或离线的时间并据此行事。
