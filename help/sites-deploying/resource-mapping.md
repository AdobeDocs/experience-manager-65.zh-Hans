---
title: 资源映射
description: 了解如何使用资源映射为Adobe Experience Manager定义重定向、虚URL和虚拟主机。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 2%

---

# 资源映射{#resource-mapping}

资源映射用于为Adobe Experience Manager (AEM)定义重定向、虚URL和虚拟主机。

例如，您可以使用这些映射执行以下操作：

* 为所有请求添加前缀`/content`，以便对网站的访客隐藏内部结构。
* 定义一个重定向，以便将指向您网站`/content/en/gateway`页面的所有请求重定向到`https://gbiv.com/`。

一个可能的HTTP映射为所有请求添加了`/content`的`localhost:4503`前缀。 在允许的情况下，此类映射可用于对网站访客隐藏内部结构：

`localhost:4503/content/we-retail/en/products.html`

要使用进行访问：

`localhost:4503/we-retail/en/products.html`

由于映射会自动将前缀`/content`添加到`/we-retail/en/products.html`。

>[!CAUTION]
>
>虚URL不支持正则表达式模式。

>[!NOTE]
>
>有关详细信息，请参阅Sling文档以及资源解析[&#128279;](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)和[资源](https://sling.apache.org/documentation/the-sling-engine/resources.html)的映射。

## 查看映射定义 {#viewing-mapping-definitions}

JCR资源解析器计算映射表单两个列表（自上而下）以查找匹配项。

可以在Felix控制台的&#x200B;**JCR ResourceResolver**&#x200B;选项下查看这些列表（以及配置信息）；例如，`https://<*host*>:<*port*>/system/console/jcrresolver`：

* 配置
显示当前配置（如[Apache Sling资源解析程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)所定义）。

* 配置测试
这可让您输入URL或资源路径。 单击&#x200B;**解析**&#x200B;或&#x200B;**映射**&#x200B;以确认系统将如何转换该条目。

* **解析程序映射条目**
ResourceResolver.resolve方法用于将URL映射到资源的条目列表。

* **映射项**
ResourceResolver.map方法用来将资源路径映射到URL的条目列表。

这两个列表显示了各种条目，包括应用程序定义为默认值的条目。 这些功能的目的通常是简化用户的URL。

列表将与&#x200B;**Pattern**（与请求匹配的正则表达式）和&#x200B;**Replacement**&#x200B;配对，后者定义要实施的重定向。

例如：

**模式** `^[^/]+/[^/]+/welcome$`

将触发：

**替换** `/libs/cq/core/content/welcome.html`。

要重定向请求：

`https://localhost:4503/welcome` »

收件人：

`https://localhost:4503/libs/cq/core/content/welcome.html`

新的映射定义将在存储库中创建。

>[!NOTE]
>
>有许多资源可帮助您解释如何定义正则表达式。 例如，[https://www.regular-expressions.info/](https://www.regular-expressions.info/)。

### 在AEM中创建映射定义 {#creating-mapping-definitions-in-aem}

在AEM的标准安装中，您可以找到以下文件夹：

`/etc/map/http`

这是为HTTP协议定义映射时使用的结构。 可以在`/etc/map`下为要映射的任何其他协议创建其他文件夹(`sling:Folder`)。

#### 配置到/content的内部重定向 {#configuring-an-internal-redirect-to-content}

要创建将任何请求作为`/content`前缀的映射到https://localhost:4503/：

1. 使用CRXDE导航到`/etc/map/http`。

1. 创建节点：

   * **类型** `sling:Mapping`
此节点类型适用于此类映射，但其用法不是强制性的。

   * **名称** `localhost_any`

1. 单击&#x200B;**全部保存**。
1. **向此节点添加**&#x200B;以下属性：

   * **名称** `sling:match`

      * **类型** `String`

      * **值** `localhost.4503/`

   * **名称** `sling:internalRedirect`

      * **类型** `String[]`

      * **值** `/content/`

1. 单击&#x200B;**全部保存**。

这将处理如下请求：
`localhost:4503/geometrixx/en/products.html`
就象：
`localhost:4503/content/geometrixx/en/products.html`
已被请求。

>[!NOTE]
>
>请参阅Sling文档中的[资源](https://sling.apache.org/documentation/the-sling-engine/resources.html)，以了解有关可用Sling属性以及如何配置这些属性的更多信息。

>[!NOTE]
>
>您可以使用`/etc/map.publish`保存发布环境的配置。 必须复制这些文件，并为发布环境的[Apache Sling资源解析器](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)的&#x200B;**映射位置**&#x200B;配置新位置(`/etc/map.publish`)。
