---
title: SEO 和 URL 管理最佳做法
description: 了解在 AEM 实施中的 SEO 最佳做法和相关建议。
topic-tags: managing
content-type: reference
docset: aem65
exl-id: b138f6d1-0870-4071-b96e-4a759ad9a76e
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: ht
source-wordcount: '3522'
ht-degree: 100%

---

# SEO 和 URL 管理最佳做法{#seo-and-url-management-best-practices}

SEO（搜索引擎优化）已成为许多营销人员的核心关注点。因此，在众多 AEM 项目中必须解决与 SEO 相关的问题。

本文档首先介绍一些 [SEO 最佳做法](#seo-best-practices)以及在 AEM 实施中的相关建议。然后，本文档更深入地介绍了第一节中提出的一些更加[复杂的实施步骤](#aem-configurations)。

## SEO 最佳做法 {#seo-best-practices}

本节介绍了一些常规的 SEO 最佳做法。

### URL {#urls}

对于 URL 有一些公认的最佳做法。

在 AEM 项目中评估 URL 时，请问自己以下问题：

“如果用户看到这个 URL 但没有看到页面内容，他们能否描述该页面？”

如果能做到，那么可能该 URL 对于搜索引擎可正常工作。

以下是有关如何构建 URL 以实施 SEO 的一些常规方法：

* 使用连字符来分隔单词。

   * 使用连字符（-）作为分隔符来命名页面。
   * 避免使用驼峰式拼写、下划线和空格。

* 尽量避免使用查询参数。如有必要，请将查询参数限制在两个以内。

   * 如果可用，请使用目录结构指示信息架构。
   * 如果无法使用目录结构，请在 URL 中使用 Sling 选择器而非查询字符串。除了提供 SEO 值外，Sling 选择器还能让页面在 Dispatcher 中实现缓存。

* URL 越具可读性越好。URL 中包含关键词能够提升值。

   * 在页面上使用选择器时，首选提供语义值的选择器。
   * 如果人们无法读取您的 URL，则搜索引擎也无法读取。
   * 例如：
     `mybrand.com/products/product-detail.product-category.product-name.html` 比 `mybrand.com/products/product-detail.1234.html` 更可取

* 尽量避免使用子域，因为搜索引擎会将其视为不同实体，从而分散网站的 SEO 值。

   * 相反，请使用第一级子路径。例如，使用 `www.mybrand.com/es/home.html`，而不是 `es.mybrand.com/home.html`。

   * 根据该指南，按照内容呈现方式规划内容层级结构。

* URL 中的关键字有效性与 URL 长度和关键字位置成反比，URL 长度越长和关键字位置越靠后有效性越低。换句话说，URL 越短越好。

   * 使用 AEM 提供的 URL 缩短技术和功能删除不必要的 URL 片段。
   * 例如，`mybrand.com/en/myPage.html` 比 `mybrand.com/content/my-brand/en/myPage.html` 更可取。

* 使用规范 URL。

   * 当 URL 来自不同路径或具有不同参数或选择器时，请确保在页面上使用 `rel=canonical` 标记。

   * 在 AEM 模板代码中包含规范 URL。

* 尽量将 URL 与页面标题匹配。

   * 应该鼓励内容作者遵循这种做法。

* 支持 URL 请求不区分大小写。

   * 配置 Dispatcher 以使其将所有入站请求都重写为小写字母。
   * 为内容作者提供使用小写字母创建页面的培训。

* 确保每个页面仅通过一种协议提供。

   * 有时，网站会通过 `http` 提供，直到用户访问包含结帐或登录表单等内容的页面时为止，此时网站将切换成 `https`。从此页面进行链接时，如果用户可以返回 `http` 页面，并且能够通过 `https` 访问这些页面，搜索引擎会将其视为两个独立的页面来跟踪。

   * 目前，Google 首选的页面是 `https` 而不是 `http`。它们有助于使每个人在通过 `https` 为整个网站提供服务时更加便捷。

### 服务器配置 {#server-configuration}

在服务器配置方面，您可以采取以下步骤来确保仅爬取正确的内容：

* 使用 `robots.txt` 文件阻止爬取任何不应建立索引的内容。

   * 阻止对测试环境的&#x200B;**所有**&#x200B;爬网。

* 在启动包含更新的 URL 的新站点时，请实施 301 重定向以确保不会丢失现有 SEO 排名。
* 包含您的站点的网站图标。
* 为了使搜索引擎更容易抓取您的内容，请实施一个 XML Sitemap。请确保为移动端和/或响应式网站加入一个移动端 Sitemap。

## AEM 配置 {#aem-configurations}

本节介绍了配置 AEM 遵循以下 SEO 建议的实施步骤。

### 使用 Sling 选择器 {#using-sling-selectors}

以前在构建企业 Web 应用程序时使用查询参数是公认的惯例。

近年来的趋势是移除参数，以提升 URL 的可读性。在许多平台上，这种移除过程通常需要在 Web 服务器或内容传递网络（CDN）上实施重定向，而 Sling 则能够让这一过程更加简便。Sling 选择器能够：

* 提高 URL 可读性。
* 它可以让您在 Dispatcher 上缓存页面，并提升安全性。
* 它允许您直接访问内容，而不是让通用的 Servlet 来检索内容。它还使您能够利用应用在存储库上的 ACL 以及在 Dispatcher 上配置的过滤器所带来的优势。

#### 为 Servlet 使用选择器 {#using-selectors-for-servlets}

在编写 Servlet 时，AEM 提供两个选项：

* **bin** servlet
* **Sling** servlet

以下示例阐述如何注册遵循这两个模式的 Servlet 以及使用 Sling Servlet 获得的利益。

#### Bin Servlet（下一级） {#bin-servlets-one-level-down}

**Bin** Servlet 遵循许多开发人员惯用的 J2EE 编程模式。在 AEM 中，Servlet 会注册到特定路径下，通常位于 `/bin`，您可以通过查询字符串提取所需的请求参数。

此类 Servlet 的 SCR 注释如下所示：

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

然后，通过 `doGet` 方法中包含的 `SlingHttpServletRequest` 对象，从查询字符串中提取参数，例如：

```
String myParam = req.getParameter("myParam");
```

使用的生成 URL 如下所示：

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

使用这种方法需要考虑以下几点：

* URL 本身会丢失 SEO 价值。访问站点（包括搜索引擎）的用户不会从 URL 收到任何语义价值，因为 URL 代表着程序化路径，而不是内容层次结构。
* 当 URL 中包含查询参数时，意味着 Dispatcher 将无法缓存该响应。
* 如果您希望保护此 Servlet，则需要在 Servlet 中实施自定义的安全逻辑。
* 必须（仔细地）配置 Dispatcher 以公开 `/bin/myApp/myServlet`。仅公开 `/bin` 可能会允许访问某些不应对站点访客开放的 Servlet。

#### Sling servlet（下一级） {#sling-servlets-one-level-down}

**Sling** Servlet 允许您以相反的方式注册 Servlet。与其通过 Servlet 并依赖查询参数来指定您希望 Servlet 渲染的内容，不如直接定位您所需的内容。然后，您可以通过 Sling 选择器来指定用于渲染该内容的 Servlet。

此类 Servlet 的 SCR 注释如下所示：

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json", methods="GET")
```

在这种情况下，URL 所指向的资源（即 `myPageType` 资源的一个实例）会在 Servlet 中自动可用。要访问它，您需要调用以下内容：

```
Resource myPage = req.getResource();
```

使用的生成 URL 如下所示：

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

这种方法的好处是：

* 您可以通过站点层次结构和页面名称中存在的语义来获得 SEO 价值。
* 既然不存在查询参数，因此 Dispatcher 可缓存响应。此外，对已寻址的页面作出任何更改，都将在激活该页面时使此缓存无效。
* 所有应用于 `/content/my-brand/my-page` 的 ACL 在用户尝试访问此 Servlet 时生效。
* Dispatcher 已经配置为在提供网站服务的同时交付此类内容。无需其他配置。

### URL 重写 {#url-rewriting}

在 AEM 中，所有网页都存储在 `/content/my-brand/my-content` 下面。尽管这一位置在存储库数据管理的角度来看非常实用，但它未必是您希望客户看到网站的方式。此外，它可能与 SEO 中“尽量缩短 URL”的指导原则相冲突。此外，您可能正在从不同域名通过同一个 AEM 实例提供多个网站。

本节会回顾 AEM 中用于管理 URL 并以更易读和 SEO 友好的方式向用户展示这些 URL 的可用选项。

#### 虚名 URL {#vanity-urls}

如果作者出于促销目的，希望从另一个位置访问页面，则 AEM 逐页定义的虚名 URL 可能会有用。要为页面添加虚名 URL，请在&#x200B;**Sites**&#x200B;控制台中导航到该页面，并编辑页面属性。在&#x200B;**基本**&#x200B;选项卡的底部，您会看到可添加虚名 URL 的部分。请记住，通过多个 URL 访问特定页面会分割该页面的 SEO 价值，因此，应向页面添加规范 URL 标记以避免出现此问题。

#### 本地化的页面名称 {#localized-page-names}

您可能希望向用户显示本地化页面名称中已翻译的内容。例如：

* 不要让讲西班牙语的用户导航到：
  `www.mydomain.com/es/home.html`

* 而最好是让用户访问以下 URL：
  `www.mydomain.com/es/casa.html`。

本地化页面名称的挑战在于，AEM Platform 上的许多可用本地化工具都依赖于让页面名称在各个不同区域环境中匹配，以保持内容同步。

`sling:alias` 属性能够同时满足这两方面的需求。您可以将 `sling:alias` 添加为任意资源的属性，从而为该资源设置别名。在前一个示例中，您会得到如下结果：

* JCR 中的页面指向：
  `…/es/home`

* 然后，向其添加属性：
  `sling:alias` = `casa`

此流程会使 AEM 翻译工具（如多网站管理器）能够继续维护以下关系：

* `/en/home`

* `/es/home`

同时，还允许最终用户与使用其母语的页面名称进行交互。

>[!NOTE]
>
>可通过[编辑“页面属性”时使用别名属性](/help/sites-authoring/editing-page-properties.md#advanced)来设置 `sling:alias` 属性。

#### /etc/map {#etc-map}

在标准 AEM 安装中：

* 对于 OSGi 配置
  **Apache Sling Resource Resolver Factory**（ `org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`）

* 属性
  **映射位置**（ `resource.resolver.map.location`）

* 默认设置为 `/etc/map`。

可以在此位置添加映射定义来映射入站请求，和/或在 AEM 中重写页面上的 URL。

要创建映射，请在 `/http` 或 `/https` 下面的此位置创建一个 `sling:Mapping` 节点。根据在此节点上设置的 `sling:match` 和 `sling:internalRedirect` 属性，AEM 会将匹配 URL 的所有流量重定向到 `internalRedirect` 属性中指定的值。

尽管此方法已在 AEM 和 Sling 的官方文档中有所说明，但与直接使用 `SlingResourceResolver` 可用的选项相比，该实施所提供的正则表达式支持范围有限。此外，以这种方式实施映射可能会导致 Dispatcher 缓存失效问题。

以下示例简要介绍了这个问题是如何发生的：

1. 用户访问您的网站并请求 `https://www.mydomain.com/my-page.html`
1. Dispatcher 将此请求转发到发布服务器。
1. 通过使用 `/etc/map`，发布服务器将此请求解析到 `/content/my-brand/my-page` 并呈现该页面。

1. Dispatcher 在 `/my-page.html` 处缓存响应并将响应返回给用户。
1. 内容作者更改此页面并激活它。
1. Dispatcher 刷新代理发送对 `/content/my-brand/my-page`**的无效请求。** 由于 Dispatcher 在此路径下没有缓存页面，旧内容仍然保留在缓存中并已过期。

有多种方法可以配置自定义调度刷新规则，这些规则将较短 URL 映射到较长 URL，以实现缓存失效的目的。

不过，还有一种更简便的方式来解决此问题：

1. **SlingResourceResolver 规则**

   使用网页控制台（例如 localhost:4502/system/console/configMgr）来配置 Sling 资源解析程序。

   * **Apache Sling Resource Resolver Factory**
     `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`。

   Adobe 建议您将缩短 URL 所需的映射构建为正则表达式，然后在构建中包含的 `config.publish` 下的 OsgiConfignode 节点下定义这些配置。

   可以将这些配置直接分配给属性 **URL 映射**（ `resource.resolver.mapping`），而不是在 `/etc/map` 中定义您的映射。

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   在这个简单的示例中，您将删除位于任何 URL 开头位置的 `/content/my-brand/`。

   它会转化 URL：

   * 从 `/content/my-brand/my-page.html`
   * 转化为 `/my-page.html`

   此类转化符合“尽量缩短 URL”的推荐做法。

1. **在页面上映射 URL 输出**

   在 Apache Sling 资源解析程序中定义映射后，请在组件中使用这些映射，以确保页面输出的 URL 简洁清晰。您可以通过 `ResourceResolver` 的 map 函数来完成这一整理工作。

   例如，如果您正在实施一个自定义导航组件，该组件列出了当前页面的子页面，则可以使用如下映射方法：

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

到目前为止，您已经与组件中的逻辑一起实施了映射，以将 URL 输出到页面时使用这些映射。

最后一步就是缩短的 URL 进入 Dispatcher 后如何进行处理，这正是 `mod_rewrite` 发挥作用的时候。使用 `mod_rewrite` 最大的好处是，在将 URL 发送到 Dispatcher 模块&#x200B;*之前*，该 URL 会映射回其长格式。这一流程意味着 Dispatcher 会向发布服务器请求长 URL，并相应地进行缓存。因此，来自发布服务器的任何 Dispatcher 刷新请求都能够成功使该内容失效。

要实施这些规则，可以在 Apache HTTP Server 配置的虚拟主机下添加 `RewriteRule` 元素。如果要将前面示例中缩短的 URL 展开，您可以实施如下规则：

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### 规范 URL 标记 {#canonical-url-tags}

规范 URL 标记是指放置到 HTML 文档标题中的链接标记，用于阐明搜索引擎在索引内容时应如何处理页面。这些标记带来的好处是，即使指向页面的 URL 可能存在差异，也能确保（不同版本的）页面的索引是相同的。

例如，如果站点要提供打印机友好版本的页面，则搜索引擎可能会将该页面与常规版本的页面分开进行索引。规范标记会告诉搜索引擎，它们是相同的。

示例：

* `https://www.mydomain.com/my-brand/my-page.html`
* `https://www.mydomain.com/my-brand/my-page.print.html`

二者均会将以下标记应用于页面的标题：

```xml
<link rel="canonical" href="my-brand/my-page.html"/>
```

`href` 可以是相对位置或绝对位置。该代码应包含在页面标记中，以确定页面的规范 URL 并输出此标记。

### 将 Dispatcher 配置为不区分大小写 {#configuring-the-dispatcher-for-case-insensitivity}

最佳做法是使用小写字母来提供所有页面。但是，您不希望当用户在 URL 中使用大写字母访问您的网站时得到 404 错误。因此，Adobe 建议您在 Apache HTTP Server 配置中添加重写规则，以将所有传入的 URL 映射为小写。此外，必须为内容作者提供使用小写字母创建页面的培训。

要配置 Apache 将所有入站流量强制转化为小写，请在 `vhost` 配置中添加以下内容：

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

此外，在 `htaccess` 文件的最上方添加以下内容：

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### 实施 robots.txt 以保护开发环境 {#implementing-robots-txt-to-protect-development-environments}

在爬取站点之前，搜索引擎&#x200B;*应该*&#x200B;检查站点根目录中是否存在 `robots.txt` 文件。尽管 Google、Yahoo 或 Bing 等主流搜索引擎都会遵循该文件，但某些海外搜索引擎可能不会。

阻止访问整个站点的最简单方法是，将名为 `robots.txt` 的文件放置到站点根目录下，并包含以下内容：

```xml
User-agent: *
Disallow: /
```

或者，在实时环境中，您可以选择禁止某些不希望索引的路径。

需要注意的是，将 `robots.txt` 文件放置在网站根目录时，Dispatcher 的刷新请求可能会清除该文件。此外，URL 映射通常会将网站根目录放置在与 Apache HTTP 服务器配置中定义的 `DOCROOT` 不同的位置。因此，通常将该文件放在站点根目录的作者实例上，并将其复制到发布实例。

### 在 AEM 上构建 XML Sitemap {#building-an-xml-sitemap-on-aem}

爬取程序使用 XML 站点地图来更好地理解网站的结构。虽然提供站点地图无法保证会提高 SEO 排名，但这是公认的最佳做法。您可以在 Web 服务器上手动维护一个 XML 文件，将其作为 Sitemap 使用。但是，Adobe 建议您以编程的方式生成 Sitemap，以确保在作者创建内容时，Sitemap 能够自动反映这些更改。

AEM 使用 [Apache Sling Sitemap 模块](https://github.com/apache/sling-org-apache-sling-sitemap)来生成 XML Sitemap，该模块为开发人员和编辑人员提供了多种选项，以使网站 XML Sitemap 保持最新状态。

>[!NOTE]
>
>此功能自 Adobe Experience Manager 6.5.11.0 起作为产品特性提供。
> 
>在更早的版本中，您可以自行注册一个 Sling Servlet，用于监听 `sitemap.xml` 请求。使用 Servlet API 提供的资源来查找当前页面及其子页面，以输出 `sitemap.xml` 文件。

Apache Sling Sitemap 模块将区分为 `sling:sitemapRoot` 属性设置为 `true` 的任何资源生成的顶级站点地图和嵌套站点地图。通常，使用树的顶级站点地图路径上的选择器来呈现站点地图，而顶级站点地图是没有其他站点地图根祖先的资源。此顶级站点地图根还公开站点地图索引，该索引通常是站点所有者将在搜索引擎的配置门户中配置或添加到站点的 `robots.txt` 的内容。

例如，考虑一个在 `my-page` 定义顶级站点地图并在 `my-page/news` 定义嵌套站点地图的网站，以便为新闻子树中的页面生成专用站点地图。生成的相关 URL 将为

* `https://www.mydomain.com/my-brand/my-page.sitemap-index.xml`
* `https://www.mydomain.com/my-brand/my-page.sitemap.xml`
* `https://www.mydomain.com/my-brand/my-page.sitemap.news-sitemap.html`

>[!NOTE]
>
>选择器 `sitemap` 和 `sitemap-index` 可能会干扰自定义实现。如果您不想使用产品功能，请使用高于 0 的 `service.ranking` 来配置用于这些选择器的自己的 servlet。

在默认配置中，“页面属性”对话框提供了一个选项，用于将页面标记为 Sitemap 根（如上所述）并生成 Sitemap 本身及其后代。此行为通过实施 `SitemapGenerator` 接口来实施，并且可以通过添加替代实施进行扩展。但是，由于重新生成 XML Sitemap 的频率取决于内容创作的工作流和工作量，产品本身并未提供任何 `SitemapScheduler` 配置。因此，该功能实际上是按需选择启用的。

若要启用生成 XML Sitemap 的后台作业，必须配置 `SitemapScheduler`。为此，可为 PID `org.apache.sling.sitemap.impl.SitemapScheduler` 创建 OSGI 配置。调度程序表达式 `0 0 0 * * ?` 可用作起点，以在每天的午夜重新生成所有 XML Sitemap 一次。

![Apache Sling Sitemap - 调度程序](assets/sling-sitemap-scheduler.png)

Sitemap 生成作业可以在创作和发布层实例上运行。通常建议在发布层实例上运行生成任务，因为只有在该层才能生成正确的规范化 URL（这是由于 Sling 资源映射规则通常只存在于发布层实例上）。不过，您也可以通过实施 [SitemapLinkExternalizer](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/externalizer/SitemapLinkExternalizer.html) 接口，插入用于生成规范化 URL 的外部化机制的自定义实施。如果自定义实施能够在创作层实例上生成 Sitemap 的规范化 URL，则可以将 `SitemapScheduler` 配置为创作运行模式。这样，XML Sitemap 的生成工作负载就可以分散到创作服务集群的各个实例中。在这种情况下，需要注意处理尚未发布、已修改或仅对特定用户组可见的内容。

AEM Sites 包含 `SitemapGenerator` 的默认实施，它将遍历页面树以生成 Sitemap。它预先配置为仅输出站点的规范 URL 和任何语言替代项（如果可用）。如果需要，它还可以配置为包含页面的上次修改日期。为此，请在 _Adobe AEM SEO - 页面树 Sitemap 生成器_&#x200B;配置中启用&#x200B;_添加最后修改时间_&#x200B;选项，并选择一个&#x200B;_最后修改时间源_。在发布层上生成站点地图时，建议使用 `cq:lastModified` 日期。

![Adobe AEM SEO - 页面树 Sitemap 生成器配置](assets/sling-sitemap-pagetreegenerator.png)

要限制 Sitemap 的内容，可以在需要时实施以下服务接口：

* 可以实施 [SitemapPageFilter](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/SitemapPageFilter.html)，以在由 AEM Sites 特定的 Sitemap 生成器生成的 XML Sitemap 中隐藏页面
* 可以实施 [SitemapProductFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapProductFilter.html) 或 [SitemapCategoryFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapCategoryFilter.html)，以从由 [Commerce 集成框架](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html?lang=zh-Hans)特定的 Sitemap 生成器生成的 XML Sitemap 筛选出产品或类别

如果默认实施无法满足特定用例，或扩展点不够灵活，您可以实施自定义的 `SitemapGenerator`，以完全控制生成的 Sitemap 内容。以下示例使用了 AEM Sites 的默认实施逻辑。它使用 [ResourceTreeSitemapGenerator](https://javadoc.io/doc/org.apache.sling/org.apache.sling.sitemap/latest/org/apache/sling/sitemap/spi/generator/ResourceTreeSitemapGenerator.html) 作为起点来遍历页面树：

```
import java.util.Optional;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.sitemap.SitemapException;
import org.apache.sling.sitemap.builder.Sitemap;
import org.apache.sling.sitemap.builder.Url;
import org.apache.sling.sitemap.spi.common.SitemapLinkExternalizer;
import org.apache.sling.sitemap.spi.generator.ResourceTreeSitemapGenerator;
import org.apache.sling.sitemap.spi.generator.SitemapGenerator;
import org.jetbrains.annotations.NotNull;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.aem.wcm.seo.sitemap.PageTreeSitemapGenerator;
import com.day.cq.wcm.api.Page;

@Component(
    service = SitemapGenerator.class,
    property = { "service.ranking:Integer=20" }
)
public class SitemapGeneratorImpl extends ResourceTreeSitemapGenerator {

    private static final Logger LOG = LoggerFactory.getLogger(SitemapGeneratorImpl.class);

    @Reference
    private SitemapLinkExternalizer externalizer;
    @Reference
    private PageTreeSitemapGenerator defaultGenerator;

    @Override
    protected void addResource(@NotNull String name, @NotNull Sitemap sitemap, Resource resource) throws SitemapException {
        Page page = resource.adaptTo(Page.class);
        if (page == null) {
            LOG.debug("Skipping resource at {}: not a page", resource.getPath());
            return;
        }
        String location = externalizer.externalize(resource);
        Url url = sitemap.addUrl(location + ".html");
        // add any additional content to the Url like lastmod, change frequency, and so on
    }

    @Override
    protected final boolean shouldFollow(@NotNull Resource resource) {
        return super.shouldFollow(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldFollow).orElse(Boolean.TRUE);
    }

    private boolean shouldFollow(Page page) {
        // add additional conditions to stop traversing some pages
        return !defaultGenerator.isProtected(page);
    }

    @Override
    protected final boolean shouldInclude(@NotNull Resource resource) {
        return super.shouldInclude(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldInclude).orElse(Boolean.FALSE);
    }

    private boolean shouldInclude(Page page) {
        // add additional conditions to stop including some pages
        return defaultGenerator.isPublished(page)
            && !defaultGenerator.isNoIndex(page)
            && !defaultGenerator.isRedirect(page)
            && !defaultGenerator.isProtected(page);
    }
}
```

此外，为 XML Sitemap 实施的功能也可应用于不同的用例，例如在页面的页头中添加规范化链接或语言替代项。有关更多信息，请参阅 [SeoTags](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/SeoTags.html) 接口。

### 为旧版 URL 创建 301 重定向 {#creating-redirects-for-legacy-urls}

由于以下两个原因，在启动具有新结构的站点时，应在 Apache HTTP Server 中测试和实施 301 重定向，这一点很重要：

* 随着时间的推移，旧版 URL 已积累了 SEO 价值。通过实施重定向，搜索引擎可以将此价值应用于新的 URL。
* 您站点的用户可能已经为这些页面创建了书签。通过实施重定向，您可以确保将用户定向到新站点上与他们尝试访问的旧站点最匹配的页面。

请务必查看下面的“其他资源”部分，以获取关于实施 301 重定向的操作说明，以及测试重定向是否按预期工作的工具。

## 其他资源 {#additional-resources}

有关详细信息，请参阅以下其他资源：

* [资源映射](/help/sites-deploying/resource-mapping.md)
* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
