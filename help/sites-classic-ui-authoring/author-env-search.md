---
title: 搜索
description: AEM 的创作环境提供了多种内容搜索机制，具体取决于资源类型。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 1f46a57f-4966-4dd1-8c99-c0740718ae76
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 12%

---

# 搜索{#searching}

AEM 的创作环境提供了多种内容搜索机制，具体取决于资源类型。

>[!NOTE]
>
>在创作环境之外，还可以搜索其他机制，如[查询生成器](/help/sites-developing/querybuilder-api.md)和[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)。

## 搜索基础知识 {#search-basics}

要访问搜索面板，请单击相应控制台左窗格顶部的&#x200B;**搜索**&#x200B;选项卡。

![chlimage_1-101](assets/chlimage_1-101.png)

通过搜索面板，您可以搜索所有网站页面。 它包含用于以下各项的字段和小部件：

* **全文**：搜索指定的文本
* **修改于**&#x200B;之后/之前：仅搜索在特定日期之间更改的页面
* **模板**：仅搜索基于指定模板的页面
* **标记**：仅搜索具有指定标记的页面

>[!NOTE]
>
>当您的实例配置为[Lucene搜索](/help/sites-deploying/queries-and-indexing.md)时，您可以在&#x200B;**全文**&#x200B;中使用以下内容：
>
>* [通配符](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [布尔运算符](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)
>
>* [正则表达式](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [字段分组](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [提升](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)
>

单击窗格底部的&#x200B;**搜索**&#x200B;以执行搜索。 单击&#x200B;**重置**&#x200B;以清除搜索条件。

## 过滤器 {#filter}

在不同的位置，可以设置（和清除）过滤器以向下钻取并优化您的视图：

![chlimage_1-102](assets/chlimage_1-102.png)

## 查找和替换 {#find-and-replace}

在&#x200B;**网站**&#x200B;控制台中，**查找和替换**&#x200B;菜单选项允许您搜索和替换网站部分字符串的多个实例。

1. 选择要执行查找和替换操作的根页面或文件夹。
1. 选择&#x200B;**工具**，然后选择&#x200B;**查找和替换**：

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. **查找和替换**&#x200B;对话框执行以下操作：

   * 确认查找操作应从何处开始的根路径
   * 定义要找到的术语
   * 定义应替换它的术语
   * 指示搜索是否应区分大小写
   * 指示是否只应找到全字（否则还会找到子字符串）

   单击&#x200B;**预览**&#x200B;列出已找到术语的列表。 您可以选择/清除要替换的特定实例：

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. 单击&#x200B;**替换**&#x200B;以实际替换所有实例。 系统将要求您确认该操作。

查找和替换servlet的默认范围包括以下属性：

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

可以使用Apache Felix Web管理控制台更改范围（例如，在`https://localhost:4502/system/console/configMgr`）。 选择`CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)`并根据需要配置作用域。

>[!NOTE]
>
>在标准AEM安装中，“查找和替换”使用Lucene进行搜索功能。
>
>Lucene索引长度最大为16k的字符串属性。 超出此范围的字符串将不会被搜索。
