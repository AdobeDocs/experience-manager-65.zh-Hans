---
title: 构建应用程序
description: 关注此页面，了解如何创建应用程序的结构。 本页介绍如何构建模板和组件以及有关JavaScript和CSS Clientlibs的信息。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 0%

---

# 构建应用程序{#structure-an-app}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

AEM Mobile项目涉及多种内容类型，包括页面、JavaScript和CSS客户端库、可重用的AEM组件、Content Sync配置和PhoneGap应用程序外壳内容。 基于[Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit)构建新的AEM Mobile应用程序是一种好方法，可以将所有不同类型的内容纳入我们推荐的结构，从而长期简化可移植性和可维护性。

## 页面内容 {#page-content}

应用程序页面都应位于/content/mobileapps下方，以便AEM Mobile控制台识别这些页面。

![chlimage_1-52](assets/chlimage_1-52.png)

根据AEM约定，应用程序的第一个页面应该是重定向到充当应用程序的默认语言的子页面之一(在Geometrixx和入门套件用例中均为“en”)。 顶级区域设置页面通常继承自foundation“splash-page”组件(/libs/mobileapps/components/splash-page)，该组件会进行支持安装无线内容同步更新所需的初始化(contentInit代码位于/etc/clientlibs/mobile/content-sync/js/contentInit.js)。

## 模板和组件 {#templates-and-components}

您应用程序的模板和组件代码应位于/apps/&lt;brand name>/&lt;app name>中。 应按照惯例将模板和组件代码放置在/apps/&lt;brand name>/&lt;app name>中。 已使用AEM中的站点的开发人员应该熟悉此模式。 通常，在发布实例上，默认情况下会将/apps/锁定为匿名访问。 因此，您的原始JSP代码会向潜在攻击者隐藏。

可以将特定于应用程序的模板配置为仅通过使用模板本身上的`allowedPaths`属性节点并将其值设置为“/content/mobileapps(/”来显示。&amp;amp；ast；)？&#39;  — 甚至某些更具体的设置，前提是模板只能用于单个应用程序。 `allowedParents`和`allowedChildren`属性还可用于根据创建新页面的位置对作者可用的模板进行细粒度控制。

从头开始创建应用程序页面组件时，建议将其`sling:resourceSuperType`属性设置为“mobileapps/components/angular/ng-page”。 这会将您的页面设置为创作和呈现为单页应用程序，并使您可以叠加组件可能需要更改的任何.jsp文件。 由于ng-page根本不包含任何UI框架，因此开发人员通常最终会叠加（至少）“template.jsp”(覆盖自/libs/mobileapps/components/angular/ng-page/template.jsp)。

希望使用AngularJS的可创作页面组件在/libs/mobileapps/components/analytics/ng-component具有等效的`sling:resourceSuperType`组件，可以通过相同的方式叠加和自定义angular组件。

## JavaScript和CSS Clientlibs {#javascript-and-css-clientlibs}

在客户端库中，对于将它们放置在存储库中的位置，开发人员有几个选项可供使用。 提供以下模式作为指导，但并非硬性要求。

如果您的客户端代码可以独立存在，并且与应用程序的特定组件无关（这意味着它可以在其他应用程序中重复使用），则Adobe建议将其存储在/etc/clientlibs/&lt;brand name>/&lt;lib name>中。 另一方面，如果clientlib特定于单个应用程序，则可以将其嵌套为应用程序设计节点（ /etc/designs/phonegap/&lt;品牌名称>/&lt;应用程序名称>/clientlibs）的子节点。 请勿将此clientlib的类别与其他库一起使用；而是根据需要嵌入其他库。 通过遵循此模式，开发人员无需每次将客户端库添加到应用程序时都添加新的内容同步配置，而只需更新应用程序设计clientlib的“embeds”属性。 例如，查看/content/phonegap/geometrixx-outdoors/en/jcr：content/pge-app/app-config/clientlibs-all中的clientlibs-all Content SyncGeometrixx。

如果您的客户端代码与特定组件紧密耦合，请将该代码放置在嵌套在/apps/中组件位置下方的客户端库中，并将其类别嵌入应用程序的“设计”clientlib。

## PhoneGap配置 {#phonegap-configuration}

每个AEM Mobile应用程序都包含一个目录，其中托管了PhoneGap [命令行界面](https://github.com/phonegap/phonegap-cli)和`https://build.phonegap.com/`上的PhoneGap Build所使用的配置文件，以便将Web内容转换为可运行的应用程序。 例如，在此Geometrixx示例中，此目录(/content/phonegap/geometrixx-outdoors/shell/jcr：content/pge-app/app-content)作为Shell的一部分而存在；作出了设计决策，因为该目录仅包含无法无线更新的内容，例如处理设备API和应用程序本身配置的插件。

在此目录中，您还找到一些[Cordova挂接](https://cordova.apache.org/docs/en/dev/guide/appdev/hooks/index.html#Hooks%20Guide)，它们可用于安装插件、将资源文件放置在其平台特定的位置，以及应在生成过程中执行的其他操作。 注意：除了在生成过程中下载每个插件外，您还可以遵循厨房接收器应用程序的模式，并将插件源代码<!-- THIS URL IS 404 (https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) -->与应用程序项目的其余部分一起下载。

## 后续步骤 {#the-next-steps}

了解应用程序的结构后，请参阅[使用应用程序控制台创建和编辑应用程序](/help/mobile/phonegap-apps-console.md)。
