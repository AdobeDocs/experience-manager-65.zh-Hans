---
title: 在 Adobe Developer Console 中弃用 JWT 凭据
description: 了解在 Adobe Developer Console 中弃用 JWT 凭据对 AEM 产生的影响
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 36c95ea717a0abcb0b6ef9b0796a94d7b0f66329
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 58%

---

# 在 Adobe Developer Console 中弃用 JWT 凭据 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud Service应参考 [本文](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) 以了解更多信息。

Adobe 客户使用 [Adobe Developer Console](https://developer.adobe.com/console) 生成通过其可访问各种 API 的凭据。客户可选择从 OAuth 服务器到服务器到单页应用程序的多种凭据类型。已弃用其中一种凭据类型，服务帐户 (JWT) 凭据，改为使用 OAuth 服务器到服务器凭据。从 2024 年 6 月 3 日起无法创建新的服务帐户 (JWT) 凭据，而现有的 JWT 凭据将从 2025 年 1 月 1 日起失效。可[了解该弃用](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

本文提供了有关AEM 6.5客户应如何处理弃用的其他上下文。

目前主要重点是 AEM 功能尚不支持新的 OAuth 服务器到服务器凭据。支持即将推出 — 如果您运行的是最新的Service Pack 20或更低版本（Service Pack 21及更高版本将自动包含该版本），那么将在2024年5月中旬之前通过一个特殊的兼容包安装用于AEM 6.5。 您可能已经收到一封电子邮件，其中包含迁移 JWT 凭据的说明，但请放心，您可以且应该推迟凭据迁移，直到 AEM 支持新的 OAuth 服务器到服务器凭据类型。

以下部分列出了客户必须（或在某些情况下不得）使用OAuth服务器到服务器凭据替换其服务帐户(JWT)凭据的情况，一旦AEM在5月中旬支持这些凭据。 [了解如何](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)在未来替换凭据。

## 将 AEM 与其他 Adobe 解决方案集成 {#integrating-aem-with-other-adobe-solutions}

**操作**：请等待迁移，直到2024年5月中旬之后AEM才支持迁移。

**相关AEM版本**：AdobeManaged Services（Service Pack 20及更低版本）。


AEM 客户使用 AEM 创作 UI 配置与所有其他 Adobe 解决方案的集成。例如，Adobe Target、Adobe Analytics、Adobe Launch、AFCS 等解决方案。

![将 AEM 与其他解决方案集成](/help/sites-administering/assets/jwt-deprecation.png)

例如，此处就是配置与 Adobe Target 的集成的[说明](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/administering/integration/integration-target-ims)。中的API密钥 [在AEM中完成IMS配置](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/administering/integration/integration-target-ims#completing-the-ims-configuration-in-aem) 一旦AEM在5月中旬支持这些凭据，应将部分迁移到OAuth服务器到服务器凭据类型。 这些说明将于5月中旬更新，以帮助您应用新的OAuth服务器到服务器凭据。

## Cloud Manager API {#cloud-manager-apis}

**操作**：请等待迁移，直到2024年5月中旬之后AEM才支持迁移。

**相关AEM版本**：AdobeManaged Services（Service Pack 20及更低版本）。

客户创建 Adobe Developer Console 项目，以使其可调用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。一旦 AEM 和 Cloud Manager 支持 OAuth 服务器到服务器凭据类型，即应将 Adobe Developer 项目中的凭据迁移到该类型。
