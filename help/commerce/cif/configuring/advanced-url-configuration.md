---
title: 高级URL配置
description: 了解如何自定义产品和类别页面的URL。 这允许实施优化搜索引擎的URL并促进发现。
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 3%

---

# 高级URL配置 {#url}

>[!NOTE]
>
>搜索引擎优化 (SEO) 已成为许多营销人员关注的重点。因此，必须解决许多AEM项目中的SEO问题。 请参阅[SEO和URL管理最佳实践](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html)以了解更多信息。

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)提供了高级配置以自定义产品和类别页面的URL。 许多实施都会自定义这些URL，以实现搜索引擎优化(SEO)。 以下视频详细介绍如何配置[Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)的`UrlProvider`服务和功能以自定义产品和类别页面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 配置 {#configuration}

要根据SEO要求和需要配置`UrlProvider`服务，项目必须提供“CIF URL提供程序配置”的OSGI配置。

>[!NOTE]
>
>自AEM CIF核心组件版本2.0.0开始，URL提供程序配置仅提供预定义的url格式，而不提供1.x版本中已知的自由文本可配置格式。 此外，使用选择器在URL中传递数据的方法已替换为后缀。

### 产品页面URL格式 {#product}

这会配置产品页面的URL，并支持以下选项：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`（默认）
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

如果存在[Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}`已替换为`/content/venia/us/en/products/product-page`
* `{{sku}}`被产品的SKU替换，例如，`VP09`
* `{{url_key}}`被产品的`url_key`属性替换，例如`lenora-crochet-shorts`
* `{{url_path}}`被产品的`url_path`替换，例如`venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}`被当前选定的变体替换，例如`VP09-KH-S`

由于`url_path`已被弃用，因此预定义产品URL格式将使用产品的`url_rewrites`，并在`url_path`不可用时选择具有最多路径区段的格式作为替代格式。

对于上述示例数据，使用默认URL格式的产品变体URL类似于`/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`。

### 类别页面URL格式 {#product-list}

这将配置类别或产品列表页面的URL，并支持以下选项：

* `{{page}}.html/{{url_path}}.html`（默认）
* `{{page}}.html/{{url_key}}.html`

如果存在[Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}`已替换为`/content/venia/us/en/products/category-page`
* `{{url_key}}`被类别的`url_key`属性替换
* `{{url_path}}`被类别的`url_path`替换

对于上述示例数据，使用默认URL格式设置的类别页面URL类似于`/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`。

>[!NOTE]
> 
>`url_path`是产品或类别祖先的`url_keys`与产品或类别的`url_key`的串联，由`/`斜杠分隔。

### 特定类别/产品页面 {#specific-pages}

只能为目录的特定类别或产品子集创建[多个类别和产品页面](multi-template-usage.md)。

`UrlProvider`预配置为在创作层实例上生成指向此类页面的深层链接。 这对于编辑器非常有用，编辑器使用预览模式浏览站点，导航到特定产品或类别页面，然后切换回编辑模式以编辑页面。

另一方面，在发布层实例中，目录页面URL应保持稳定，以免在搜索引擎排名方面失去优势。 因此，默认情况下，发布层实例不会呈现指向特定目录页面的深层链接。 若要更改此行为，可以将&#x200B;_CIF URL提供程序特定页面策略_&#x200B;配置为始终生成特定页面URL。

## 自定义URL格式 {#custom-url-format}

提供项目可以实现[`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html)或[`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html)服务接口的自定义URL格式，并将该实现注册为OSGI服务。 这些实施（如果可用）会替换已配置的预定义格式。 如果注册了多个实施，则服务排名较高的实施将替换服务排名较低的实施。

自定义URL格式实施必须实施一对方法，以便根据给定参数构建URL，并解析URL以分别返回相同的参数。

## 与Sling映射组合 {#sling-mapping}

除了`UrlProvider`之外，还可以配置[Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)以重写并处理URL。 AEM Archetype项目还提供了[示例配置](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)，以便为端口4503（发布）和80(Dispatcher)配置一些Sling映射。

## 与AEM Dispatcher相结合 {#dispatcher}

使用带有`mod_rewrite`模块的AEM Dispatcher HTTP Server也可以实现URL重写。 [AEM项目原型](https://github.com/adobe/aem-project-archetype)提供了一个引用AEM Dispatcher配置，该配置已包含所生成大小的基本[重写规则](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)。

## 示例

[Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)项目包含示例配置，用于演示产品和类别页面的自定义URL的使用情况。 这使得每个项目都可以根据其SEO需求，为产品和类别页面设置单独的URL模式。 使用如上所述的CIF `UrlProvider`和Sling映射的组合。

>[!NOTE]
>
>此配置必须使用项目使用的外部域进行调整。 Sling映射基于主机名和域工作。 因此，此配置默认处于禁用状态，必须在部署之前启用。 为此，请根据使用的域名重命名`ui.content/src/main/content/jcr_root/etc/map.publish/https`中的Sling映射`hostname.adobeaemcloud.com`文件夹，并通过将`resource.resolver.map.location="/etc/map.publish"`添加到项目的`JcrResourceResolver`配置中来启用此配置。

## 其他资源

* [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)
* [AEM资源映射](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
