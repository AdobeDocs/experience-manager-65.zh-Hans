---
title: 创建和管理应用程序内容
description: 管理应用程序内容需要开发人员、内容作者和管理员共同努力。 作者处理基于模板和应用程序开发人员生成的组件的页面。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 9d350935-129a-40d3-89f4-2e6f69676e5e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# 创建和管理应用程序内容{#creating-and-managing-app-content}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

管理应用程序内容需要来自的集体努力 [开发人员](#developer)，内容 [作者](#author)、和 [管理员](#administrator). 作者处理基于模板和应用程序开发人员生成的组件的页面。

最后，管理员策略性地发布更新的应用程序内容。

>[!NOTE]
>
>**先决条件**：
>
>在 [部署和维护](/help/sites-deploying/deploy.md)、开发人员熟悉Adobe Experience Manager (AEM)中的系统组件和模板。

## “管理页面内容”拼贴 {#the-manage-page-content-tile}

>[!CAUTION]
>
>如果您没有使用现成的应用程序模板，则要启用要通过OTA发布的新应用程序内容，必须配置内容同步处理程序。
>
>请参阅 [通过内容同步处理移动设备](/help/mobile/phonegap-contentsync.md) 有关详细信息，请参阅开发人员部分。

在这里，可以像在AEM Sites中一样在AEM Mobile中创建、编辑和删除内容。

此 **“管理页面内容”拼贴** 显示托管内容的页数以及上次为特定有效负载修改的页数。 您可以通过单击图块中的每个记录，深入查看内容以创建、复制、移动、删除和更新页面。

内容更新后，管理员可以通过向客户发布内容更新有效负荷Over-The-Air (OTA) **“管理内容包”图块。**

![chlimage_1-161](assets/chlimage_1-161.png)

选择列出的内容包之一以创建或编辑内容，如创建、编辑或删除页面，更改导航和页面顺序，创建或更新内容，如复制（文本）和媒体。

注意 *一切都是内容*，这意味着应用程序样式、复制（文本）、媒体、页面、导航和内容定位都可以在OTA中编辑和更新，而无需前往应用商店。

要编辑AEM Mobile内容，*AEM作者*需要对AEM内容编辑界面有一定的了解： [在AEM中创作页面。](/help/sites-authoring/qg-page-authoring.md)

## “管理内容包”图块 {#the-manage-content-packages-tile}

此处， *AEM管理员* 可以快速轻松地更新其应用程序以提供引人入胜的体验和最新内容，从而推动品牌参与度并实现业务目标，而无需重新提交开发人员或应用商店。

![chlimage_1-162](assets/chlimage_1-162.png)

一次 *AEM作者* 通过“管理内容”拼贴添加或修改了内容， *AEM管理员* 能够通过内容包更新将这些更改推送到客户。

内容包操作允许 *AEM创作* 在开发团队更改主机应用程序设计和实施（包括导航、样式、服务器端逻辑、模板和组件）的同时创建和编辑页面内容，然后将这些更改从OTA推送给客户，而无需重新提交到各个商店进行分发。

**发布新内容或更新内容**

从图块中选择一个内容包，在本例中是英文包。 请注意，内容更新对话框将列出相关的 *内容同步* 配置。 如果自上次更新以来已修改应用程序内容，则将显示状态 *待处理*，如下所示。

![chlimage_1-163](assets/chlimage_1-163.png)

接下来，选择 **Stage** 操作。 添加相应的更新信息，然后按“完成”。

![chlimage_1-164](assets/chlimage_1-164.png)

此 *内容同步* 然后，处理程序通过形成delta(包 *仅限* 更改了哪些内容)。 完成后，此更新内容包已暂存，如下所示。

对内容进行暂存更新允许在将内容发布到OTA到移动设备之前进行多项更新。

>[!NOTE]
>
>暂存内容可在发布之前使用AEM Verify应用程序进行验证。
>
>请参阅 [适用于AEM的Mobile Quickstart验证](/help/mobile/phonegap-mobile-quickstart.md) 有关AEM Verify应用程序的更多详细信息。

![chlimage_1-165](assets/chlimage_1-165.png)

准备好通过Content Sync OTA向应用程序用户提供新内容时，请选择 **Publish** 如下所示。

![chlimage_1-166](assets/chlimage_1-166.png)

### 后续步骤 {#the-next-steps}

了解如何在应用程序功能板中创建和管理应用程序内容后，请参阅以下资源以了解其他创作角色：

* [“管理应用程序”拼贴](/help/mobile/phonegap-app-details-tile.md)
* [编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md)
* [应用程序定义](/help/mobile/phonegap-app-definitions.md)
* [使用创建应用程序向导创建新应用程序](/help/mobile/phonegap-create-new-app.md)
* [导入现有的混合应用程序](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM开发Adobe PhoneGap Enterprise](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
