---
title: 为 AEM 应用程序进行配置
description: 了解如何使用Adobe Experience Manager应用程序更新应用程序OTA（空中）的内容。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 523b1ccd-901e-5e3b-9fa7-f3dfd82463d5
    internal-label: Configuring
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 18%
---
# 为 AEM 应用程序进行配置{#configuring-for-aem-apps}

Adobe Experience Manager应用程序允许您更新应用程序OTA的内容（空中）。 更新的内容存储在发布实例上。 要允许设备上的应用程序连接到发布实例并检查更新，必须将发布实例配置为允许空的反向链接标头。

## 配置空反向链接标头 {#configuring-empty-referrer-header}

要配置反向链接过滤器服务：

* 在以下地址打开 Apache Felix 控制台（**配置**）：
* https://<服务器>：<端口号>/system/console/configMgr
* 以管理员身份登录。
* 在&#x200B;**配置**&#x200B;菜单中，选择： *Apache Sling引用过滤器*
* 选中允许空字段，以便您可以允许为空/缺少反向链接标头。
* 单击&#x200B;**保存**&#x200B;以保存更改。

![chlimage_1-58](assets/chlimage_1-58a.png)

有关更多详细信息，请参阅[OSGI配置设置](/help/sites-deploying/osgi-configuration-settings.md)和[安全核对清单 — 跨站点请求伪造问题](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)。
