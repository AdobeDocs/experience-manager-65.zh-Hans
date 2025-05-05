---
title: AEM Commerce - GDPR就绪
description: 了解在AEM Commerce中处理GDPR请求的过程以及如何使用它们。
contentOwner: carlino
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Architect, Developer, Leader, User, Data Architect, Data Engineer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# AEM Commerce - GDPR就绪{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>以下部分使用GDPR作为示例，但包含的详细信息适用于所有数据保护和隐私法规；例如GDPR和CCPA。

欧盟有关数据隐私权的《通用数据保护条例》自2018年5月起生效。 请参阅Adobe隐私中心[&#128279;](https://business.adobe.com/privacy/general-data-protection-regulation.html)的GDPR页面。

>[!NOTE]
>
>有关更多详细信息，请参阅[AEM GDPR准备工作](/help/managing/data-protection-and-privacy.md)。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

通过Adobe现成的Commerce集成，AEM成为体验层，使用服务并将数据发送回以Headless模式运行的客户商务平台。

对于某些商务平台，Adobe在AEM中存储配置文件信息(`/home/users`)和商业令牌（登录到Commerce平台）。 对于这些用例，请阅读[处理AEM平台的GDPR请求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## 处理AEM Commerce的GDPR请求 {#handling-gdpr-requests-for-aem-commerce}

对于SalesforceCommerce Cloud集成，AEM Commerce不会存储任何GDPR相关信息。 将请求转发到[Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp)。

对于hybris和HCL WebSphere® Commerce的集成，AEM中提供了一些数据。 使用[AEM Platform GDPR说明](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)并考虑以下问题：

1. **我的数据在哪里存储/使用？**&#x200B;缓存的用户配置文件信息，如名称、商业用户标识符、令牌、密码和地址数据，如AEM中所示。
1. **我应该与谁共享包含的GDPR数据？** AEM Commerce中与GDPR相关的数据的任何更新都不会存储（除了上面提到的相关配置文件信息之外），而是通过代理传回Commerce平台。
1. **如何删除我的用户数据**？ 在AEM中删除用户配置文件并调用商务平台上的用户删除操作。

>[!NOTE]
>
>如有必要，请查看[hybris wiki](https://wiki.hybris.com/)或[HCL WebSphere® Commerce文档](https://help.hcltechsw.com/commerce/index.html)。
