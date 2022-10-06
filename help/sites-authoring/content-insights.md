---
title: 内容分析
seo-title: Content Insight
description: 内容分析使用 Web 分析和 SEO 推荐提供有关页面性能的信息
seo-description: Content Insight provides information about page performance using web analytics and SEO recommendation
uuid: 32f5b37c-2a82-462a-9f0a-c19bed46e198
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 60f980fd-049e-43c1-8b5d-60a8279b357a
exl-id: 187f3cde-a0db-4c02-9e8b-08272987a67d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 96%

---

# 内容分析{#content-insight}

内容分析使用 Web 分析和 SEO 推荐提供有关页面性能的信息。使用内容分析可决定如何修改页面，或了解以前所做的更改使性能发生何种变化。对于您创作的每个页面，您都可以打开内容分析来分析页面。

![chlimage_1-311](assets/chlimage_1-311.png)

“内容分析”页面的布局会根据您所用设备的屏幕尺寸和方向进行相应更改。

## 报表数据

“内容分析”页面包含使用 Adobe SiteCatalyst、Adobe Target、Adobe Social 和 BrightEdge 数据的报表：

* SiteCatalyst：提供以下量度的报表：

   * 页面查看次数
   * 页面平均逗留时间
   * 源

* Target：关于您的页面包含其选件的营销活动的报表。
* BrightEdge：关于可提高页面对搜索引擎的可见性的页面功能，以及应当实施的推荐功能的报表。

请参阅[打开页面的分析和推荐](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page)。

## 报表时间段

报表会显示您控制的一段时间的数据。调整报表时间段时，报表会自动使用该时间段的数据进行刷新。可视提示会指示页面版本的更改时间，以便您可以比较每个版本的性能。

您还可以指定报表数据的粒度，例如您可以查看每日、每周、每月或每年的数据。

请参阅[更改报表时间段](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period)。

>[!NOTE]
>
>内容分析报表要求您的管理员将 AEM 与 SiteCatalyst、Target 和 BrightEdge 集成在一起。请参阅 [与SightCatalyst集成](/help/sites-administering/adobeanalytics.md), [与Adobe Target集成](/help/sites-administering/target.md)和 [与BrightEdge集成](/help/sites-administering/brightedge.md).

## “查看次数”报表 {#the-views-report}

“查看次数”报表包含以下用于评估页面流量的功能：

* 报表时间段内页面的总查看次数。
* 报表时间段内查看次数的图表：

   * 总查看次数。
   * 独特访客数。

![chlimage_1-312](assets/chlimage_1-312.png)

## “页面平均参与”报表 {#the-page-average-engaged-report}

“页面平均参与”报表包含以下用于评估页面有效性的功能：

* 页面在整个报表时间段内保持打开的平均时间。
* 报表时间段内页面查看平均时长的图表。

![chlimage_1-313](assets/chlimage_1-313.png)

## “源”报表 {#the-sources-report}

“源”报表指示用户导航到页面的方式，例如从搜索引擎结果或使用已知的 URL 进行导航。

![chlimage_1-314](assets/chlimage_1-314.png)

## “跳出次数”报表 {#the-bounces-report}

“跳出次数”报表包含一个图表，显示在选定报表时间段内页面发生的跳出次数。

![chlimage_1-315](assets/chlimage_1-315.png)

## “&lt;营销活动名称> 活动”报表 {#the-campaign-activity-report}

对于页面处于激活状态的每个营销活动，均会显示一个名为“*&lt;营销活动名称>* 活动”的报表。该报表显示了为其提供选件的每个区段的页面展示次数和转化次数。

![chlimage_1-316](assets/chlimage_1-316.png)

## “SEO 推荐”报表 {#the-seo-recommendations-report}

“SEO 推荐”报表包含页面的 BrightEdge 分析结果。该报表是页面功能的核对清单，用于指示页面包含和未包含的哪些功能可最大限度地提高使用搜索引擎的可查找性。

该报表使您能够创建任务，以便做出改进来提高页面可查找性。推荐指示已创建相关任务来实施推荐。请参阅[为 SEO 推荐分配任务](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations)。

![chlimage_1-317](assets/chlimage_1-317.png)
