---
title: 功能板
seo-title: 功能板
description: 了解如何创建、配置和开发新的AEM仪表板。
seo-description: 了解如何创建、配置和开发新的AEM仪表板。
uuid: 3eadbba2-0ce1-41be-a9f8-e6cafa109893
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 40560e06-2508-45a4-a648-39629ed54f28
translation-type: tm+mt
source-git-commit: 69dfd6b41b32cb9131fd90fd7039a0c224889db5

---


# 功能板{#dashboards}

使用 AEM 可以管理多种不同类型的内容（如页面、资产）。AEM 功能板提供一种简单易用的自定义方式来定义主要显示综合数据的页面。

>[!NOTE]
>
>AEM 功能板是基于每位用户创建的，因此用户只能访问他们自己的功能板。
>
>However, [Dashboard templates](#creating-a-dashboard-template) can be used to share common configuration and Dashboard layout.

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## 管理功能板 {#administering-dashboards}

### 创建功能板 {#creating-a-dashboard}

要创建新的功能板，可按照以下步骤进行操作：

1. 在&#x200B;**工具**&#x200B;区域中，单击&#x200B;**配置控制台**。
1. In the tree, Double-Click **Dashboard**.
1. 单击&#x200B;**新建功能板**。
1. 键入&#x200B;**标题**（例如“我的功能板”）和&#x200B;**名称**。
1. 单击&#x200B;**创建**。

### 克隆功能板 {#cloning-a-dashboard}

建议您创建多个功能板，以便在不同的视图中快速查看与内容有关的信息。为了帮助您创建新功能板，AEM 提供了一种克隆功能，可用于复制现有的功能板。要克隆功能板，请按照以下步骤执行操作：

1. 在&#x200B;**工具**&#x200B;区域中，单击&#x200B;**配置控制台**。

1. 在树中，单击&#x200B;**功能板**。
1. 单击要克隆的功能板。

1. 单击&#x200B;**克隆**。

1. 键入新功能板的&#x200B;**名称**。

### 删除功能板 {#removing-a-dashboard}

1. 在&#x200B;**工具**&#x200B;区域中，单击&#x200B;**配置控制台**。

1. 在树中，单击&#x200B;**功能板**。
1. 单击要删除的功能板。

1. 单击&#x200B;**删除**。

1. 单击&#x200B;**是**&#x200B;以确认。

## 功能板组件 {#dashboard-components}

### 概述 {#overview}

Dashboard components are nothing more than regular [AEM components](/help/sites-developing/developing-components-samples.md). 本节介绍随 AEM 一起推出的报表组件。

### 网站分析报表组件 {#web-analytics-reporting-components}

AEM ships with a set of components that render multiple metrics of your [SiteCatalyst](/help/sites-administering/adobeanalytics.md) data. 这些组件在&#x200B;**功能板**&#x200B;区域下方的 Sidekick 中列出。

每个报表组件提供至少三个选项卡：

* **基本**：包含主配置。

* **报表**：包含每个组件的特定配置。
* **样式**：包含样式配置，如图表大小和边距。

报表组件会初始化为默认配置，这有助于您快速设置功能板。

#### 基本配置 {#basic-configuration}

**基本**&#x200B;选项卡提供对以下配置条目的访问权：

**标题** 功能板上显示的标题。

**请求类型** ：请求数据的方式。

**SiteCatalyst配置（可选）** ：要用于连接SiteCatalyst的配置。 如果未提供，则认为该配置是在功能板页面上进行配置的（通过页面属性）。

**报表包ID（可选）** ，要用于生成图形的SiteCatalyst报表包。

#### 报表配置 {#report-configuration}

为了显示网站分析，您需要定义想要获取的数据的日期范围。**报表**&#x200B;选项卡提供两个用于定义该范围的字段。

>[!NOTE]
>
>若设置一个较大的日期范围，会降低功能板的响应能力。

**日期从** “绝对”或从中获取数据的相对日期。

**日期至** 获取数据的绝对或相对日期。

每个组件还定义特定设置。

#### 超时报表 {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**日期粒度** X轴的时间单位（例如，日、小时）。

**量度** 要显示的事件列表。

**元素** 分类图中度量数据的元素列表。

#### 排名列表报表 {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**元素** 分解图形中度量数据的元素。

**量度** ：要显示的事件。

**否. of top items** Number of the report displayed by the items.

#### 排名报表 {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**量度** ：要显示的事件。

**元素** 分解图形中度量数据的元素。

#### 热门网站区域报表 {#top-site-section-report}

该组件显示一个图形，图中又根据以下配置显示网站中访问量较大的区域。

![chlimage_1-29](assets/chlimage_1-29a.png)

**否. 排名最前的项目** ，报告中显示的章节数。

#### 趋势报表 {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**日期粒度** X轴的时间单位（例如，日、小时）。

**量度** ：要显示的事件。

**元素** 分解图形中度量数据的元素。

## 扩展功能板 {#extending-dashboard}

### 概述 {#overview-1}

功能板是普通页面 (`cq:Page`)，因此任何组件都可用于构建功能板。

There is a default component group `Dashboard` containing analytics reporting components which are enabled on the template by default.

### 创建功能板模板 {#creating-a-dashboard-template}

模板定义新功能板的默认内容。您可以使用多个模板来创建不同类型的功能板。

Dashboard templates are created like other page templates, except that they are stored under `/libs/cq/dashboards/templates/`. 请参阅创 [建内容页面模板](/help/sites-developing/website.md#creating-the-contentpage-template) 。

>[!NOTE]
>
>功能板模板可在用户之间共享。

### 开发功能板组件 {#developing-a-dashboard-component}

开发功能板组件包括创建一个常用 AEM 组件。本节介绍用于显示头 10 位参与者的组件示例。

![chlimage_1-31](assets/chlimage_1-31a.png)

The top author components is stored in the repository at `/apps/geometrixx-outdoors/components/reporting` and is composed of :

1. 一个 `jsp` 文件，它可读取数据并定义 `html` 占位符。

1. 一个客户端库，其中包含一个可对数据进行获取或排序，然后填充 `js` 占位符的 `html` 文件。

![chlimage_1-32](assets/chlimage_1-32a.png)

The following Javascript file is defined in the `geout.reporting.topauthors` [Client Library](/help/sites-developing/clientlibs.md) as a child of the component itself.

QueryBuilder [用于查询存储库以读取节](/help/sites-developing/querybuilder-api.md)`cq:AuditEvent` 点。 查询结果是一个可从其中提取作者投稿的 JSON 对象。

#### top_authors.js {#top-authors-js}

```
$.ajax({
  url: "/bin/querybuilder.json",
  cache: false,
  data: {
       "orderby": "cq:time",
       "orderby.sort": "desc",
       "p.hits": "full",
       "p.limit": 100,
       "path": "/var/audit/com.day.cq.wcm.core.page/",
       "type": "cq:AuditEvent"
   },
  dataType: "json"
}).done(function( res ) {
    var authors = {};
    // from JSON to Object
    for(var r in res.hits) {
        var userId = res.hits[r].userId;
        if(userId == undefined) {
            continue;
        }
        var auth = authors[userId] || {userId : userId};
        auth.contrib = (auth.contrib || 0) +1;

        authors[userId] = auth;
    }

    // order by contribution
    var orderedByContrib = [];
    for(var a in authors) {
        orderedByContrib.push(authors[a]);
    }
    orderedByContrib.sort(function(a,b){return b.contrib - a.contrib});

    // produce the list
    for (var i=0, tot=orderedByContrib.length; i < tot; i++) {
        var current = orderedByContrib[i];
        $("<div> #" + (i + 1) +" "+ current.userId + " (" + current.contrib +" contrib.)</div>").appendTo("#authors-list");

    }
});
```

其中 `JSP` 包括 `global.jsp` 和 `clientlib`。

#### top_authors.jsp {#top-authors-jsp}

```java
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%
%><%@include file="/libs/foundation/global.jsp" %><%
%>
<ui:includeClientLib categories="geout.reporting.topauthors" />
<%
String reportletTitle = properties.get("title", "Top Authors");
%>
<html>
     <h3><%=xssAPI.encodeForHTML(reportletTitle) %></h3>
     <div id="authors-list"></div>
</html>
```

