---
title: DSRP — 关系数据库存储资源提供程序
description: 设置AEM Communities以使用关系数据库作为其公用存储
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# DSRP — 关系数据库存储资源提供程序 {#dsrp-relational-database-storage-resource-provider}

## 关于DSRP {#about-dsrp}

当AEM Communities配置为使用关系数据库作为其公用存储时，用户生成的内容(UGC)可从所有创作和发布实例访问，而无需同步或复制。

另请参阅[SRP选项的特性](working-with-srp.md#characteristics-of-srp-options)和[推荐的拓扑](topologies.md)。

## 要求 {#requirements}

* [MySQL](#mysql-configuration)，关系数据库。
* [Apache Solr](#solr-configuration)，搜索平台。

>[!NOTE]
>
>默认存储配置现在存储在conf路径(`/conf/global/settings/community/srpc/defaultconfiguration`)中，而不是`etc`路径(`/etc/socialconfig/srpc/defaultconfiguration`)中。 建议您按照[迁移步骤](#zerodt-migration-steps)操作，以使defaultsrp按预期工作。

## 关系数据库配置 {#relational-database-configuration}

### MySQL配置 {#mysql-configuration}

通过使用不同的数据库（模式）名称和不同的连接（服务器：端口），可以在同一连接池中的启用功能和公用存储(DSRP)之间共享MySQL安装。

有关安装和配置详细信息，请参阅[DSRP的MySQL配置](dsrp-mysql.md)。

### Solr 配置 {#solr-configuration}

可以使用不同的集合在节点存储(Oak)和公用存储(SRP)之间共享Solr安装。

如果Oak和SRP集合都大量使用，则可能会出于性能原因安装第二个Solr。

对于生产环境，SolrCloud模式比独立模式（单个本地Solr设置）提供了更好的性能。

有关安装和配置详细信息，请参阅SRP的[Solr配置](solr.md)。

### 选择DSRP {#select-dsrp}

[存储配置控制台](srp-config.md)允许选择默认存储配置，该配置标识要使用的SRP实现。

在作者中，访问Storage Configuration控制台

* 使用管理员权限登录
* 从&#x200B;**主菜单**

   * 选择&#x200B;**[!UICONTROL 工具]** （从左侧窗格）
   * 选择&#x200B;**[!UICONTROL 社区]**
   * 选择&#x200B;**[!UICONTROL 存储配置]**

      * 例如，结果位置为： [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)

     >[!NOTE]
     >
     >默认存储配置现在存储在conf路径(`/conf/global/settings/community/srpc/defaultconfiguration`)中      而不是`etc`路径(`/etc/socialconfig/srpc/defaultconfiguration`)。 建议您按照[迁移步骤](#zerodt-migration-steps)操作，以使defaultsrp按预期工作。

  ![dsrp-config](assets/dsrp-config.png)

* 选择&#x200B;**[!UICONTROL 数据库存储资源提供程序(DSRP)]**
* **数据库配置**

   * **[!UICONTROL JDBC数据源名称]**

     为MySQL连接指定的名称必须与[JDBC OSGi配置](dsrp-mysql.md#configurejdbcconnections)中输入的名称相同

     *默认*：社区

   * **[!UICONTROL 数据库名称]**

     为[init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)脚本中的架构指定的名称

     *默认*：社区

* **SolrConfiguration**

   * **[Zookeeper](https://solr.apache.org/guide/6_6/using-zookeeper-to-manage-configuration-files.html)主机**

     如果使用内部ZooKeeper运行Solr，则将此值留空。 否则，在使用外部ZooKeeper的[SolrCloud模式](solr.md#solrcloud-mode)中运行时，请将此值设置为ZooKeeper的URI，如&#x200B;*my.server.com:80*

     *默认*： *&lt;空白>*

   * **[!UICONTROL Solr URL]**

     *默认*： https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr收藏集]**

     *默认值*： collection1

* 选择&#x200B;**[!UICONTROL 提交]**。

### Defaultsrp的零停机迁移步骤 {#zerodt-migration-steps}

要确保defaultsrp页面[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)按预期工作，请执行以下步骤：

1. 将`/etc/socialconfig`处的路径重命名为`/etc/socialconfig_old`，以便系统配置回退到jsrp（默认）。
1. 转到配置jsrp的defaultsrp页面[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)。 单击&#x200B;**[!UICONTROL 提交]**&#x200B;按钮，以便在`/conf/global/settings/community/srpc`创建新的默认配置节点。
1. 删除已创建的默认配置`/conf/global/settings/community/srpc/defaultconfiguration`。
1. 复制旧配置`/etc/socialconfig_old/srpc/defaultconfiguration`以替换上一步骤中删除的节点(`/conf/global/settings/community/srpc/defaultconfiguration`)。
1. 删除旧`etc`节点`/etc/socialconfig_old`。

## 发布配置 {#publishing-the-configuration}

必须将DSRP标识为所有创作实例和发布实例上的公用存储。

要使相同的配置在发布环境中可用，请执行以下操作：

* 对于作者：

   * 从主菜单导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 复制]**
   * 双击&#x200B;**[!UICONTROL 激活树]**
   * **起始路径**：

      * 浏览到`/etc/socialconfig/srpc/`

   * 确保未选择`Only Modified`。
   * 选择&#x200B;**[!UICONTROL 激活]**。

## 管理用户数据 {#managing-user-data}

有关&#x200B;*用户*、*用户配置文件*&#x200B;和&#x200B;*用户组*&#x200B;的信息（通常在发布环境中输入），请访问：

* [用户同步](sync.md)
* [管理用户和用户组](users.md)

## 为DSRP重新索引Solr {#reindexing-solr-for-dsrp}

要重新索引DSRP Solr，请按照[重新索引MSRP](msrp.md#msrp-reindex-tool)的文档进行操作，但是在重新索引DSRP时，请改用此URL： **/services/social/datastore/rdb/reindex**

例如，用于重新索引DSRP的curl命令如下所示：

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
