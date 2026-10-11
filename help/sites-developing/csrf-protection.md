---
title: CSRF 保护框架
description: 该框架使用令牌来确保客户端请求合法
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 6%
---
# CSRF 保护框架{#the-csrf-protection-framework}

除了Apache Sling反向链接过滤器之外，Adobe还提供了一个新的CSRF保护框架来抵御此类攻击。

该框架使用令牌来保证客户端请求的合法性。 令牌在表单发送到客户端时生成，并在表单发送回服务器时进行验证。

>[!NOTE]
>
>匿名用户的发布实例上没有任何令牌。

## 要求 {#requirements}

### 依赖项 {#dependencies}

任何依赖于`granite.jquery`依赖关系的组件都可以自动从CSRF保护框架中受益。 如果不是，则对于您的任何组件，您必须先向`granite.csrf.standalone`声明依赖关系，然后才能使用框架。

### 复制加密密钥 {#replicating-crypto-keys}

要使用令牌，您需要将HMAC二进制文件复制到部署中的所有实例。 有关详细信息，请参阅[复制HMAC密钥](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key)。

>[!NOTE]
>
>此外，请确保进行了必要的Dispatcher配置更改以使用CSRF保护框架：
>
>* [配置Adobe Experience Manager Dispatcher以防御CSRF攻击](https://experienceleague.adobe.com/en/docs/experience-manager-dispatcher/using/configuring/configuring-dispatcher-to-prevent-csrf)
>* [Dispatcher概述](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-dispatcher/using/dispatcher)

>[!NOTE]
>
>如果您将清单缓存与Web应用程序一起使用，请确保将“**&amp;ast；**”添加到清单中，以确保令牌不会使CSRF令牌生成调用脱机。 有关详细信息，请参阅此[链接](https://www.w3.org/TR/offline-webapps/)。
>
>有关CSRF攻击以及缓解这些攻击方法的详细信息，请参阅[跨站点请求伪造OWASP页面](https://owasp.org/www-community/attacks/csrf)。
