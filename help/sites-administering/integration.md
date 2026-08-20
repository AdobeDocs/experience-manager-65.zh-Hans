---
title: 解决方案集成
description: 详细了解Adobe Experience Manager (AEM)与其他Adobe或第三方服务集成。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ee5e8ebb-773f-4aa6-9c3e-2cc3bf4a3bbd
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 21%

---

# 解决方案集成{#solutions-integration}

* [与Adobe Experience Cloud集成](/help/sites-administering/marketing-cloud.md)
* [与第三方服务集成](/help/sites-administering/third-party-services.md)
* [外部提供商的 Analytics](/help/sites-administering/external-providers.md)
* [目录生成器](/help/sites-administering/catalog-producer.md)
* [了解、应用和策划智能标记](/help/assets/enhanced-smart-tags.md)

以下信息介绍了如何将AEM与其他Adobe或第三方服务集成：

>[!NOTE]
>
>如果您将自定义代理配置与集成结合使用，则必须同时配置HTTP客户端代理配置，因为AEM的某些功能使用的是3.x API，而其他一些功能使用的是4.x API：
>
>* 3.x使用[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)进行配置
>* 4.x配置有[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
