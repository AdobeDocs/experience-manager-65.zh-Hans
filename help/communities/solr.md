---
title: SRP的Solr配置
description: Apache Solr安装可以通过使用不同的集合在节点存储(Oak)和公用存储(SRP)之间共享
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: a9fc9c06-b9e6-4a5e-ab5e-0930ecd4b51b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 2%

---

# SRP的Solr配置 {#solr-configuration-for-srp}

## 适用于AEM平台的Solr {#solr-for-aem-platform}

可以使用其他收藏集在[节点存储](../../help/sites-deploying/data-store-config.md) (Oak)和[公用存储](working-with-srp.md) (SRP)之间共享[Apache Solr](https://solr.apache.org/)安装。

如果Oak和SRP集合都大量使用，则可能会出于性能原因安装第二个Solr。

对于生产环境，[SolrCloud模式](#solrcloud-mode)比独立模式（单个本地Solr设置）提供了更好的性能。

### 要求 {#requirements}

下载并安装Apache Solr：

* [版本7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr需要Java™ 1.7或更高版本
* 无需服务
* 运行模式的选择：

   * 独立模式
   * [SolrCloud模式](#solrcloud-mode) （建议用于生产环境）

* 多语言搜索(MLS)的选择

   * [安装标准MLS](#installing-standard-mls)
   * [安装高级MLS](#installing-advanced-mls)

## SolrCloud模式 {#solrcloud-mode}

建议在生产环境中使用[SolrCloud](https://solr.apache.org/guide/6_6/solrcloud.html)模式。 在SolrCloud模式下运行时，必须先安装和配置SolrCloud，然后才能安装多语言搜索(MLS)。

建议按照SolrCloud的说明进行安装：

* 同一服务器上的3个SolrCloud节点。
* 外部Apache ZooKeeper。

还建议配置JVM以调整内存使用量和垃圾收集。

### JVM配置示例 {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### SolrCloud设置命令 {#solrcloud-setup-commands}

在SolrCloud模式下运行时，在MLS安装之前，需要使用和了解以下SolrCloud安装命令。

#### 1.将配置上传到ZooKeeper {#upload-a-configuration-to-zookeeper}

引用：
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

用法：
sh 。/scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *服务器：端口* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2.创建收藏集 {#create-a-collection}

引用：
[https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create](https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create)

用法：
./bin/solr创建 \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *端口*\
-s *分片数* \
-rf *副本数*

#### 3.将收藏集链接到配置集 {#link-a-collection-to-a-configuration-set}

将收藏集链接到已上传到ZooKeeper的配置。

引用：
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

用法：
sh 。/scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *服务器：端口* \
-collection *mycollection-name* \
-confname *myconfig-name*

### 标准和高级MLS的比较 {#comparison-of-standard-and-advanced-mls}

AEM Communities的多语言搜索(MLS)是为Solr平台而构建的，旨在跨所有受支持的语言（包括英语）提供改进的搜索。

适用于AEM Communities的MLS可用作标准MLS或高级MLS。 标准MLS仅包含Solr配置设置，并排除任何插件或资源文件。 高级MLS是更全面的解决方案，包括Solr配置设置以及插件和相关资源

标准MLS包括用于搜索以下语言内容的增强功能：

* 英语：改进了尝试匹配单词派生项的词干分析。
* 日语：改进了半角字符的日语标记化。

高级MLS包括针对以下语言的内容搜索的增强功能：

* 英语：用左撇子替换词干。
* 德语：添加了分解。
* 法语：添加了版本处理。
* 中文（简体）：添加了更智能的标记器。
* 各种语言：添加了词干器、停用词列表和规范化程序。

总之，高级MLS支持以下33种语言。

| 阿拉伯语 | 德语 | 挪威语 |
|---|---|---|
| 保加利亚语 | 希腊语 | 波兰语 |
| 中文（简体） | 海地克里奥尔语 | 葡萄牙语 |
| 中文(繁体) | 希伯来语 | 罗马尼亚语 |
| 捷克语 | 匈牙利语 | 俄语 |
| 丹麦语 | 印尼语 | 斯洛伐克语 |
| 荷兰语 | 意大利语 | 斯洛文尼亚语 |
| 英语 | 日语 | 西班牙语 |
| 爱沙尼亚语 | 朝鲜语 | 瑞典语 |
| 芬兰语 | 拉脱维亚语 | 泰语 |
| 法语 | 立陶宛语 | 土耳其语 |

#### AEM 6.1 Solr搜索、标准MLS和高级MLS的比较 {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**注意**： AEM 6.1引用AEM 6.1 Communities FP3及更早版本。

![compare-solr-mls](assets/compare-solr-mls.png)

### 安装标准MLS {#installing-standard-mls}

对于SRP集合（MSRP或DSRP），要支持标准多语言搜索(MLS)，必须修改两个Solr配置文件：

* **schema.xml**
* **solrconfig.xml**

适用于Solr 4.10的标准MLS文件(schema.xml、solrconfig.xml)。

适用于Solr 5.x的标准MLS文件(schema.xml、solrconfig.xml)。

标准MLS文件存储在AEM存储库中。

**注意**：虽然Solr文件存储在msrp/文件夹中，但它们也用于DSRP（无需更改）。

**下载说明**：将`solrX`替换为`solr4`或`solr5`（如果适用）。

1. 使用CRXDE|Lite，查找：

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. 下载到部署Solr的本地服务器。

   * 找到`jcr:content`节点的`jcr:data`属性。
   * 要开始下载，请选择`view`。
   * 确保使用适当的名称和编码(UTF8)保存文件。

1. 按照独立模式或SolrCloud模式的安装说明进行操作。

#### SolrCloud模式 — 标准MLS {#solrcloud-mode-standard-mls}

1. 在SolrCloud模式下安装和配置Solr。
1. 准备新配置：

   1. 创建new-config-dir*，如`solr-install-dir*/myconfig/`

   1. 将现有Solr配置目录的内容复制到&#x200B;*new-config-dir*

      * 对于Solr4：复制`solr-install-dir/example/solr/collection1/conf/`
      * 对于Solr5：复制`solr-install-dir/server/solr/configsets/data_driven_schema_configs/`

   1. 将下载的&#x200B;**schema.xml**&#x200B;和&#x200B;**solrconfig.xml**&#x200B;复制到&#x200B;*new-config-dir*&#x200B;以覆盖现有文件。

1. [将新配置](#upload-a-configuration-to-zookeeper)上传到ZooKeeper。
1. [创建集合](#create-a-collection)，并指定必要的参数，如分片数、副本数和配置名称。
1. 如果配置名称*未*在创建收藏集期间提供，则[将此新创建的收藏集](#link-a-collection-to-a-configuration-set)与上传到ZooKeeper的配置相关联。

1. 对于MSRP，请运行[MSRP重新索引工具](msrp.md#msrp-reindex-tool)，除非此安装是新的。

#### 独立模式 — 标准MLS {#standalone-mode-standard-mls}

1. 在独立模式下安装Solr。
1. 如果运行Solr5，请创建集合1（与Solr4类似）：

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. 在Solr配置目录中备份&#x200B;**schema.xml**&#x200B;和&#x200B;**solrconfig.xml**，例如：

   * 对于Solr4： `solr-install-dir/example/solr/collection1/conf/`
   * 已为Solr5创建：`solr-install-dir/server/solr/collection1/conf/`

1. 将下载的&#x200B;**schema.xml**&#x200B;和&#x200B;**solrconfig.xml**&#x200B;复制到同一目录。

1. 重新启动Solr。
1. 对于MSRP，请运行[MSRP重新索引工具](#msrpreindextool)，除非此安装是新的。

### 安装高级MLS {#installing-advanced-mls}

对于SRP集合（MSRP或DSRP）以支持高级MLS，除了自定义架构和Solr配置之外，还需要新的Solr插件。 所有必需的项目都打包到一个可下载的zip文件中。 此外，还包含安装脚本，以便在Solr以独立模式部署时使用。

要获取高级MLS包，请参阅文档部署部分中的[AEM高级MLS](deploy-communities.md#aem-advanced-mls)。

要开始使用SolrCloud或独立模式的安装，请执行以下操作：

* 将AEM-SOLR-MLS zip存档下载到托管Solr的服务器。
* 解压缩存档。

#### SolrCloud模式 — 高级MLS {#solrcloud-mode-advanced-mls}

安装说明 — 请注意与Solr4和Solr5的一些区别：

1. 在SolrCloud模式下安装和配置Solr。
1. 将高级MLS包的内容提取到磁盘。 内容应包括：

   * **schema.xml**
   * **solrconfig.xml**
   * **停用词/**&#x200B;文件夹
   * **配置文件/**&#x200B;文件夹
   * **额外库/**&#x200B;文件夹

1. 准备新配置：

   1. 创建&#x200B;*new-config-dir*

      * 如`solr-install-dir/myconfig/`
      * 创建子文件夹`stopwords/`和`lang/`

   1. 将现有Solr配置目录的内容复制到&#x200B;*new-config-dir*

      * 对于Solr4：复制`solr-install-dir/example/solr/collection1/conf/`
      * 对于Solr5：复制`solr-install-dir/server/solr/configsets/data_driven_schema_configs/`

   1. 将提取的&#x200B;**schema.xml**&#x200B;和&#x200B;**solrconfig.xml**&#x200B;复制到&#x200B;*new-config-dir*&#x200B;以覆盖现有文件。
   1. 对于Solr5：将`solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt`复制到`new-config-dir/lang/`
   1. 将提取的&#x200B;**stopwords/**&#x200B;文件夹复制到&#x200B;*new-config-dir*，从而生成`new-config-dir/stopwords/*.txt`

1. [将新配置](#upload-a-configuration-to-zookeeper)上传到ZooKeeper
1. 复制新的&#x200B;**配置文件/**&#x200B;文件夹……

   * 对于Solr4：复制到每个节点的资源/文件夹
   * 对于Solr5：复制到每个Solr安装的服务器/资源/文件夹。 如果所有节点都位于同一个Solr安装目录中，则仅执行此步骤一次。

1. 在SolrCloud中每个节点的solr-home目录（包含solr.xml）中创建一个&#x200B;**lib/**&#x200B;文件夹。 将jar从以下位置复制到每个节点上的新库/文件夹：

   * 从高级MLS包提取的&#x200B;**extra-libs/**
   * *solr-install-dir/contrib/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/analysis-extras/lib/*.jar
   * *solr-install-dir/contrib/analysis-extras/lucene-libs/*.jar

1. [创建集合](#create-a-collection)，并指定必要的参数，如分片数、副本数和配置名称。
1. 如果配置名称为&#x200B;*未在创建收藏集期间提供*，则[将此新创建的收藏集](#link-a-collection-to-a-configuration-set)与上传到ZooKeeper的配置相关联。

1. 对于MSRP，请运行[MSRP重新索引工具](#msrpreindextool)，除非此安装是新的。

#### 独立模式 — 高级MLS {#standalone-mode-advanced-mls}

安装脚本包含在高级MLS包中。

将软件包的内容提取到托管独立Solr服务器的服务器后，运行安装脚本以安装必要的资源和配置文件。

* 在独立模式下安装Solr。
* 如果运行Solr5，请创建集合1（与Solr4类似）：

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* 运行安装脚本： Install [-v 4|5] [-d solrhome] [-c collectionpath]
其中：

   * -d solrhome

     Solr安装目录

   * -c集合路径

     solr中的收藏集路径

   * — 帮助

     打印命令行选项

   * -v [4|5]

     为solr设置版本

* Solr 4.10.4的示例：

   * Install.bat -v 4 -d c：/solr-4.10.4 -c：/solr-4.10.4/example/solr/collection1

* Solr 5.4.0的示例：

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**注释**：

* 安装脚本在安装新版本之前通过附加“.orig”备份schema.xml和solrconfig.xml

### 关于solrconfig.xml {#about-solrconfig-xml}

**solrconfig.xml**&#x200B;文件控制自动提交间隔和搜索可见性，并需要测试和优化。

`<autoCommit>`：默认情况下，AutoCommit间隔（硬提交到稳定存储）设置为15秒。 搜索可见性默认为使用预提交索引。

若要更改搜索以使用更新后的索引来反映由于提交而导致的更改，请将包含的`openSearcher`更改为true。

`autoSoftCommit`：“soft”提交可确保更改可见（索引已更新），但不确保将更改同步到稳定存储（硬提交）。 结果是性能得到提高。 默认情况下，`autoSoftCommit`被禁用，包含的`maxTime`设置为–1。
