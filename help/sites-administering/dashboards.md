---
title: 功能板
description: 了解如何创建、配置和开发新的AEM功能板。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 5b934e3a-f554-46ec-a913-8d570abb1503
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 3%

---

# 功能板{#dashboards}

使用AEM时，您可以管理多种不同类型的内容（例如，页面、资源）。 AEM功能板提供了一种易于使用和自定义的方法来定义显示合并数据的页面。

>[!NOTE]
>
>AEM功能板是按用户创建的，因此用户只能访问自己的功能板。
>
>但是，[仪表板模板](#creating-a-dashboard-template)可用于共享通用配置和仪表板布局。

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## 管理功能板 {#administering-dashboards}

### 创建功能板 {#creating-a-dashboard}

1. 在&#x200B;**工具**&#x200B;部分中，单击&#x200B;**配置控制台**。
1. 在树中，双击&#x200B;**仪表板**。
1. 单击&#x200B;**新仪表板**。
1. 键入&#x200B;**Title** （例如，我的仪表板）和&#x200B;**Name**。
1. 单击&#x200B;**创建**。

### 克隆功能板 {#cloning-a-dashboard}

您可能希望具有多个功能板，以便从不同视图快速查看有关您的内容的信息。 为了帮助您创建新功能板，AEM提供了一个克隆功能，您可以使用该功能复制现有功能板。 要克隆功能板，请按照以下步骤操作：

1. 在&#x200B;**工具**&#x200B;部分中，单击&#x200B;**配置控制台**。

1. 在树中，单击&#x200B;**仪表板**。
1. 单击要克隆的功能板。

1. 单击&#x200B;**克隆**。

1. 键入新仪表板的&#x200B;**Name**。

### 删除功能板 {#removing-a-dashboard}

1. 在&#x200B;**工具**&#x200B;部分中，单击&#x200B;**配置控制台**。

1. 在树中，单击&#x200B;**仪表板**。
1. 单击要删除的仪表板。

1. 单击&#x200B;**删除**。

1. 单击&#x200B;**是**&#x200B;以确认。

## 功能板组件 {#dashboard-components}

### 概述 {#overview}

仪表板组件只是常规的[AEM组件](/help/sites-developing/developing-components-samples.md)。 本节介绍AEM附带的报表组件。

### 网站分析报表组件 {#web-analytics-reporting-components}

AEM附带一组组件，这些组件呈现[SiteCatalyst](/help/sites-administering/adobeanalytics.md)数据的多个指标。 这些组件在Sidekick中的&#x200B;**仪表板**&#x200B;部分下列出。

每个报表组件至少提供三个选项卡：

* **基本**：包含主配置。

* **报告**&#x200B;包含每个报告的特定配置。
* **样式**：包含样式配置，如图表大小和边距。

报表组件使用默认配置进行初始化，可帮助您快速设置功能板。

#### 基本配置 {#basic-configuration}

**基本**&#x200B;选项卡提供对以下配置项的访问：

**标题**&#x200B;仪表板上显示的标题。

**请求类型**&#x200B;请求数据的方式。

**SiteCatalyst配置（可选）**&#x200B;要用于连接到SiteCatalyst的配置。 如果未提供，则假定已在功能板页面（通过页面属性）上配置配置。

**报表包ID（可选）**&#x200B;要用于生成图形的SiteCatalyst报表包。

#### 报告配置 {#report-configuration}

要显示Web统计信息，您需要定义要收集的数据的日期范围。 **报表**&#x200B;选项卡提供了两个字段来定义该范围。

>[!NOTE]
>
>设置较大的日期范围可能会降低仪表板的响应性。

**起始日期**&#x200B;从中获取数据的绝对或相对日期。

**截止日期**&#x200B;获取数据的绝对或相对日期。

每个组件还会定义特定的设置。

#### 超时报表 {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**日期粒度** X轴的时间单位（例如，天、小时）。

**量度**&#x200B;要显示的事件列表。

**元素**&#x200B;划分图形中量度数据的元素列表。

#### 排名列表报表 {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**元素**&#x200B;在图形中划分量度数据的元素。

**量度**&#x200B;要显示的事件。

**否。 排名最前的项目**&#x200B;报告显示的项目数。

#### 排名报表 {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**量度**&#x200B;要显示的事件。

**元素**&#x200B;在图形中划分量度数据的元素。

#### 顶级网站区域报表 {#top-site-section-report}

此组件根据以下配置显示一个图形，其中显示了网站中访问次数最多的部分。

![chlimage_1-29](assets/chlimage_1-29a.png)

**否。 排名最前的项目**&#x200B;报表中显示的节数。

#### 趋势报表 {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**日期粒度** X轴的时间单位（例如，天、小时）。

**量度**&#x200B;要显示的事件。

**元素**&#x200B;在图形中划分量度数据的元素。

## 扩展功能板 {#extending-dashboard}

### 概述 {#overview-1}

仪表板是普通页面(`cq:Page`)，因此任何组件都可以用于组装仪表板。

有一个默认组件组`Dashboard`，其中包含模板上默认启用的Analytics报表组件。

### 创建功能板模板 {#creating-a-dashboard-template}

模板定义新功能板的默认内容。 您可以使用多个模板来创建不同类型的功能板。

功能板模板与其他页面模板一样创建，只是它们存储在`/libs/cq/dashboards/templates/`下。 请参阅[创建Contentpage模板](/help/sites-developing/website.md#creating-the-contentpage-template)部分。

>[!NOTE]
>
>仪表板模板在用户之间共享。

### 开发功能板组件 {#developing-a-dashboard-component}

开发功能板组件包括创建常规AEM组件。 本节介绍显示前10个贡献者的组件的示例。

![chlimage_1-31](assets/chlimage_1-31a.png)

顶级创作组件存储在`/apps/geometrixx-outdoors/components/reporting`的存储库中，由：

1. 读取jcr数据并定义`html`占位符的`jsp`文件。

1. 客户端库，其中包含一个`js`文件，该文件用于提取和排序数据，然后填充`html`占位符。

![chlimage_1-32](assets/chlimage_1-32a.png)

以下JavaScript文件在`geout.reporting.topauthors` [客户端库](/help/sites-developing/clientlibs.md)中定义为组件本身的子项。

[QueryBuilder](/help/sites-developing/querybuilder-api.md)用于查询存储库以读取`cq:AuditEvent`节点。 查询结果是JSON对象，将从该对象中提取作者贡献。

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

`JSP`包括`global.jsp`和`clientlib`。

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
