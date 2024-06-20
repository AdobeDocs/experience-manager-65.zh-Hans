---
title: 为AEM设置IMS集成
description: 了解如何为AEM设置IMS集成
feature: Security
role: Admin
exl-id: 3c6dbb7e-847f-407b-ac9c-4676dba671a5
source-git-commit: c2d996586d2ec7299e856a97ae1b744245c730bb
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 63%

---

# 为AEM设置IMS集成 {#setting-up-ims-integrations-for-aem}


>[!NOTE]
>
>Adobe客户使用 [Adobe Developer控制台](https://developer.adobe.com/console) 生成凭据以启用对各种API的访问。 客户可选择从 OAuth 服务器到服务器到单页应用程序的多种凭据类型。凭据类型服务帐户(JWT)现已弃用，推荐使用Service Pack 20的OAuth服务器到服务器凭据。 此更改可以重新移植到旧版Service Pack，从Service Pack 11开始直到Service Pack 20，并使用您可以下载的修补程序 [此处](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/ims-jwt-compatibility-package-6.5-1.0.zip).

Adobe Experience Manager (AEM)可与许多其他Adobe解决方案集成。 例如，Adobe Target、Adobe Analytics 等。

这些集成使用配置了 S2S OAuth 的 IMS 集成。

* 创建后：

   * [Developer Console 中的凭据](#credentials-in-the-developer-console)

* 然后您就可以：

   * 创建（新）[OAuth 配置](#creating-oauth-configuration)

   * [将现有 JWT 配置迁移到 OAuth 配置](#migrating-existing-JWT-configuration-to-oauth)

>[!CAUTION]
>
>以前，配置是使用 [JWT 凭据进行的，但现在这些凭据在 Adobe Developer Console 中已遭弃用](/help/sites-administering/jwt-credentials-deprecation-in-adobe-developer-console.md)。
>
>无法再创建或更新此类配置，但可以将它们迁移到 OAuth 配置。

## Developer Console 中的凭据 {#credentials-in-the-developer-console}

第一步，您必须在Adobe Developer控制台中配置OAuth凭据。

有关如何执行此配置的详细信息，请参阅开发人员控制台文档，具体取决于您的要求：

* 概述：

   * [服务器到服务器身份验证](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

* 创建新的 OAuth 凭据：

   * [OAuth 服务器到服务器凭据实施指南](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)

* 将现有的 JWT 凭据迁移到 OAuth 凭据：

   * [从服务帐户 (JWT) 凭据迁移到 OAuth 服务器到服务器凭据](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)

例如：

![Developer Console 中的 OAuth 凭据](assets/ims-configuration-developer-console.png)

## 创建 OAuth 配置 {#creating-oauth-configuration}

要使用 OAuth 创建新的 Adobe IMS 集成：

1. 在 AEM 中，导航到&#x200B;**工具**、**安全**、**Adobe IMS 集成**。

1. 选择&#x200B;**创建**。

1. 根据 [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/) 中的详细信息完成配置。例如：

   ![创建 OAuth 配置](assets/ims-create-oauth-configuration.png)

1. **保存**&#x200B;您的更改。

## 将现有 JWT 配置迁移到 OAuth 配置 {#migrating-existing-JWT-configuration-to-oauth}

要迁移基于 JWT 凭据的现有 Adobe IMS 集成，请执行以下操作：

>[!NOTE]
>
>此示例显示启动 IMS 配置。

1. 在 AEM 中，导航到&#x200B;**工具**、**安全**、**Adobe IMS 集成**。

1. 选择需要迁移的 JWT 配置。JWT 配置标有 **JWT 凭据（已弃用）**&#x200B;警告。

1. 选择&#x200B;**属性**：

   ![选择 JWT 配置](assets/ims-migrate-jwt-select-configuration.png)

1. 该配置将以只读方式打开：

   ![配置属性 - 只读](assets/ims-migrate-jwt-properties-read-only.png)

1. 从&#x200B;**身份验证类型**&#x200B;下拉菜单中选择 **OAuth**：

   ![选择身份验证类型](assets/ims-migrate-jwt-authentication-type.png)

1. 可用属性已更新。 使用 Developer Console 中的详细信息来完成以下操作：

   ![填写 OAuth 详细信息](assets/ims-migrate-jwt-complete-oauth-details.png)

1. 使用&#x200B;**保存并关闭**来保存您的更新。
当您返回到控制台时， **JWT凭据（已弃用）** 警告已消失。
