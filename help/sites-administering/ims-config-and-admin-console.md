---
title: 对Adobe Experience Manager Managed Services的Adobe IMS身份验证和 [!DNL Admin Console] 支持
description: 了解如何在Adobe Experience Manager中使用 [!DNL Admin Console] 。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 6%

---

# AEM Managed Services的Adobe IMS身份验证和[!DNL Admin Console]支持 {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>此功能仅适用于AdobeManaged Services客户。

## 简介 {#introduction}

AEM 6.4.3.0为&#x200B;**AEM Managed Services**&#x200B;客户引入了对AEM实例和基于Adobe IMS(Identity Management System)的身份验证的[!DNL Admin Console]支持。

AEM加入[!DNL Admin Console]将允许AEM Managed Services客户在一个控制台中管理所有Experience Cloud用户。 可以将用户分配到与AEM实例关联的产品配置文件，从而让他们登录到特定实例。

## 主要亮点 {#key-highlights}

* AEM IMS身份验证支持仅适用于AEM作者、管理员或开发人员，不适用于客户站点的外部最终用户，如站点访客
* [!DNL Admin Console]将AEM Managed Services客户表示为IMS组织，将其实例表示为产品上下文。 客户系统和产品管理员将能够管理对实例的访问
* AEM Managed Services将与[!DNL Admin Console]同步客户拓扑。 在[!DNL Admin Console]中，每个实例将有一个AEM Managed Services产品上下文实例。
* [!DNL Admin Console]中的产品配置文件将决定用户可以访问哪些实例
* 支持使用客户自己的符合SAML 2的身份提供程序的联合身份验证
* 仅支持Enterprise ID或Federated ID（适用于客户的单点登录），不支持个人AdobeID。
* [!DNL User Management] (Adobe[!DNL Admin Console]中)将继续由客户管理员拥有。

## 架构 {#architecture}

IMS身份验证在AEM和Adobe IMS端点之间使用OAuth协议来工作。 将用户添加到 IMS 并拥有 Adobe 身份后，他们便可以使用 IMS 凭证登录到 AEM Managed Services 实例。

用户登录流程如下所示，用户将被重定向到IMS，并可以选择性地重定向客户IDP以进行SSO验证，然后重定向回AEM。

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## 如何设置 {#how-to-set-up}

### 将组织载入[!DNL Admin Console] {#onboarding-organizations-to-admin-console}

客户载入[!DNL Admin Console]是使用Adobe IMS进行AEM身份验证的先决条件。

第一步，客户应在Adobe IMS中设置组织。 Adobe企业客户在[Adobe [!DNL Admin Console]](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)中表示为IMS组织。

AEM Managed Services客户应已设置组织，作为IMS设置的一部分，客户实例将在[!DNL Admin Console]中可用，以用于管理用户权利和访问权限。

迁移到IMS进行用户身份验证是AMS和客户共同努力的结果，每个客户都有要完成的工作流。

客户作为IMS组织存在且AMS完成为客户配置IMS后，以下是所需的配置工作流的摘要：

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. 指定的系统管理员会收到登录到[!DNL Admin Console]的邀请
1. 系统管理员声明域以确认域的所有权(在此示例中为acme.com)
1. 系统管理员设置用户目录
1. 系统管理员在[!DNL Admin Console]中为SSO设置配置身份提供程序(IDP)。
1. AEM管理员可以像往常一样管理本地组、权限和特权。 请参阅用户和组同步

>[!NOTE]
>
>有关AdobeIdentity Management基础知识（包括IDP配置）的更多信息，请参阅关于[设置标识和单点登录](https://helpx.adobe.com/cn/enterprise/using/set-up-identity.html)的文章。
>
>有关企业管理和[!DNL Admin Console]的详细信息，请参阅[欢迎使用企业和团队管理指南](https://helpx.adobe.com/cn/enterprise/managing/user-guide.html)。

### 将用户载入[!DNL Admin Console] {#onboarding-users-to-the-admin-console}

根据客户的规模和偏好，可通过三种方式载入用户：

1. 在[!DNL Admin Console]中手动创建用户和组
1. 上传包含用户的CSV文件
1. 从客户的企业Active Directory同步用户和组。

#### 通过[!DNL Admin Console] UI手动添加 {#manual-addition-through-admin-console-ui}

可以在[!DNL Admin Console] UI中手动创建用户和组。 如果客户没有许多要管理的用户，则可以使用此方法。 例如，少于50个AEM用户。

如果客户已在使用此方法管理其他Adobe产品(如Adobe Analytics、Adobe Target或Adobe Creative Cloud应用程序)，也可以手动创建用户。

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### 在[!DNL Admin Console] UI中上传文件 {#file-upload-in-the-admin-console-ui}

为便于创建用户，可以上传CSV文件以批量添加用户：

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### 用户同步工具 {#user-sync-tool}

User Sync Tool （简称UST）使企业客户能够创建或管理使用Active Directory或其他经过测试的OpenLDAP目录服务的Adobe用户。 目标用户是IT标识管理员（企业目录和系统管理员），他们将能够安装和配置该工具。 该开源工具可自定义，因此客户可以让开发人员对其进行修改以满足他们自己的特定要求。

当用户同步运行时，它会从组织的Active Directory（或任何其他兼容的数据源）中获取用户列表，并将其与[!DNL Admin Console]中的用户列表进行比较。 然后，它会调用Adobe[!DNL User Management] API，以便[!DNL Admin Console]与组织的目录同步。 更改流是完全单向的；在[!DNL Admin Console]中所做的任何编辑都不会推送到该目录。

该工具允许系统管理员将客户目录中的用户组与[!DNL Admin Console]中的产品配置和用户组进行映射，新的UST版本还允许在[!DNL Admin Console]中动态创建用户组。

要设置用户同步，组织需要创建一组凭证，其方式与使用[[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html)的方式相同。

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

User Sync是通过AdobeGithub存储库在以下位置分发的：

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

请注意，支持创建动态组的预发行版2.4RC1可用，可从此处找到： [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

此版本的主要功能是能够动态映射新的LDAP组以获得[!DNL Admin Console]中的用户成员资格，以及动态创建用户组。

有关新组功能的更多信息，请访问：

[https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options](https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options)

>[!NOTE]
>
>有关更多详细信息，请参阅：
>
>* [用户同步工具 — Adobe用户同步](https://adobe-apiplatform.github.io/user-sync.py/en/)
>
>* User Sync Tool需要使用[API访问身份验证](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)中描述的过程注册为Adobe I/O客户端UMAPI
>
>* [Adobe Developer Console文档](https://developer.adobe.com/developer-console/docs/guides/)。
>
>* [用户管理API文档](https://adobe-apiplatform.github.io/umapi-documentation/en/)。
>

>[!NOTE]
>
>AEM IMS配置将由AdobeManaged Services团队处理。 但是，客户管理员可以根据他们的要求（例如，自动组成员资格或组映射）对其进行修改。 您的Managed Services团队还将注册IMS客户端。

## 使用方法 {#how-to-use}

### 在[!DNL Admin Console]中管理产品和用户访问权限 {#managing-products-and-user-access-in-admin-console}

当客户产品管理员登录到[!DNL Admin Console]时，他们将看到AEM Managed Services产品上下文的多个实例，如下所示：

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

在此示例中，组织&#x200B;*AEM-MS-Onboard*&#x200B;具有32个实例，这些实例跨不同的拓扑和环境，如Stage、Prod等。

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

可以检查实例详细信息以标识实例：

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

在每个“产品上下文”实例下，都有一个关联的产品配置文件。 此产品配置文件用于为用户分配访问权限。

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

在此产品配置文件下添加的任何用户都将能够登录到该实例，如下例所示：

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### 登录AEM {#logging-into-aem}

#### 本地管理员登录 {#local-admin-login}

AEM可以继续支持管理员用户在本地登录，因为登录屏幕提供了在本地登录的选项：

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### 基于IMS的登录 {#ims-based-login}

对于其他用户，只需在实例上配置 IMS 即可使用基于 IMS 的登录。用户第一次单击&#x200B;**使用Adobe**&#x200B;登录，如下所示：

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

然后，他们将被重定向到IMS登录屏幕并输入其凭据：

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

如果在初始[!DNL Admin Console]设置期间配置了联合IDP，则用户将被重定向到用于SSO的客户IDP。

在以下示例中，IDP为Okta ：

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

身份验证完成后，用户将被重定向回 AEM 并登录：

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### 迁移现有用户 {#migrating-existing-users}

对于正在使用其他身份验证方法并且现在正迁移到IMS的现有AEM实例，需要执行迁移步骤。

AEM存储库中的现有用户（通过LDAP或SAML本地获取）可以使用用户迁移实用程序作为IDP迁移到指向IMS。

此实用程序将作为IMS配置的一部分由您的AMS团队运行。

### 在AEM中管理权限和ACL {#managing-permissions-and-acls-in-aem}

将继续在AEM中管理访问控制和权限，这可以通过将来自IMS的用户组(例如，以下示例中的AEM-GRP-008)与定义权限和访问控制的本地组分离来实现。 可以将从IMS同步的用户组分配给本地组并继承权限。

在以下示例中，我们将同步的组作为示例添加到本地 *Dam_Users* 组。

此处，用户也已分配给[!DNL Admin Console]中的几个组。 (可以使用用户同步工具从LDAP同步用户和组，也可以在本地创建。 请参阅&#x200B;**以前将用户载入[!DNL Admin Console]**。

>[!NOTE]
>
>用户组仅在用户登录实例时同步。

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

用户是 IMS 中以下组的一部分：

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

用户登录时，会同步其组成员资格，如下所示：

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

在AEM中，可以将从IMS同步的用户组作为成员添加到现有的本地组，例如DAM用户。

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

如下所示，组&#x200B;*AEM-GRP_008*&#x200B;继承DAM用户的权限和特权。 这是管理已同步组权限的有效方式，也常用于基于LDAP的身份验证方法。

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
