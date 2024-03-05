---
title: Adobe Developer Console 中的 JWT 凭据弃用
description: 了解 Adobe Developer Console 中的 JWT 凭据弃用对 AEM 的影响
source-git-commit: 18bee77ab6fcb2d635d389f929c1dd8e2bc25de5
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 81%

---


# Adobe Developer Console 中的 JWT 凭据弃用 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud Service应参考 [本文](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) 以了解更多信息。

Adobe 客户使用 [Adobe Developer Console](https://developer.adobe.com/console) 生成可用于访问各种 API 的凭据。客户可以从 OAuth 服务器到服务器到单页应用程序的各种凭据类型中进行选择。其中一种凭据类型（即服务帐户 (JWT) 凭据）已被弃用，取而代之的是 OAuth 服务器到服务器凭据。自 2024 年 5 月 1 日起将无法创建新的服务帐户 (JWT) 凭据，并且现有的 JWT 凭据自 2025 年 1 月 1 日起将失效。您可以[阅读有关弃用的信息](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

本文提供了有关AEM 6.5客户应如何处理弃用的其他上下文。

目前，主要要点是 AEM 功能尚不支持新的 OAuth 服务器到服务器凭据。支持即将推出 — 如果您运行的是最新的Service Pack 20或更低版本（Service Pack 21及更高版本将自动包含该版本），那么将在2024年4月中旬之前通过一个特殊的兼容包安装用于AEM 6.5。 您可能已经收到一封电子邮件，其中包含迁移 JWT 凭据的说明，但请放心，您可以且应该推迟凭据迁移，直到 AEM 支持新的 OAuth 服务器到服务器凭据类型。

在以下部分中列出的场景中，一旦 AEM 在 4 月中旬支持 OAuth 服务器到服务器凭据，客户就必须（或在某些情况下不得）将其服务帐户 (JWT) 凭据替换为这些凭据。[了解将来](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)如何更换凭据。

>[!NOTE]
>
>[**AEM** Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#crxde-lite-and-developer-console)（请注意，可通过名称中的 **AEM** 来与 **Adobe** Developer Console 区分开来）提供了一个实用程序来生成用于服务器到服务器 API 的 [JWT 令牌](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html)。这些凭据未被弃用，可继续使用。


## 将 AEM 与其他 Adobe 解决方案集成 {#integrating-aem-with-other-adobe-solutions}

**行动**：等到 2024 年 4 月中旬 AEM 支持这些凭据后再进行迁移。

**相关AEM版本**：AdobeManaged Services（Service Pack 20及更低版本）。


AEM 客户使用 AEM 创作 UI 配置与所有其他 Adobe 解决方案的集成。例如，Adobe Target、Adobe Analytics、Adobe Launch、AFCS 等。

![将 AEM 与其他解决方案集成](/help/sites-administering/assets/jwt-deprecation.png)

例如，以下是有关配置与 Adobe Target 的集成的[说明](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=zh-Hans)。在 AEM 于 4 月中旬支持 OAuth 服务器到服务器凭据后，[在 AEM 中完成 IMS 配置](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem)部分中的 API 密钥应迁移到 OAuth 服务器到服务器凭据类型。这些说明将在 4 月中旬进行更新和修订，以帮助您应用新的 OAuth 服务器到服务器凭据。

## Cloud Manager API {#cloud-manager-apis}

**行动**：等到 2024 年 4 月中旬 AEM 支持这些凭据后再进行迁移。

**相关AEM版本**：AdobeManaged Services（Service Pack 20及更低版本）。

客户创建 Adobe Developer Console 项目，以便调用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。在 AEM 和 Cloud Manager 支持 OAuth 服务器到服务器凭据后，Adobe Developer 项目中的凭据应迁移到 OAuth 服务器到服务器凭据类型。
