---
title: 将AEM 6.5与Adobe Campaign集成
description: 了解AEM 6.5对Adobe Campaign集成的支持。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ab41e540-1d43-4fc2-99d4-621ff2290e77
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 12%
---

# 将AEM 6.5与Adobe Campaign集成{#integrating-with-adobe-campaign}

了解AEM 6.5对Adobe Campaign集成的支持。

Adobe Campaign是一套解决方案，可让您在所有线上和线下渠道之间个性化并提交促销活动。

>[!NOTE]
>
>本文档介绍如何将Adobe Campaign与AEM 6.5、内部部署或AMS托管的AEM解决方案集成。
>
>有关将Adobe Campaign与AEM as a Cloud Service（云原生AEM解决方案）集成的详细信息，[请参阅此文档。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/integrations/campaign.html)

## 与 Adobe Campaign Classic 集成 {#acc}

有几个Adobe Campaign Classic (ACC)版本。 是否支持与AEM集成，取决于您实施的ACC版本，以及Adobe Manage Services (AMS)中是否本地安装了AEM。

| ACC 版本 | 与AEM 6.5 <br>内部部署集成 | 与AEM 6.5<br>AMS集成 |
|---|---|---|
| [v7](https://experienceleague.adobe.com/docs/campaign-classic.html) | 支持 | 支持 |
| [v8客户端控制台](https://experienceleague.adobe.com/docs/campaign-v8.html) | 支持 | 支持 |

以下文档介绍了如何将AEM与Adobe Campaign Classic集成。

* [与Adobe Campaign Classic集成](/help/sites-administering/campaignonpremise.md) — 了解有关配置集成的分步详细信息。

以下附加文档介绍了如何使用集成。

* [电子邮件核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html) — 了解可用于在AEM中创作Campaign内容的标准电子邮件组件。
* [Adobe Campaign Classic集成疑难解答](/help/sites-administering/troubleshooting-campaignintegration.md) — 了解如何修复AEM-ACC集成最常见的问题。

## 与 Adobe Campaign Standard 集成 {#acs}

[Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html) (ACS)与AEM的集成取决于AEM是否安装在Adobe Manage Services (AMS)的内部部署中。

| 与AEM 6.5 <br>内部部署集成 | 与AEM 6.5<br>AMS集成 |
|---|---|
| 支持 | 支持 |
| 支持 | 支持 |

以下文档介绍了如何将AEM与Adobe Campaign Standard集成。

* [与 Adobe Campaign Standard 集成](/help/sites-administering/campaignstandard.md)

以下附加文档介绍了如何使用集成。

* [电子邮件核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html)
