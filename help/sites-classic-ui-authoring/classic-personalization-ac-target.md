---
title: 定位您的 Adobe Campaign
seo-title: Targeting your Adobe Campaign
description: 设置分段包括创建区段、品牌、营销活动和体验。
seo-description: Setting up segmentation includes creating segments, a brand, campaign, and experiences.
uuid: 520cd006-0aa8-43f3-b754-efb7397bb92f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bbc2aac9-ccf1-40c3-be4f-d59c2d0d8a6c
exl-id: e56986b2-397e-4802-992b-05a9ea7b2e36
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 74%

---

# 定位您的 Adobe Campaign{#targeting-your-adobe-campaign}

要定位您的 Adobe Campaign 新闻稿，您需要先设置分段，分段仅在经典 UI 中可用。之后，您可以为 Adobe Campaign 创建目标体验。

## 在 AEM 中设置分段 {#setting-up-segmentation-in-aem}

设置分段包括创建区段、品牌、营销活动和体验。您只能在经典 UI 中创建区段。您可以在触屏UI中创建品牌、营销活动和体验。

>[!NOTE]
>
>需要将区段 ID 映射到 Adobe Campaign 端的区段 ID。

### 创建区段 {#creating-segments}

要创建区段，请执行以下操作：

1. 打开 [分段控制台](http://localhost:4502/miscadmin#/etc/segmentation) at **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. 创建新页面并输入标题 — 例如， **交流区段**  — 并选择 **区段(Adobe Campaign)** 模板。
1. 在左侧的树视图中选择已创建的页面。
1. 创建一个区段（例如定位男性用户），方法是在您创建的名为“Male”的区段下创建一个新页面，然后选择&#x200B;**区段 (Adobe Campaign)** 模板。
1. 打开创建的区段页面，然后将&#x200B;**区段 ID** 从 Sidekick 拖放到该页面上。
1. 双击该特征，输入表示在此示例中定义的男性区段的ID — 例如， **男**  — 单击 **确定**. 应会显示以下消息： `targetData.segmentCode == "MALE"`
1. 重复执行这些步骤以创建另一个区段，例如，定位女性用户的区段。

### 创建品牌 {#creating-a-brand}

要创建品牌，请执行以下操作：

1. 在&#x200B;**站点**&#x200B;中，导航到&#x200B;**营销活动**&#x200B;文件夹（例如，在 We.Retail 中）。
1. 单击&#x200B;**创建页面**&#x200B;并输入页面标题（例如 We.Retail Brand），然后选择&#x200B;**品牌**&#x200B;模板。

### 创建活动 {#creating-a-campaign}

要创建营销活动，请执行以下操作：

1. 打开刚刚创建的&#x200B;**品牌**&#x200B;页面。
1. 单击&#x200B;**创建页面**&#x200B;并输入页面标题（例如 We.Retail Campaign），然后选择&#x200B;**营销活动**&#x200B;模板并单击&#x200B;**创建**。

### 创建体验 {#creating-experiences}

要为区段创建体验，请执行以下操作：

1. 打开刚刚创建的&#x200B;**营销活动**&#x200B;页面。
1. 通过单击 **创建页面** 并为页面输入标题（例如，当您为“男性”区段创建体验时），然后选择 **体验** 模板。
1. 打开创建的体验页面。
1. 单击&#x200B;**编辑**，然后单击“区段”下的&#x200B;**添加项目**。
1. 例如，输入男区段的路径 `/etc/segmentation/ac-segments/male` 单击 **确定**. 应会显示以下消息： *体验的目标：男*
1. 重复执行上述步骤以便为所有区段都创建体验，例如针对女性目标。

## 创建包含目标内容的新闻稿 {#creating-a-newsletter-with-targeted-content}

创建区段、品牌、营销活动和体验后，您可以创建包含目标内容的新闻稿。创建体验后，您可以将体验与区段相关联。

您可以在启用了触屏操作的用户界面和经典用户界面中创建包含目标内容的新闻稿。 本文档介绍了触屏UI的操作过程。

要创建包含目标内容的新闻稿，请执行以下操作：

1. 创建包含目标内容的新闻稿：在Geometrixx Outdoors中的“电子邮件促销活动”下方，单击或点按 **创建** > **页面**，然后选择其中一个Adobe Campaign邮件模板。

   >[!NOTE]
   >
   >[仅 Geometrixx 中提供了电子邮件示例](/help/sites-developing/we-retail.md#weretail)。请从“包共享”中下载 Geometrixx 示例内容。

1. 在新闻稿中，添加一个“文本与个性化”组件。
1. 在该“文本与个性化”组件中添加文本，例如“This is the default”。
1. 单击旁边的箭头 **编辑** 选择 **定位**.
1. 从“品牌”下拉菜单中选择您的品牌，然后选择您的营销活动。（这是您之前创建的品牌和营销活动）。
1. 单击&#x200B;**开始定位**。您会看到您的区段显示在“受众”区域中。如果已定义的区段都不匹配，则会使用默认体验。

   >[!NOTE]
   >
   >默认情况下，AEM 附带的电子邮件示例使用 Adobe Campaign 作为定位引擎。对于自定义新闻稿，您可能需要选择 Adobe Campaign 作为定位引擎。定位时，请点按或单击工具栏中的“+”，为新活动输入标题，然后选择 **Adobe Campaign** 作为定位引擎。

1. 单击&#x200B;**默认**，然后单击您添加的“文本与个性化”组件，此时您会看到带有箭头的靶心图标。单击该图标以定位此组件。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 导航到另一个区段 (Male)，单击&#x200B;**添加选件**，然后单击加号图标 (+)。接着，编辑该选件。
1. 导航到另一个区段 (Female)，单击&#x200B;**添加选件**，然后单击加号图标 (+)。接着，编辑该选件。
1. 单击 **下一个** 要查看映射，请单击 **下一个** 要查看不适用于Adobe Campaign的设置，请单击 **保存**.

   当 Adobe Campaign 中的分发使用内容时，AEM 会自动为 Adobe Campaign 生成正确的定位代码。

1. 在 Adobe Campaign 中，创建您的分发 - 选择&#x200B;**使用 AEM 内容的电子邮件分发**，然后根据需要选择本地 AEM 帐户并确认您的更改。

   在 HTML 视图中，目标组件的不同体验会包含在 Adobe Campaign 定位代码中。

   ![chlimage_1-166](assets/chlimage_1-166.png)

   >[!NOTE]
   >
   >如果您也在 Adobe Campaign 中设置了区段，则单击&#x200B;**预览**&#x200B;会显示每个区段的体验。
