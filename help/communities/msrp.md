---
title: MSRP - MongoDB存储资源提供程序
description: 设置AEM Communities以使用关系数据库作为其公用存储
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 0%

---

# MSRP - MongoDB存储资源提供程序 {#msrp-mongodb-storage-resource-provider}

## 关于MSRP {#about-msrp}

当AEM Communities配置为使用MSRP作为其公用存储时，用户生成的内容(UGC)可从所有创作和发布实例访问，而无需同步或复制。

另请参阅[SRP选项的特性](working-with-srp.md#characteristics-of-srp-options)和[推荐的拓扑](topologies.md)。

## 要求 {#requirements}

* [MongoDB](https://www.mongodb.org/)：

   * 版本2.6或更高版本
   * 无需配置蒙戈或分片
   * 强烈建议使用[副本集](#mongoreplicaset)
   * 可以在与AEM相同的主机上运行或远程运行

* [Apache Solr](https://lucene.apache.org/solr/)：

   * Solr版本7.0
   * Solr需要Java 1.7或更高版本
   * 无需服务
   * 运行模式的选择：
      * 独立模式
      * [SolrCloud模式](solr.md#solrcloud-mode) （建议用于生产环境）
   * 多语言搜索(MLS)的选择：
      * [安装标准MLS](solr.md#installing-standard-mls)
      * [安装高级MLS](solr.md#installing-advanced-mls)

## MongoDB配置 {#mongodb-configuration}

### 选择MSRP {#select-msrp}

[存储配置控制台](srp-config.md)允许选择默认存储配置，该配置标识要使用的SRP实现。

在创作时，要访问Storage Configuration控制台，请执行以下操作：

* 从全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社区]** > **[!UICONTROL 存储配置]**。

![msrp](assets/msrp.png)

* 选择&#x200B;**[!UICONTROL MongoDB存储资源提供程序(MSRP)]**
* **[!UICONTROL mongoDB配置]**

   * **[!UICONTROL mongoDB URI]**

     *默认*： mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB数据库]**

     *默认*：社区

   * **[!UICONTROL mongoDB UGC收藏集]**

     *默认值*：内容

   * **[!UICONTROL mongoDB附件集合]**

     *默认值*：附件

* **[!UICONTROL SolrConfiguration]**

   * **[Zookeeper](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)主机**

     在使用外部ZooKeeper在[SolrCloud模式](solr.md#solrcloud-mode)中运行时，请将此值设置为ZooKeeper的`HOST:PORT`，如&#x200B;*my.server.com:2181*

     对于ZooKeeper Ensemble，请输入逗号分隔的`HOST:PORT`值，如&#x200B;*host1:2181，host2:2181*

     如果使用内部ZooKeeper以独立模式运行Solr，则保留为空。
     *默认值*： *&lt;空白>*

      * **[!UICONTROL Solr URL]**
用于在独立模式下与Solr通信的URL。
如果以SolrCloud模式运行，则保留为空。
        *默认值*： https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr收藏集]**
Solr收藏集名称。
        *默认值*： collection1

* 选择&#x200B;**[!UICONTROL 提交]**

>[!NOTE]
>
>不应将默认为名称`communities`的mongoDB数据库设置为用于[节点存储或数据（二进制）存储](../../help/sites-deploying/data-store-config.md)的数据库的名称。 另请参阅AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md)中的[存储元素。

### MongoDB副本集 {#mongodb-replica-set}

对于生产环境，强烈建议设置一个副本集，即MongoDB服务器群集，用于实施主辅助复制和自动故障切换。

要了解有关副本集的更多信息，请访问MongoDB的[复制](https://docs.mongodb.org/manual/replication/)文档。

若要使用副本集并了解如何定义应用程序与MongoDB实例之间的连接，请访问MongoDB的[连接字符串URI格式](https://docs.mongodb.org/manual/reference/connection-string/)文档。

#### 连接到复制副本集的Url示例  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 配置 {#solr-configuration}

可以使用不同的集合在节点存储(Oak)和公用存储(MSRP)之间共享Solr安装。

如果Oak和MSRP集合都大量使用，则可能会出于性能原因安装第二个Solr。

对于生产环境，[SolrCloud模式](solr.md#solrcloud-mode)比独立模式（单个本地Solr设置）提供了更好的性能。

有关配置详细信息，请参阅SRP](solr.md)的[Solr配置。

### 升级 {#upgrading}

如果从使用MSRP配置的早期版本升级，则需要：

1. 执行[升级到AEM Communities](upgrade.md)
1. 安装新的Solr配置文件
   * 对于[标准MLS](solr.md#installing-standard-mls)
   * 对于[高级MLS](solr.md#installing-advanced-mls)
1. 重新索引MSRP
请参阅[MSRP重新索引工具](#msrp-reindex-tool)部分

## 发布配置 {#publishing-the-configuration}

MSRP必须标识为所有创作实例和发布实例上的公用存储。

要使相同的配置在发布环境中可用，请登录您的创作实例并按照以下步骤操作：

* 从主菜单导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 复制]**。
* 选择&#x200B;**[!UICONTROL 激活树]**
* **[!UICONTROL 起始路径]**：
   * 浏览到`/etc/socialconfig/srpc/`
* 选择&#x200B;**[!UICONTROL 激活]**

## 管理用户数据 {#managing-user-data}

有关&#x200B;*用户*、*用户配置文件*&#x200B;和&#x200B;*用户组*&#x200B;的信息（通常在发布环境中输入），请访问

* [用户同步](sync.md)
* [管理用户和用户组](users.md)

## MSRP重新索引工具 {#msrp-reindex-tool}

安装新配置文件或修复损坏的Solr索引时，存在HTTP端点可为MSRP重新索引Solr。

使用此工具，MongoDB是MSRP的&#x200B;*truth*&#x200B;的源；只需备份MongoDB。

可以重新索引整个UGC树，也可以只重新索引特定的子树，如*path *data参数所指定。

此工具可以使用cURL或任何其他HTTP工具从命令行运行。

重新索引时，内存和性能之间存在一个权衡，该权衡由*batchSize *data参数控制，该参数指定每个批次重新索引的UGC记录数。

合理的缺省值为5000：

* 如果内存有问题，请指定较小的数字
* 如果速度有问题，请指定较大的数字以提高速度

### 使用cURL命令运行MSRP重新索引工具 {#running-msrp-reindex-tool-using-curl-command}

以下cURL命令显示HTTP请求重新索引存储在MSRP中的UGC所需的内容。

基本格式为：

cURL -u *登录* -d *数据* *重新索引 — url*

*登录* = administrator-id：password
例如：admin：admin

*数据* = &quot;batchSize=*大小*&amp;path=*路径&quot;*

*大小* =每个操作要重新索引的UGC条目数
`/content/usergenerated/asi/mongo/`

*path* =要重新索引的UGC树的根位置

* 要重新索引所有UGC，请指定的`asipath`属性值
  `/etc/socialconfig/srpc/defaultconfiguration`
* 若要将索引限制为某个UGC，请指定`asipath`的子树

*reindex-url* =用于重新索引SRP的终结点
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>如果您[正在重新索引DSRP Solr](dsrp.md)，则URL为&#x200B;**/services/social/datastore/rdb/reindex**

### MSRP重新索引示例 {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## 如何演示MSRP {#how-to-demo-msrp}

要为演示或开发环境设置MSRP，请参阅[如何为演示设置MongoDB](demo-mongo.md)。

## 疑难解答 {#troubleshooting}

### UGC在MongoDB中可见 {#ugc-not-visible-in-mongodb}

通过检查存储选项的配置，确保MSRP已配置为默认提供程序。 默认情况下，存储资源提供程序为JSRP。

在所有创作和发布AEM实例上，重新访问[存储配置控制台](srp-config.md)或检查AEM存储库：

* 在JCR中，如果[/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * 不包含[srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)节点，这意味着存储提供程序是JSRP。
   * 如果srpc节点存在并且包含节点[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，则defaultconfiguration的属性应将MSRP定义为默认提供程序。

### 升级后UGC消失 {#ugc-disappears-after-upgrade}

如果从现有的AEM Communities 6.0站点进行升级，则在升级到AEM Communities 6.3后，必须转换任何预先存在的UGC以符合[SRP](srp.md) API所需的结构。

GitHub上为此提供了一个开源工具：

* [AEM Communities UGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

可以自定义迁移工具，以便将AEM Social早期版本的UGC导出到AEM Communities 6.1或更高版本中。

### 错误 — 未定义的字段provider_id {#error-undefined-field-provider-id}

如果日志中显示以下错误，则表示Solr架构文件未正确配置。

#### JsonMappingException：未定义的字段provider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

若要解决此错误，在遵循[安装标准MLS](solr.md#installing-standard-mls)的说明时，请确保：

* 已将XML配置文件复制到正确的Solr位置。
* 在新的配置文件替换了现有配置文件之后，Solr已重新启动。

### 与MongoDB的安全连接失败 {#secure-connection-to-mongodb-fails}

如果由于缺少类定义而尝试与MongoDB服务器建立安全连接失败，则需要更新可从公共maven存储库中找到的MongoDB驱动程序包`mongo-java-driver`。

1. 从[https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar)（版本2.13.2或更高版本）下载驱动程序。
1. 将捆绑包复制到AEM实例的“crx-quickstart/install”文件夹中。
1. 重新启动AEM实例。

## 资源 {#resources}

* [带有MongoDB的AEM](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB文档](https://docs.mongodb.org/)
