---
title: 定位您的Adobe Campaign
description: 设置分段后，您可以为Adobe Campaign创建定位体验。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 1%
---
# 面向 Adobe Campaign 的目标选择{#targeting-your-adobe-campaign}

要定位Adobe Campaign新闻稿，您需要先设置仅在Classic UI（适用于客户端上下文）中提供的分段。 之后，您可以为Adobe Campaign创建定位体验。 本节将介绍这两种方法。

## 在AEM中设置分段 {#setting-up-segmentation-in-aem}

要设置分段，您需要使用经典UI设置区段。 其余步骤可以在标准UI中执行。

设置分段包括创建区段、品牌、营销活动和体验。

>[!NOTE]
>
>区段ID需要映射到Adobe Campaign端的ID。

### 创建区段 {#creating-segments}

要创建区段，请执行以下操作：

1. 在&#x200B;**&lt;host>：&lt;port>/miscadmin#/etc/segmentation**&#x200B;处打开[分段控制台](http://localhost:4502/miscadmin#/etc/segmentation)。
1. 创建页面并输入标题 — 例如&#x200B;**AC区段** — 并选择&#x200B;**区段(Adobe Campaign)**&#x200B;模板。
1. 在左侧的树视图中选择创建的页面。
1. 创建一个区段，例如，以男性用户为目标，方法是在您创建的名为“男性”的区段下创建一个页面，然后选择&#x200B;**区段(Adobe Campaign)**&#x200B;模板。
1. 打开创建的区段页面，并将&#x200B;**区段ID**&#x200B;从Sidekick拖放到页面上。
1. 双击该特征，输入表示在此例中为Adobe Campaign中定义的男性区段的ID，例如&#x200B;**MALE**，然后单击&#x200B;**确定**。 应显示以下消息： *`targetData.segmentCode == "MALE"`*
1. 对另一个区段重复这些步骤，例如，针对女性用户的区段。

### 创建品牌 {#creating-a-brand}

要创建品牌，请执行以下操作：

1. 在&#x200B;**Sites**&#x200B;中，导航到&#x200B;**Campaigns**&#x200B;文件夹（例如，在We.Retail中）。
1. 单击&#x200B;**创建页面**&#x200B;并输入页面的标题，例如We.Retail品牌，然后选择&#x200B;**品牌**&#x200B;模板。

### 创建活动 {#creating-a-campaign}

要创建活动，请执行以下操作：

1. 打开您创建的&#x200B;**品牌**&#x200B;页面。
1. 单击&#x200B;**创建页面**&#x200B;并为您的页面输入标题，例如We.Retail促销活动，选择&#x200B;**促销活动**&#x200B;模板，然后单击&#x200B;**创建**。

### 创建体验 {#creating-experiences}

要为区段创建体验，请执行以下操作：

1. 打开您创建的&#x200B;**Campaign**&#x200B;页面。
1. 通过单击&#x200B;**创建页面**&#x200B;并为页面输入标题（例如，在为“男性”区段创建体验时输入“男性”），为区段创建体验，然后选择&#x200B;**体验**&#x200B;模板。
1. 打开已创建的体验页面。
1. 单击&#x200B;**编辑**，然后在“区段”下方单击&#x200B;**添加项**。
1. 输入男性区段的路径，例如&#x200B;**/etc/segmentation/ac-segments/male**，然后单击&#x200B;**确定**。 应该显示以下消息：*体验面向：男性*
1. 重复上述步骤为所有区段（例如，女性目标）创建体验。
