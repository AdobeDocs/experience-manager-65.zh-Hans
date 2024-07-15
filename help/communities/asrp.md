---
title: ASRP -Adobe存储资源提供程序
description: 设置AEM Communities以使用关系数据库作为其公用存储
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---

# ASRP -Adobe存储资源提供程序 {#asrp-adobe-storage-resource-provider}

## 关于ASRP {#about-asrp}

当AEM Communities配置为使用ASRP作为其公用存储时，用户生成的内容(UGC)可从所有创作和发布实例访问，而无需同步或复制。

另请参阅[SRP选项的特性](/help/communities/working-with-srp.md#characteristics-of-srp-options)和[推荐的拓扑](/help/communities/topologies.md)。

## 要求 {#requirements}

使用ASRP需要额外的许可证。

要将您的AEM Communities站点配置为使用ASRP进行UGC，请联系您的客户代表，以获得：

* 数据中心URL（ASRP终结点的地址）
* 使用者密钥
* 密钥
* 报表包ID

消费方密钥和密钥在公司的所有报表包中共享。 每个租户有一个报表包。

## 配置 {#configuration}

### 选择ASRP {#select-asrp}

[存储配置控制台](/help/communities/srp-config.md)允许选择默认存储配置，该配置标识要使用的SRP实现。

**在AEM创作实例上：**

* 在全局导航中，导航到&#x200B;**[!UICONTROL 工具> Communities > Storage Configuration]**，然后选择&#x200B;**[!UICONTROL Adobe存储资源提供程序(ASRP)]**。

![asrp-default](assets/asrp-default.png)

以下信息来自预配过程：

* **数据中心URL**：用于选择由您的客户代表标识的生产数据中心的下拉列表。
* **默认报表包**：输入默认报表包的名称。
* **使用者密钥**：输入使用者密钥。
* **密码**：输入密码。
* 选择&#x200B;**提交**。

准备发布实例：

* [复制加密密钥](#replicate-the-crypto-key)
* [复制配置](#publishing-the-configuration)

提交配置后，测试连接：

* 选择&#x200B;**测试配置**。

  对于每个创作和发布实例，测试从“存储配置”控制台到数据中心的连接。

* 确保配置文件数据的站点URL可通过[外部化链接](#externalize-links)从数据中心路由。

### 复制加密密钥 {#replicate-the-crypto-key}

使用者密钥和秘密密钥已加密。 为了使密钥正确加密/解密，所有AEM实例上的主Granite加密密钥必须相同。

按照[复制加密密钥](/help/communities/deploy-communities.md#replicate-the-crypto-key)中的说明操作。

### 将链接外部化 {#externalize-links}

有关正确的配置文件和配置文件图像链接，请确保正确[配置链接外部化器](/help/sites-developing/externalizer.md)。

请确保将域设置为可从数据中心URL（ASRP端点）路由的URL。

### 时间同步 {#time-synchronization}

为了成功通过ASRP端点进行身份验证，运行您托管的AEM Communities的计算机必须经过时间同步，例如与[网络时间协议(NTP)](https://www.ntp.org/)同步。

### 发布配置 {#publishing-the-configuration}

在所有创作实例和发布实例上，必须将ASRP标识为公用存储。

要使相同的配置在发布环境中可用，请执行以下操作：

在AEM创作实例上：

* 从主菜单导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]**
* 选择&#x200B;**激活树**
* **开始路径**：浏览到`/conf/global/settings/communities/srpc/`
* 取消选择&#x200B;**Only Modified**
* 选择&#x200B;**激活**

## 从AEM 6.0升级 {#upgrading-from-aem}

>[!CAUTION]
>
>如果在已发布的社区站点上启用ASRP，则任何已存储在[JCR](/help/communities/jsrp.md)中的UGC将不再可见，因为本地存储和云存储之间没有数据同步。

**`AEM Communities Extension`**&#x200B;之前在AEM 6.0 social communities中引入为cloud service。 从AEM 6.1 Communities开始，无需云配置，只需从[存储配置控制台](/help/communities/srp-config.md)中选择ASRP。

由于新的存储结构，从社交社区升级到社区时需要遵循[升级](/help/communities/upgrade.md#adobe-cloud-storage)说明。

## 管理用户数据 {#managing-user-data}

有关&#x200B;*用户*、*用户配置文件*&#x200B;和&#x200B;*用户组*&#x200B;的信息（通常在发布环境中输入），请访问

* [用户同步](/help/communities/sync.md)
* [管理用户和用户组](/help/communities/users.md)

## 疑难解答 {#troubleshooting}

### 升级后UGC消失 {#ugc-disappears-after-upgrade}

如果从现有AEM 6.0社交社区站点升级，请确保遵循[升级说明](/help/communities/upgrade.md#adobe-cloud-storage)，否则UGC似乎已丢失。

### 身份验证错误 {#authentication-errors}

如果收到针对数据中心URL的身份验证错误，并且AEM error.log包含有关过时时间戳的消息，请验证是否正在进行时间同步。

使用诸如[网络时间协议(NTP)](https://www.ntp.org/)之类的工具来时间同步所有AEM创作和发布服务器。

### 新内容未出现在搜索中 {#new-content-does-not-appear-in-searches}

Adobe云存储基础结构使用&#x200B;*最终一致性*&#x200B;来实现其扩展和性能目标。 因此，新内容不会立即可用，并且需要几秒钟才能显示在搜索结果中。

在监视影响最终一致性的间隔时，如果新内容在搜索中需要超过几秒的时间才能显示，请联系您的客户代表。

### UGC在ASRP中不可见 {#ugc-not-visible-in-asrp}

通过检查存储选项的配置，确保已将ASRP配置为默认提供程序。 默认情况下，存储资源提供程序是JSRP，而不是ASRP。

在所有创作和发布AEM实例上，重新访问“存储配置”控制台，或检查AEM存储库。

在JCR中，如果[/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)：

* 不包含[srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp)节点，这意味着存储提供程序是JSRP。
* 如果srpc节点存在并包含[defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration)节点，则defaultconfiguration的属性将ASRP定义为默认提供程序。
