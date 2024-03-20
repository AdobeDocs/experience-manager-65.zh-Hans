---
title: 实施Analytics的服务器端页面命名
description: Adobe Analytics使用s.pageName属性来唯一标识页面，并关联为页面收集的数据
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# 实施Analytics的服务器端页面命名{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics使用 `s.pageName` 属性，用于唯一标识页面并关联为页面收集的数据。 通常，您需要在AEM中执行以下任务，为AEM发送到Analytics的此属性分配值：

* 使用Analytics云服务框架将CQ变量映射到Analytics `s.pageName` 属性。 (请参阅 [将组件数据映射到Adobe Analytics属性](/help/sites-administering/adobeanalytics-mapping.md).)

* 设计页面组件，使其包含映射到的CQ变量 `s.pageName` 属性。 (请参阅 [为自定义组件实施Adobe Analytics跟踪](/help/sites-developing/extending-analytics-components.md).)

要在Sites控制台和内容分析中显示Analytics报表数据，AEM需要使用 `s.pageName` 属性。 AEM Analytics Java API定义 `AnalyticsPageNameProvider` 您实施的用于为站点控制台和内容分析提供值的界面。 `s.pageName` 属性。 您的 `AnaltyicsPageNameProvider` 服务解析服务器上用于报告的pageName属性，因为它可以在客户端上使用JavaScript动态设置以进行跟踪。

## 默认的Analytics页面名称提供程序服务 {#the-default-analytics-page-name-provider-service}

此 `DefaultPageNameProvider` service是默认服务，用于确定 `s.pageName` 用于检索页面的Analytics数据的属性。 该服务可与AEM foundation页面组件( `/libs/foundation/components/page`)。 此页面组件定义以下旨在映射到的CQ变量 `s.pageName` 属性：

* `pagedata.path`：将该值设置为页面路径。
* `pagedata.title`：将该值设置为页面标题。
* `pagedata.navTitle`：将该值设置为页面导航标题。

此 `DefaultPageNameProvider` 服务确定这些CQ变量中的哪个已映射到 `s.pageName` 属性。 然后，该服务会确定用于检索Analytics报表数据的相应页面属性：

* `pagedata.path`：服务使用 `page.getPath()`

* `pagedata.title`：服务使用 `page.getTitle()`

* `pagedata.navTitle`：服务使用 `page.getNavigationTitle()`

此 `page` 对象是 [`com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) 页面的Java对象。

如果不将CQ变量映射到 `s.pageName` 属性，其值 `s.pageName` 是从页面路径生成的。 例如，路径为 `/content/geometrixx/en` 使用值 `content:geometrixx:en` 对象 `s.pageName`.

>[!NOTE]
>
>DefaultPageNameProvider服务使用的服务等级为100。

## 维护Analytics报表的连续性 {#maintaining-continuity-in-analytics-reporting}

要维护页面的分析数据的完整历史记录，需要永不更改用于页面的s.pageName属性的值。 但是，可以轻松更改基础页面组件定义的分析属性。 例如，移动页面会更改 `pagedata.path` 并中断报告历史记录的连续性：

* 为上一路径收集的数据不再与页面关联。
* 如果其他页面使用另一个页面曾经使用的路径，则该不同页面会继承该路径的数据。

为确保报告连续性，将 `s.pageName` 应具有以下特征：

* 唯一。
* 稳定。
* 人工可读。

例如，自定义页面组件可以包含页面属性，作者可使用它为页面指定唯一ID，作为页面的值 `s.pageProperties` 属性：

* 页面包含一个Analytics变量，该变量设置为存储在页面属性中的唯一ID的值。
* Analytics变量将映射到 `s.pageProperties` 属性。
* AnalyticsPageNameProvider接口的实施将检索用于查询页面分析数据的页面属性的值。

>[!NOTE]
>
>请咨询您的Analytics顾问，以帮助您制定有效的策略 `s.pageName` 值。

### 实施Analytics页面名称提供程序服务 {#implementing-an-analytics-page-name-provider-service}

实施 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` 界面作为OSGi服务，用于自定义检索 `s.pageName` 属性值。 “站点”页面分析和内容分析使用此服务从Analytics中检索报表数据。

AnalyticsPageNameProvider接口定义了必须实施的两种方法：

* `getPageName`：返回 `String` 值，表示要用作 `s.pageName` 属性。

* `getResource`：返回 `org.apache.sling.api.resource.Resource` 表示与关联的页面的对象 `s.pageName` 属性。

这两种方法都需要 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` 对象。 此 `AnalyticsPageNameContext` 类提供了有关analytics调用上下文的信息：

* 页面资源的基本路径。
* 此 `Framework` Analytics云服务配置的对象。
* 此 `Resource` 页面的对象。
* 此 `ResourceResolver` 页面的对象。

类还为页面名称提供setter。

### AnalyticsPageNameProvider实施示例 {#example-analyticspagenameprovider-implementation}

以下示例 `AnalyticsPageNameProvider` 实施支持自定义页面组件：

* 该组件扩展了基础页面组件。
* 该对话框包括一个字段，作者使用该字段指定 `s.pageName` 属性。
* 属性值存储在的pageName属性中 `jcr:content`页面实例的节点。
* 存储 `s.pageName` 属性名为 `pagedata.pagename`. 此属性已映射到 `s.pageName` 属性。

以下实施的 `getPageName` 如果正确配置了框架映射，则方法会返回pageName节点属性的值：

```java
public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.pagename")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }
```

getResource方法的以下实施返回该页的Resource对象：

```java
     public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
             Iterator<Resource>
             hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
             if (hits.hasNext()) {
              res = hits.next();
              res = res.getParent();
             }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
```

以下代码表示整个类，包括配置服务的SCR注释。 服务排名为200，覆盖默认服务。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2019 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.day.cq.analytics.sitecatalyst;

import java.util.Iterator;

import javax.jcr.query.Query;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;

import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext;
import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider;
import com.day.cq.analytics.sitecatalyst.Framework;
import com.day.cq.wcm.api.Page;

import static com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext.S_PAGE_NAME;

/**
 * Default implementation of {@link AnalyticsPageNameProvider} that resolves
 * page title, path or navTitle if mapped in {@link Framework}.
 */
@Component(
    service = { AnalyticsPageNameProvider.class },
    property = {
        Constants.SERVICE_DESCRIPTION + "=Example Page Name Resolver implementation",
        Constants.SERVICE_RANKING + ":Integer=200"
    }
)
public class ExamplePageNameProvider implements AnalyticsPageNameProvider {
    public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.path")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }

    public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
                Iterator<Resource>
                hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
                if (hits.hasNext()) {
                    res = hits.next();
                    res = res.getParent();
                }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
}
```
