---
title: SRP — 社区内容存储
description: 从AEM Communities 6.1开始，用户生成的内容(UGC)存储在存储资源提供商(SRP)提供的单个公共存储中
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# SRP — 社区内容存储 {#srp-community-content-storage}

## 简介 {#introduction}

从AEM Communities 6.1开始，用户生成的内容(UGC)存储在存储资源提供商(SRP)提供的单个公共存储中。 有几种SRP选项可供选择，如ASRP、MSRP和JSRP。

与以前的版本不同，UGC不会跨AEM实例进行反向/正向复制。 相反，SRP允许直接从所有创作和发布实例中访问UGC以进行创建、读取、更新和删除(CRUD)操作，但JSRP除外。

以下是每个SRP选项](#characteristics-of-srp-options)的[特性，在选择适当的SRP和[基础部署](/help/communities/topologies.md)时，这些特性对于决策过程至关重要。

有关使用SRP for UGC的详细信息，请参阅[存储资源提供程序概述](/help/communities/srp.md)。

>[!NOTE]
>
>SRP仅适用于社区内容。 它不影响站点内容的存储位置（[节点存储](/help/sites-deploying/data-store-config.md)），也不影响AEM实例之间用户注册、用户配置文件和用户组的安全处理（另请参阅[管理用户数据](#managing-user-data)）。

>[!CAUTION]
>
>截至AEM 6.1，[UGC从未复制](#ugc-never-replicated)。
>
>当部署不包含公用存储（如默认的[JSRP](/help/communities/topologies.md#jsrp)拓扑）时，UGC将仅在输入它的AEM发布或创作实例上可见。 仅当拓扑包含发布群集时，UGC才在任何发布实例上可见。

## SRP选项的特性 {#characteristics-of-srp-options}

[ASRP -Adobe存储资源提供程序](/help/communities/asrp.md)

使用此选项，UGC会远程保留在由Adobe托管和管理的云服务中。 它需要额外的许可证，并且需要与客户代表合作，为该特定许可证设置帐户。 ASRP要求：

* Adobe提供并支持的相关云服务用于存储社区内容。
* 在特定地区（美国、欧洲、中东和非洲、亚太地区）选择数据中心。

* 对UGC的所有编程访问都必须通过SRP API。

ASRP适合：

* 对于TarMK发布场。
* 如果无意投资本地存储，

>[!NOTE]
>
>在ASRP中，将附件上载到帖子（或注释）存在限制，即50 MB。

[MSRP - MongoDB存储资源提供程序](/help/communities/msrp.md)

利用此选项，UGC将直接保留在本地MongoDB实例中。

MSRP要求：

* MongoDB的本地许可安装用于存储社区内容。
* Apache Solr的本地安装。
* 对UGC的所有编程访问都必须通过SRP API。

ASRP适合：

* 对于现有TarMK发布场。
* 用于MongoMK或RdbMK群集。
* 需要大量社区内容时。

[DSRP — 关系数据库存储资源提供程序](/help/communities/dsrp.md)

使用此选项，UGC将直接保留在本地MySQL数据库实例中。

DSRP要求：

* 用于存储社区内容的MySQL的本地安装。
* Apache Solr的本地安装。
* 对UGC的所有编程访问都必须通过SRP API。

DSRP适合：

* 对于现有TarMK发布场。
* 用于MongoMK或RdbMK群集。
* 需要大量社区内容时。

[JSRP - JCR存储资源提供程序](/help/communities/jsrp.md)

使用默认选项，没有公用存储。 UGC仅保留在与输入它的AEM实例相同的JCR存储库中。

JSRP：

* 将社区内容存储在社区内容发布到的AEM创作或发布实例的JCR存储库。
* 要求通过SRP API访问UGC的所有程序化权限。
* 如果部署了多个发布实例，则需要发布群集（TarMK场中的发布实例之间没有复制机制）。
* 审核仅在发布环境中执行（创作和发布之间没有反向/正向复制机制）。
* 最适合用于开发、演示和培训。

## 配置SRP {#configuring-srp}

通过[存储配置控制台](/help/communities/srp-config.md)，基于基础部署指定默认存储选项。

有关每个选项的详细配置信息，请参阅：

* [ASRP -Adobe存储资源提供程序](/help/communities/asrp.md)
* [MSRP - MongoDB存储资源提供程序](/help/communities/msrp.md)
* [DSRP — 关系数据库存储资源提供程序](/help/communities/dsrp.md)
* [JSRP - JCR存储资源提供程序](/help/communities/jsrp.md)

如果未主动选择存储选项，则默认启用JSRP。

## 附加信息 {#additional-information}

### 从未复制UGC {#ugc-never-replicated}

在创作环境中，作者创建页面内容并将其复制到发布环境。 当页面包含交互式AEM Communities功能（如评论、审核、论坛、博客或QnA）时，成员（在网站访客中签名）在发布实例上的交互会导致在发布环境中输入用户生成的内容(UGC)。

以前，此社区内容反向复制到创作实例，并从创作复制到发布实例。 在使用反向和正向复制来维护AEM实例之间的一致性时出现问题。

从AEM Communities 6.1开始，通过为UGC使用共享存储（如上所述），消除了UGC复制的需要。

在复制站点内容时，从不复制UGC。

### 管理用户数据 {#managing-user-data}

CommunitIes感兴趣的还有&#x200B;[*用户*、*用户组*&#x200B;和&#x200B;*用户配置文件*](/help/communities/users.md)。 当拓扑是[发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)时，在发布环境中创建和更新此用户相关数据时，这些数据需要可供其他发布实例使用。

从AEM Communities 6.1开始，使用Sling分发而不是复制来同步用户相关数据。 有关详细信息，请访问[用户同步](/help/communities/sync.md)。

### 升级到AEM Communities 6.5 {#upgrading-to-aem-communities}

在升级到AEM 6.5 Communities时，如果需要保留预先存在的UGC，则应该根据AEM 5.6.1或AEM 6.0社区使用的是Adobe按需存储还是UGC本地存储来采取步骤。

有关详细信息，请访问[升级到AEM Communities 6.5](/help/communities/upgrade.md)。
