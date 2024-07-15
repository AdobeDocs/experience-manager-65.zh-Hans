---
title: Search Essentials
description: 了解搜索功能，该功能是AEM Communities的一项基本功能。 社区还为用户生成的内容提供搜索API。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 3%

---

# Search Essentials {#search-essentials}

## 概述 {#overview}

搜索功能是Adobe Experience Manager (AEM)社区的一项基本功能。 除了[AEM平台搜索](../../help/sites-deploying/queries-and-indexing.md)功能外，AEM Communities还提供用于搜索用户生成内容(UGC)的[UGC搜索API](#ugc-search-api)。 UGC具有独特的属性，因为它与其他AEM内容和用户数据分开输入和存储。

对于Communities，通常搜索的两项内容是：

* 社区成员发布的内容

   * 它使用AEM Communities的UGC搜索API。

* 用户和用户组（用户数据）

   * 它使用AEM平台搜索功能。

文档中的此部分与创建自定义组件（用于创建或管理UGC）的开发人员有关。

## 安全和影子节点 {#security-and-shadow-nodes}

对于自定义组件，必须使用[SocialResourceUtilities](socialutils.md#socialresourceutilities-package)方法。 创建和搜索UGC的实用工具方法建立了所需的[影子节点](srp.md#about-shadow-nodes-in-jcr)，并确保该成员具有正确的请求权限。

不通过SRP实用程序管理的是与审核相关的属性。

有关用于访问UGC和ACL影子节点的实用程序方法的信息，请参阅[SRP和UGC Essentials](srp-and-ugc.md)。

## UGC搜索API {#ugc-search-api}

[UGC公用存储](working-with-srp.md)由各种存储资源提供程序(SRP)之一提供，每个提供程序可能具有不同的本地查询语言。 因此，无论选择哪个SRP，自定义代码都应使用[UGC API包](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*)中的方法，这些方法会调用适用于所选SRP的查询语言。

### ASRP搜索 {#asrp-searches}

对于[ASRP](asrp.md)，UGC存储在Adobe云中。 虽然UGC在CRX中不可见，但[审核](moderate-ugc.md)在创作环境和Publish环境中均可用。 [UGC搜索API](#ugc-search-api)的使用对于ASRP的工作方式与其他SRP的工作方式相同。

当前不存在用于管理ASRP搜索的工具。

创建可搜索的自定义属性时，必须遵循[命名要求](#naming-of-custom-properties)。

### MSRP搜索 {#msrp-searches}

对于[MSRP](msrp.md)，UGC存储在配置为使用Solr进行搜索的MongoDB中。 UGC在CRX中不可见，但[审核](moderate-ugc.md)在创作环境和Publish环境中均可用。

关于MSRP和Solr：

* AEM平台的嵌入式Solr不用于MSRP。
* 如果对AEM平台使用远程Solr，则可以与MSRP共享，但它们应使用不同的集合。
* Solr可以配置为标准搜索或多语言搜索(MLS)。
* 有关配置详细信息，请参阅用于MSRP的[Solr配置](msrp.md#solr-configuration)。

自定义搜索功能应使用[UGC搜索API](#ugc-search-api)。

创建可搜索的自定义属性时，必须遵循[命名要求](#naming-of-custom-properties)。

### JSRP搜索 {#jsrp-searches}

对于[JSRP](jsrp.md)，UGC存储在[Oak](../../help/sites-deploying/platform.md)中，并且仅在输入它的AEM Author或Publish实例的存储库中可见。

由于UGC通常在Publish环境中输入，因此对于多发布者生产系统，必须配置[发布群集](topologies.md)，而不是发布场，以便输入的内容对所有发布者可见。

对于JSRP，在Publish环境中输入的UGC在创作环境中从不可见。 因此，所有[审核](moderate-ugc.md)任务均在Publish环境中执行。

自定义搜索功能应使用[UGC搜索API](#ugc-search-api)。

#### Oak索引 {#oak-indexing}

虽然从AEM 6.2开始，Oak索引不会自动为AEM平台搜索创建，但已为AEM Communities添加这些索引，以改进性能并在显示UGC搜索结果时支持分页。

如果自定义属性正在使用中并且搜索缓慢，则必须为自定义属性创建其他索引以提高其性能。 要保持可移植性，在创建可搜索的自定义属性时，请遵循[命名要求](#naming-of-custom-properties)。

要修改现有索引或创建自定义索引，请参阅[Oak查询和索引](../../help/sites-deploying/queries-and-indexing.md)。

[Oak索引管理器](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html)可从ACS AEM Commons获得。 它提供：

* 现有索引的视图。
* 启动重新索引的功能。

要查看[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)中的现有Oak索引，位置为：

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## 索引搜索属性 {#indexed-search-properties}

### 默认搜索属性 {#default-search-properties}

以下是用于各种Communities功能的一些可搜索属性：

| **属性** | **数据类型** |
|---|---|
| isFlagged | *布尔型* |
| isSpam | *布尔型* |
| 读取 | *布尔型* |
| 影响 | *布尔型* |
| 附件 | *布尔型* |
| 情绪 | *长* |
| 已标记 | *布尔型* |
| 已添加 | *日期* |
| modifieddate | *日期* |
| 州/省 | *字符串* |
| 用户标识符 | *字符串* |
| 回复 | *长* |
| jcr:title | *字符串* |
| jcr：description | *字符串* |
| sling:resourceType | *字符串* |
| allowThreadedReply | *布尔型* |
| isDraft | *布尔型* |
| publishdate | *日期* |
| publishJobId | *字符串* |
| 已回复 | *布尔型* |
| chosenanswered | *布尔型* |
| 标记 | *字符串* |
| cq：Tag | *字符串* |
| author_display_name | *字符串* |
| location_t | *字符串* |
| 父路径 | *字符串* |
| parentTitle | *字符串* |

### 自定义属性的命名 {#naming-of-custom-properties}

添加自定义属性时，对于使用[UGC搜索API](#ugc-search-api)创建的排序和搜索可见的属性，需要&#x200B;*向属性名称添加后缀*。

后缀用于使用架构的查询语言：

* 它将该属性标识为可搜索。
* 它标识数据类型。

Solr是使用架构的查询语言的示例。

| **后缀** | **数据类型** |
|---|---|
| _b | *布尔型* |
| _dt | *日历* |
| _d | *双精度浮点数* |
| _tl | *长* |
| _s | *字符串* |
| _t | *文本* |

**注释：**

* *Text*&#x200B;是标记化的字符串，*String*&#x200B;不是。 使用&#x200B;*文本*&#x200B;进行模糊（更类似于）搜索。

* 对于多值类型，请将“s”添加到后缀，例如：

   * `viewDate_dt`：单一日期属性
   * `viewDates_dts`：日期属性列表

## 过滤器 {#filters}

包含[注释系统](essentials-comments.md)的组件除支持其端点外，还支持筛选器参数。

AND和OR逻辑的过滤器语法如下所示（在URL编码之前显示）：

* 要指定OR或使用带有逗号分隔值的过滤器参数，请执行以下操作：

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* 要指定AND使用多个过滤器参数，请执行以下操作：

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

[搜索组件](search.md)的默认实现使用此语法，如打开[社区组件指南](components-guide.md)中的搜索结果页面的URL中所示。 要试验，请浏览到[http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html)。

筛选器运算符为：

| EQ | 等于 |
|---|---|
| NE | 不等于 |
| LT | 小于 |
| LTE | 小于或等于 |
| 通用电气 | 大于 |
| GTE | 大于或等于 |
| 点赞 | 模糊匹配 |

URL引用Communities组件（资源），而不是引用放置该组件的页面，这一点很重要：

* 正确：论坛组件
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* 不正确：论坛页面
   * `/content/community-components/en/forum.social.json`

## SRP工具 {#srp-tools}

有一个Adobe Experience Cloud GitHub项目，该项目包含：

[AEM Communities SRP工具](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

此存储库包含用于管理SRP中数据的工具。

目前，有一个servlet可以从任何SRP中删除所有UGC。

例如，要删除ASRP中的所有UGC，请执行以下操作：

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## 疑难解答 {#troubleshooting}

### Solr查询 {#solr-query}

要帮助解决Solr查询的问题，请为以下对象启用DEBUG日志记录

`com.adobe.cq.social.srp.impl.SocialSolrConnector`。

实际Solr查询在调试日志中显示编码的URL：

对solr的查询是： `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

`q`参数的值为查询。 解码URL编码后，可将查询传递到Solr管理员查询工具进行进一步调试。

## 相关资源 {#related-resources}

* [社区内容存储](working-with-srp.md) — 讨论UGC公用存储的可用SRP选项。
* [存储资源提供程序概述](srp.md) — 简介和存储库使用情况概述。
* [使用SRP访问UGC](accessing-ugc-with-srp.md) — 编码准则。
* [SocialUtils重构](socialutils.md) — 用于替换SocialUtils的SRP的实用工具方法。
* [搜索和搜索结果组件](search.md) — 正在向模板添加UGC搜索功能。
