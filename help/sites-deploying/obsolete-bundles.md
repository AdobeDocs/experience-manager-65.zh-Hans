---
title: 升级后卸载的废弃捆绑包列表
description: 此列表详细列出了升级到AEM 6.3时自动卸载的包。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 0defbdc7-d414-4662-a31f-88c8d63d68eb
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 835ee49e-9248-5578-a60a-15c097807178
    internal-label: Upgrading
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 6%
---
# 升级后卸载的废弃捆绑包列表{#list-of-obsolete-bundles-uninstalled-after-the-upgrade}

>[!NOTE]
>
>如果您的代码依赖于这些捆绑包，请确保与Adobe支持部门联系，并请求为受影响的区域提供兼容包。

升级到AEM 6.3时，将根据执行升级的AEM版本，自动卸载以下包：

**AEM 6.1：**

* org.eclipse.equinox.region，版本1.1.0.v20120522-1841，活动
* org.apache.sling.installer.factory.subsystems，版本1.0.0，活动
* org.apache.aries.subsystem.core，版本1.2.0，活动
* org.apache.aries.subsystem.api，版本1.1.0，活动
* org.apache.felix.resolver，版本1.0.0，活动
* org.osgi.service.subsystem.region.context.0，版本1.0.0，活动
* com.adobe.cq.cq-creativecloud-cloudims，版本0.0.10，活动
* com.adobe.cq.cq-creativecloud-commons，版本0.0.8，活动
* com.adobe.cq.cq-creativecloud-filesync，版本0.0.12，已安装
* com.adobe.cq.cq-creativecloud-storage，版本0.0.8，已安装
* biz.aQute.bndlib，版本1.43.0，活动
* com.day.cq.dam.commons.nekohtml，版本0.9.5，活动
* com.day.cq.mcm.cq-mcm-silverpop-integration，版本1.2.2，活动

**AEM 6.0：**

* org.apache.sling.discovery.impl，版本1.1.6，活动
* com.adobe.granite.installer.patch，版本0.4.0，活动
* biz.aQute.bndlib，版本1.43.0，活动
* com.day.cq.cq-jobs-core，版本5.4.0，活动
* com.day.cq.cq-opensocial，版本5.7.2，活动
* com.day.cq.cq-pinauthhandler，版本1.1.2，活动
* com.day.cq.dam.commons.nekohtml，版本0.9.5，活动
* com.day.cq.mcm.cq-mcm-silverpop-integration，版本1.1.6，活动
* com.day.cq.wcm.cq-wcm-mobile-phonegap-build-integration，版本5.7.18，活动

**CQ 5.6.1：**

* biz.aQute.bndlib，版本1.43.0，活动
* com.day.cq.cq-pinauthhandler，版本1.0.0，活动
* com.day.cq.dam.commons.nekohtml，版本0.9.5，活动
* com.day.crx.crxde-support，版本2.3.14，已安装
* com.day.cq.mcm.cq-mcm-silverpop-integration，版本1.0.2，活动

**CQ 5.6.0：**

* com.day.cq.cq-pinauthhandler，版本1.0.0，活动
* com.day.cq.dam.commons.nekohtml，版本0.9.5，活动
* com.day.crx.crxde-support，版本2.3.14，已安装
