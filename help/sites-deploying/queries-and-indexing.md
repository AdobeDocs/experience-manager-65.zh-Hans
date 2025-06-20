---
title: Oak查询和索引
description: 了解如何使用Adobe Experience Manager (AEM) 6.5配置索引。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: eeeb31d81c22f8dace7a170953bf45a709f5ac73
workflow-type: tm+mt
source-wordcount: '3051'
ht-degree: 0%

---

# Oak查询和索引{#oak-queries-and-indexing}

>[!NOTE]
>
>本文介绍了如何在AEM 6中配置索引。 有关优化查询和索引性能的最佳实践，请参阅[有关查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

## 简介 {#introduction}

与Jackrabbit 2不同，默认情况下，Oak不为内容编制索引。 必要时必须创建自定义索引，就像传统关系数据库一样。 如果没有针对特定查询的索引，则可能会遍历许多节点。 查询可能仍然有效，但速度可能较慢。

如果Oak遇到没有索引的查询，则会打印WARN级别的日志消息：

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## 支持的查询语言 {#supported-query-languages}

Oak查询引擎支持以下语言：

* XPath（推荐）
* SQL-2
* SQL（已弃用）
* JQOM

## 索引器类型和成本计算 {#indexer-types-and-cost-calculation}

基于Apache Oak的后端允许在存储库中插入不同的索引器。

一个索引器是&#x200B;**属性索引**，其索引定义存储在存储库本身中。

默认情况下，**Apache Lucene**&#x200B;和&#x200B;**Solr**&#x200B;的实施也可用，它们都支持全文索引。

如果没有其他索引器可用，则使用&#x200B;**遍历索引**。 这意味着内容未编制索引，将遍历内容节点以查找与查询匹配的内容。

如果一个查询有多个可用的索引器，则每个可用的索引器都会估计执行查询的成本。 然后Oak选择预计成本最低的索引器。

![chlimage_1-148](assets/chlimage_1-148.png)

上图是Apache Oak查询执行机制的高层表示形式。

首先，将查询解析为抽象语法树。 然后，检查查询并将其转换为SQL-2，后者是Oak查询的本地语言。

接下来，查询每个索引以估计查询的成本。 完成此操作后，将检索来自最便宜索引的结果。 最后，对结果进行过滤，既确保当前用户具有对结果的读取权限，又确保结果与完整的查询相匹配。

## 配置索引 {#configuring-the-indexes}

>[!NOTE]
>
>对于大型存储库，构建索引是一项耗时的操作。 这既适用于初始创建索引，也适用于重新编制索引（在更改定义后重建索引）。 另请参阅[Oak索引疑难解答](/help/sites-deploying/troubleshooting-oak-indexes.md)和[防止重新索引速度缓慢](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing)。

如果大型存储库中需要重新索引，尤其是使用MongoDB和进行全文索引时，请考虑文本预提取，并使用oak-run构建初始索引和重新索引。

索引在&#x200B;**Oak：index**&#x200B;节点下的存储库中配置为节点。

索引节点的类型必须是&#x200B;**oak：QueryIndexDefinition。**&#x200B;每个索引器都有几个配置选项作为节点属性使用。 有关详细信息，请参阅下面每种索引器类型的配置详细信息。

### 属性索引 {#the-property-index}

属性索引对于具有属性约束但不是全文的查询非常有用。 可按照以下步骤对其进行配置：

1. 通过转到`http://localhost:4502/crx/de/index.jsp`打开CRXDE
1. 在&#x200B;**oak：index**&#x200B;下创建节点
1. 为节点&#x200B;**PropertyIndex**&#x200B;命名，并将节点类型设置为&#x200B;**oak：QueryIndexDefinition**
1. 为新节点设置以下属性：

   * **类型：** `property` （类型为String）
   * **propertyNames：** `jcr:uuid`（类型为Name）

   此特定示例对`jcr:uuid`属性编制索引，该属性的作业是公开它所附加节点的通用唯一标识符(UUID)。

1. 保存更改。

属性索引具有以下配置选项：

* **type**&#x200B;属性指定索引的类型，在这种情况下，必须将其设置为&#x200B;**属性**

* **propertyNames**&#x200B;属性指示存储在索引中的属性的列表。 如果缺少节点名称，则会将节点名称用作属性名称引用值。 在此示例中，其作业是公开其节点的唯一标识符(UUID)的&#x200B;**jcr：uuid**&#x200B;属性将添加到索引中。

* **唯一**&#x200B;标志，如果设置为&#x200B;**true**，则该标志在属性索引上添加唯一性约束。

* **declaringNodeTypes**&#x200B;属性允许您指定仅应用索引的特定节点类型。
* **重新索引**&#x200B;标志，如果设置为&#x200B;**true**，将触发完整的内容重新索引。

### 有序索引 {#the-ordered-index}

Ordered索引是Property索引的扩展。 但是，它已被弃用。 必须将此类型的索引替换为[Lucene属性索引](#the-lucene-property-index)。

### Lucene全文索引 {#the-lucene-full-text-index}

AEM 6中提供了基于Apache Lucene的全文索引器。

如果配置了全文索引，则无论是否有其他条件被索引，也无论是否有路径限制，所有具有全文条件的查询都使用全文索引。

如果未配置全文索引，则具有全文条件的查询将无法按预期工作。

由于索引是通过异步后台线程更新的，因此在后台进程完成之前，某些全文搜索在很短的时间内不可用。

您可以按照以下过程配置Lucene全文索引：

1. 打开CRXDE并在&#x200B;**oak：index**&#x200B;下创建节点。
1. 为节点&#x200B;**LuceneIndex**&#x200B;命名，并将节点类型设置为&#x200B;**oak：QueryIndexDefinition**
1. 将以下属性添加到节点：

   * **类型：** `lucene` （类型为String）
   * **异步：** `async`（字符串类型）

1. 保存更改。

Lucene索引具有以下配置选项：

* 指定索引类型的&#x200B;**type**&#x200B;属性必须设置为&#x200B;**lucene**
* **async**&#x200B;属性必须设置为&#x200B;**async**。 这会将索引更新进程发送到后台线程。
* **includePropertyTypes**&#x200B;属性，用于定义索引中包含的属性类型的子集。
* 定义属性名称列表的&#x200B;**excludePropertyNames**&#x200B;属性 — 应从索引中排除的属性。
* **重新索引**&#x200B;标志，当设置为&#x200B;**true**&#x200B;时，将触发完整的内容重新索引。

### 了解全文搜索 {#understanding-fulltext-search}

例如，本节中的文档适用于Apache Lucene、Elasticsearch，以及PostgreSQL、SQLite和MySQL的全文索引。 以下示例适用于AEM/Oak/Lucene。

<b>要编制索引的数据</b>

起点是必须编制索引的数据。 以下列文档为例：

| <b>文档ID</b> | <b>路径</b> | <b>全文</b> |
| --- | --- | --- |
| 100 | /content/rubik | “鲁比克是一个芬兰品牌。” |
| 200 | /content/rubiksCube | “魔方发明于1974年。” |
| 300 | /content/cube | “立方体是一个三维物体。” |


<b>反转索引</b>

索引机制将全文拆分为名为“令牌”的单词，并构建名为“反转索引”的索引。 此索引包含文档列表，其中每个单词均显示了该索引。

短而常见的词语（也称为“停用词”）不会编制索引。 所有令牌都将转换为小写，并应用字干处理。

特殊字符（如&#x200B;*“ — ”*）未编制索引。

| <b>令牌</b> | <b>文档ID</b> |
| --- | --- |
| 194 | ...，200，... |
| 品牌 | ...，100... |
| 多维数据集 | ...，200,300，... |
| 维度 | 300 |
| 完成 | ...，100... |
| 发明 | 200 |
| 对象 | ...，300... |
| 鲁比克 | ...，100,200，... |

文档列表已排序。 这在查询时很方便。

<b>正在搜索</b>

以下是查询的示例。 请注意，所有特殊字符（如&#x200B;*&#39;*）都已替换为空格：

```
/jcr:root/content//element(\*; cq:Page)`[` jcr:contains('Rubik s Cube')`]`
```

这些单词的标记化和过滤方式与索引时相同（例如，删除单个字符单词）。 因此，在本例中，搜索的目标是：

```
+:fulltext:rubik +:fulltext:cube
```

索引将查阅这些单词的文档列表。 如果文档很多，列表可能会很大。 例如，假设它们包含以下内容：


| <b>令牌</b> | <b>文档ID</b> |
| --- | --- |
| 鲁比克 | 10、100、200、1000 |
| 多维数据集 | 30， 200， 300， 2000 |


Lucene在两个列表（或循环`n`列表，在搜索`n`个单词时）之间来回切换：

* 在“rubik”中读取将获得第一个条目：它找到10
* 在“多维数据集”中读取将获得第一个条目`>` = 10。 找不到10，则下一个为30。
* 在“rubik”中读取将获得第一个条目`>` = 30：它找到100。
* 在“多维数据集”中读取将获得第一个条目`>` = 100：它找到200。
* 在“rubik”中读取将获得第一个条目`>` = 200。 找到200个。 因此，文档200是两个术语的匹配项。 人们会记住这一点。
* 在“rubik”中读到下一个条目： 1000。
* 在“多维数据集”中读取将获取第一个条目`>` = 1000：它找到2000。
* 在“rubik”中读取将获得第一个条目`>` = 2000：列表结束。
* 最后，你可以停止搜索。

找到的唯一包含这两个术语的文档为200，如下例所示：

| 200 | /content/rubiksCube | “魔方发明于1974年。” |
| --- | --- | --- |

找到多个条目后，将按分数排序。

>[!NOTE]
>
>本节中介绍的搜索机制使用Lucene索引，而不是像Linux `grep`命令那样的部分匹配。

### Lucene属性索引 {#the-lucene-property-index}

由于&#x200B;**Oak 1.0.8**，因此Lucene可用于创建包含非全文属性约束的索引。

要实现Lucene属性索引，**fulltextEnabled**&#x200B;属性必须始终设置为false。

以以下示例查询为例：

```xml
select * from [nt:base] where [alias] = '/admin'
```

若要为上述查询定义Lucene属性索引，可通过在&#x200B;**`oak:index`下创建节点来添加以下定义：**

* **名称：** `LucenePropertyIndex`
* **类型：** `oak:QueryIndexDefinition`

创建节点后，添加以下属性：

* **类型：**

  ```xml
  lucene (of type String)
  ```

* **异步：**

  ```xml
  async (of type String)
  ```

* **已启用全文：**

  ```xml
  false (of type Boolean)
  ```

* **includePropertyNames：** `["alias"] (of type String)`

>[!NOTE]
>
>与常规属性索引相比，Lucene属性索引始终在异步模式下配置。 因此，索引返回的结果可能并不总是反映存储库的最新状态。

>[!NOTE]
>
>有关Lucene属性索引的更多具体信息，请参阅[Apache Jackrabbit Oak Lucene文档页](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### Lucene分析器 {#lucene-analyzers}

从版本1.2.0开始，Oak支持Lucene分析器。

分析器在文档被编制索引时和查询时都使用。 分析器检查字段的文本并生成令牌流。 Lucene分析器由一系列标记器和过滤类组成。

可以通过`oak:index`定义中的`analyzers`节点（类型为`nt:unstructured`）配置分析器。

索引的默认分析器配置在分析器节点的`default`子节点中。

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>有关可用分析器的列表，请参阅您使用的Lucene版本的API文档。

#### 直接指定分析器类 {#specifying-the-analyzer-class-directly}

如果要使用任何开箱即用的分析器，可以按照以下步骤对其进行配置：

1. 在`oak:index`节点下找到要与分析器一起使用的索引。

1. 在索引下，创建一个名为`default`且类型为`nt:unstructured`的子节点。

1. 将属性添加到具有以下属性的默认节点：

   * **名称：** `class`
   * **类型：** `String`
   * **值：** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   该值是要使用的分析器类的名称。

   您还可以使用可选的`luceneMatchVersion`字符串属性，将分析器设置为与特定的Lucene版本一起使用。 将其与Lucene 4.7一起使用的有效语法为：

   * **名称：** `luceneMatchVersion`
   * **类型：** `String`
   * **值：** `LUCENE_47`

   如果未提供`luceneMatchVersion`，则Oak会使用随附的Lucene版本。

1. 如果要将stopwords文件添加到分析器配置，则可以在`default`节点下创建具有以下属性的节点：

   * **名称：** `stopwords`
   * **类型：** `nt:file`

#### 通过合成创建分析器 {#creating-analyzers-via-composition}

分析器也可以基于`Tokenizers`、`TokenFilters`和`CharFilters`组成。 为此，可指定分析器并为其可选令牌化器和过滤器创建子节点，这些子节点将按列出的顺序应用。 另请参阅[https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

以此节点结构为例：

* **名称：** `analyzers`

   * **名称：** `default`

      * **名称：** `charFilters`
      * **类型：** `nt:unstructured`

         * **名称：** `HTMLStrip`
         * **名称：** `Mapping`

      * **名称：** `tokenizer`

         * **属性名称：** `name`

            * **类型：** `String`
            * **值：** `Standard`

      * **名称：** `filters`
      * **类型：** `nt:unstructured`

         * **名称：** `LowerCase`
         * **名称：** `Stop`

            * **属性名称：** `words`

               * **类型：** `String`
               * **值：** `stop1.txt, stop2.txt`

            * **名称：** `stop1.txt`

               * **类型：** `nt:file`

            * **名称：** `stop2.txt`

               * **类型：** `nt:file`

过滤器、charFilters和tokenizers的名称是通过删除工厂后缀形成的。 因此：

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory`变为`standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory`变为`Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory`变为`Stop`

工厂所需的任何配置参数均指定为相关节点的属性。

对于必须加载外部文件内容的加载停用词，可以通过为相关文件创建`nt:file`类型的子节点来提供内容。

### Solr索引 {#the-solr-index}

Solr索引的用途是全文搜索，但也可按路径、属性限制和主类型限制来索引搜索。 这意味着Oak中的Solr索引可用于任何类型的JCR查询。

AEM中的集成在存储库级别进行，因此Solr是可以在AEM随附的新存储库实施Oak中使用的可能索引之一。

它可以配置为作为远程服务器与AEM实例一起使用。

### 使用单个远程Solr服务器配置AEM {#configuring-aem-with-a-single-remote-solr-server}

AEM也可以配置为与远程Solr服务器实例配合使用：

1. 下载并解压缩最新版本的Solr。 有关如何执行此操作的更多信息，请参阅[Apache Solr安装文档](https://solr.apache.org/guide/6_6/installing-solr.html)。
1. 现在，创建两个Solr分片。 为此，您可以为解压缩Solr的文件夹中的每个分区创建文件夹：

   * 对于第一个分片，创建文件夹：

   `<solrunpackdirectory>\aemsolr1\node1`

   * 对于第二个分片，创建文件夹：

   `<solrunpackdirectory>\aemsolr2\node2`

1. 在Solr软件包中找到示例实例。 它位于包根目录中名为“`example`”的文件夹中。
1. 将以下文件夹从示例实例复制到两个分片文件夹（ `aemsolr1\node1`和`aemsolr2\node2`）：

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 在两个分片文件夹的每个文件夹中创建一个名为“`cfg`”的文件夹。
1. 将Solr和Zookeeper配置文件放入新创建的`cfg`文件夹中。

   >[!NOTE]
   >
   >有关Solr和ZooKeeper配置的更多信息，请参阅[Solr配置文档](https://cwiki.apache.org/confluence/display/solr/ConfiguringSolr)和[ZooKeeper入门指南](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html)。

1. 通过转到`aemsolr1\node1`并运行以下命令来启动支持ZooKeeper的第一个分片：

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. 转到`aemsolr2\node2`并运行以下命令以启动第二个分片：

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 两个分片都启动后，通过连接到`http://localhost:8983/solr/#/`上的Solr接口来测试所有内容均已启动并正在运行
1. 启动AEM并转到位于`http://localhost:4502/system/console/configMgr`的Web控制台
1. 在&#x200B;**Oak Solr远程服务器配置**&#x200B;下设置以下配置：

   * Solr HTTP URL： `http://localhost:8983/solr/`

1. 在&#x200B;**Oak Solr**&#x200B;服务器提供程序下的下拉列表中选择&#x200B;**远程Solr**。

1. 前往CRXDE并以管理员身份登录。
1. 在&#x200B;**oak：index**&#x200B;下创建名为&#x200B;**solrIndex**&#x200B;的节点，并设置以下属性：

   * **类型：** solr（类型为String）
   * **异步：**&#x200B;异步（字符串类型）
   * **重新索引：** true （类型为Boolean）

1. 保存更改。

#### 推荐的Solr配置 {#recommended-configuration-for-solr}

以下是基本配置的示例，该配置可以与本文所述的所有三个Solr部署一起使用。 它包含AEM中已存在的专用属性索引；请勿与其他应用程序一起使用。

要正确使用它，必须将归档文件的内容直接放在Solr主目录中。 如果有多节点部署，则它应直接位于每个节点的根文件夹下。

推荐的Solr配置文件

[获取文件](assets/recommended-conf.zip)

### AEM索引工具 {#aem-indexing-tools}

AEM 6.1还集成了AEM 6.0中存在的两个索引工具，作为Adobe Consulting Services Commons工具集的一部分：

1. **解释查询**，该工具旨在帮助管理员了解查询的执行方式；
1. **Oak索引管理器**，用于维护现有索引的Web用户界面。

现在，您可以从AEM欢迎屏幕转到&#x200B;**工具 — 操作 — 仪表板 — 诊断**&#x200B;来联系他们。

有关如何使用它们的详细信息，请参阅[操作仪表板文档](/help/sites-administering/operations-dashboard.md)。

#### 通过OSGi创建属性索引 {#creating-property-indexes-via-osgi}

ACS Commons包还公开可用于创建属性索引的OSGi配置。

您可以通过搜索“**确保Oak属性索引**”从Web控制台访问它。

![chlimage_1-150](assets/chlimage_1-150.png)

### 索引问题疑难解答 {#troubleshooting-indexing-issues}

可能会出现查询执行时间较长，且一般系统响应时间缓慢的情况。

本节提供了一系列关于必须执行哪些操作来跟踪此类问题原因的建议以及如何解决这些问题的建议。

#### 准备调试信息以供分析 {#preparing-debugging-info-for-analysis}

获取正在运行的查询所需信息的最简单方法是通过[Explain查询工具](/help/sites-administering/operations-dashboard.md#explain-query)。 这样，您就可以收集调试慢查询所需的精确信息，而无需查阅日志级别信息。 如果您知道正在调试的查询，这是可取的。

如果由于任何原因而无法执行此操作，您可以将索引日志收集到单个文件中，并使用它来解决特定问题。

#### 启用日志记录 {#enable-logging}

要启用日志记录，必须为与Oak索引和查询相关的类别启用&#x200B;**DEBUG**&#x200B;级别日志。 这些类别包括：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

**com.day.cq.search**&#x200B;类别仅适用于使用AEM提供的QueryBuilder实用工具。

>[!NOTE]
>
>请务必仅在要排除故障的查询正在运行期间，将日志设置为DEBUG 。 否则，随着时间的推移，日志中会生成许多事件。 因此，在收集到所需的日志后，请切换回INFO级别日志记录，以用于上述类别。

您可以按照以下步骤启用日志记录：

1. 将浏览器指向`https://serveraddress:port/system/console/slinglog`
1. 单击控制台下部的&#x200B;**添加新记录器**&#x200B;按钮。
1. 在新创建的行中，添加上述类别。 您可以使用&#x200B;**+**&#x200B;符号将多个类别添加到单个日志程序。
1. 从&#x200B;**日志级别**&#x200B;下拉列表中选择&#x200B;**DEBUG**。
1. 将输出文件设置为`logs/queryDebug.log`。 这会将所有DEBUG事件关联到一个日志文件中。
1. 运行查询或呈现正在使用要调试的查询的页面。
1. 执行查询后，返回日志记录控制台并将新创建的日志记录器的日志级别更改为&#x200B;**INFO**。

#### 索引配置 {#index-configuration}

查询的评估方式在很大程度上受索引配置的影响。 分析索引配置或将其发送给支持人员很重要。 您可以以内容包形式获取配置，也可以获取JSON演绎版。

通常，索引配置存储在CRXDE中的`/oak:index`节点下，您可以在以下位置获取JSON版本：

`https://serveraddress:port/oak:index.tidy.-1.json`

如果在不同位置配置了索引，请相应地更改路径。

#### MBean输出 {#mbean-output}

有时，提供与索引相关的MBean的输出以进行调试会很有用。 您可以执行以下操作来实现此目标：

1. 转到JMX控制台：
   `https://serveraddress:port/system/console/jmx`

1. 搜索以下MBean：

   * Lucene索引统计数据
   * CopyOnRead支持统计数据
   * Oak查询统计数据
   * IndexStat

1. 单击每个MBean，以便获取性能统计信息。 创建屏幕截图，或记下它们以备需要提交支持时使用。

您还可通过以下URL获取这些统计数据的JSON变体：

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

您还可以通过`https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`提供统一的JMX输出。 这将包括JSON格式的所有与Oak相关的MBean详细信息。

#### 其他详细信息 {#other-details}

您可以收集其他详细信息来帮助解决问题，例如：

1. 运行实例的Oak版本。 您可以通过打开CRXDE并查看欢迎页面右下角的版本或检查`org.apache.jackrabbit.oak-core`包的版本来查看此内容。
1. 疑难查询的QueryBuilder Debugger输出。 可在以下位置访问该调试器： `https://serveraddress:port/libs/cq/search/content/querydebug.html`
