---
title: JSRP - JCR存储资源提供程序
seo-title: JSRP - JCR存储资源提供程序
description: JSRP通常最适合一个发布实例和一个创作实例的演示或开发环境
seo-description: JSRP通常最适合一个发布实例和一个创作实例的演示或开发环境
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# JSRP - JCR存储资源提供程序 {#jsrp-jcr-storage-resource-provider}

## 关于JSRP {#about-jsrp}

当AEM Communities使用JSRP作为其存储选项（默认）时，社区内容存储在JCR中，用户生成的内容(UGC)只能从发布到的创作或发布实例访问。

由于部署的简单性，JSRP通常最适合一个发布实例和一个创作实例的演示或开发环境。

另请参阅[SRP选项的特性](working-with-srp.md#characteristics-of-srp-options)和[推荐的拓扑](topologies.md)。

## 配置 {#configuration}

### 选择JSRP {#select-jsrp}

默认情况下，JSRP是UGC的存储选项。

[存储配置控制台](srp-config.md)允许选择默认存储配置，该配置标识要使用的SRP实施。

在创作环境中，要访问存储配置控制台

* 从全局导航：**[!UICONTROL 工具]** > **[!UICONTROL 社区]** > **[!UICONTROL 存储配置]**

* 选择&#x200B;**[!UICONTROL JCR存储资源提供程序(JSRP)]**

* 选择&#x200B;**[!UICONTROL Submit]**

![jsrp-configuration](assets/jsrp-configuration.png)

### 发布配置 {#publishing-the-configuration}

虽然JSRP是默认配置，但要确保在发布环境中设置相同的配置：

* 从全局导航：**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]**
* 选择&#x200B;**[!UICONTROL 激活树]** > **[!UICONTROL 启动路径]**:

   * 浏览到`/conf/global/settings/community/srpc/`

* 选择&#x200B;**[!UICONTROL 激活]**

## 管理用户数据 {#managing-user-data}

有关&#x200B;*用户*、*用户配置文件*&#x200B;和&#x200B;*用户组*&#x200B;的信息，请访问：

* [用户同步](sync.md)
* [管理用户和用户组](users.md)

## 疑难解答 {#troubleshooting}

### UGC在JCR中不可见 {#ugc-not-visible-in-jcr}

通过检查存储选项的配置，确保JSRP配置为默认提供程序。 默认情况下，存储资源提供程序为JSRP。

在所有创作和发布AEM实例上，重新访问存储配置控制台或检查AEM存储库：

* 在JCR中，如果[/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * 不包含[srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc)节点，表示存储提供程序是JSRP。
   * 如果srpc节点存在并且包含节点[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)，则默认配置的属性应将JSRP定义为默认提供程序。

### UGC在创作实例上不可见 {#ugc-not-visible-on-author-instance}

这不是错误。 JSRP的一个特点是，在发布环境中输入的社区内容仅在发布环境中可见。

### UGC在发布实例上不可见 {#ugc-not-visible-on-publish-instance}

如果单个发布实例或已部署发布群集，请按照[UGC Not Visible in JCR](#ugc-not-visible-in-jcr)的说明操作。

如果部署了发布场，则JSRP的一个特点是，社区内容仅在发布到的发布实例上可见。

要使UGC从任何发布实例中可见，需要发布群集。
