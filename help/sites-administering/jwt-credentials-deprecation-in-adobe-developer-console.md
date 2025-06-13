---
title: 在 Adobe Developer Console 中弃用 JWT 凭据
description: 了解在 Adobe Developer Console 中弃用 JWT 凭据对 AEM 产生的影响
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 72%

---

# 在 Adobe Developer Console 中弃用 JWT 凭据 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> 有关详细信息，AEM as a Cloud Service应引用[AEMaaCS版本](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=zh-Hans)的可比较文章。

Adobe 客户使用 [Adobe Developer Console](https://developer.adobe.com/console) 生成通过其可访问各种 API 的凭据。客户可选择从 OAuth 服务器到服务器到单页应用程序的多种凭据类型。已弃用其中一种凭据类型，服务帐户 (JWT) 凭据，改为使用 OAuth 服务器到服务器凭据。从 2024 年 6 月 3 日起无法创建新的服务帐户 (JWT) 凭据，而现有的 JWT 凭据将从 2025 年 1 月 1 日起失效。可[了解该弃用](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration)。

本文提供了有关Adobe Experience Manager (AEM) 6.5客户应如何处理弃用的其他上下文。

主要功能是，AEM现在支持AEM的新OAuth服务器到服务器凭据。 您可能已经收到一封关于迁移 JWT 凭据的说明邮件，现在可以进行迁移了。

在以下部分中列出的场景中，既然 AEM 支持 OAuth 服务器到服务器凭据，客户就必须（或在某些情况下不得）将其服务帐户 (JWT) 凭据替换为这些凭据。[了解如何](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration#migration-overview)迁移凭据。

## 将 AEM 与其他 Adobe 解决方案集成 {#integrating-aem-with-other-adobe-solutions}

**操作**：由于 AEM 现支持 OAuth 凭据，请迁移您的配置。

**相关的AEM版本**： Adobe Managed Services （Service Pack 21及更高版本）。

AEM客户使用AEM来配置与所有其他Adobe解决方案的集成。 例如，Adobe Target、Adobe Analytics 等。

![将 AEM 与其他解决方案集成](/help/sites-administering/assets/jwt-deprecation.png)

有关如何完成以下操作的详细信息，请参阅[为AEM设置IMS集成](/help/sites-administering/setting-up-ims-integrations-for-aem.md)：

* 使用 OAuth 凭据创建配置
* 将使用 JWT 凭据创建的配置迁移到使用 OAuth 凭据

## Cloud Manager API {#cloud-manager-apis}

**操作**：确认何时可以将这些从 JWT 迁移到 OAuth 凭据。

**相关的AEM版本**： Adobe Managed Services （Service Pack 21及更高版本）。

客户创建 Adobe Developer Console 项目，以使其可调用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。在弃用的 JWT 凭证于 2025 年 1 月到期之前，Adobe Developer 项目中的凭据应迁移到 OAuth 服务器到服务器凭据类型。
