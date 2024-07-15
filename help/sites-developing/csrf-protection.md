---
title: CSRF保护框架
description: 该框架使用令牌来确保客户端请求合法
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# CSRF保护框架{#the-csrf-protection-framework}

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
>请确保您还进行了必要的[Dispatcher配置更改](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)以使用CSRF Protection Framework。

>[!NOTE]
>
>如果您在Web应用程序中使用清单缓存，请确保将“**&amp;amp；ast；**”添加到清单中，以确保令牌不会使CSRF令牌生成调用脱机。 有关详细信息，请参阅此[链接](https://www.w3.org/TR/offline-webapps/)。
>
有关CSRF攻击以及缓解这些攻击方法的详细信息，请参阅[跨站点请求伪造OWASP页面](https://owasp.org/www-community/attacks/csrf)。
