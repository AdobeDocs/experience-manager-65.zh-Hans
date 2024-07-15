---
title: 全面搜索
description: 通过全面的搜索更快地找到您的内容。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: dd65b308-c449-4f64-9f46-0797b922910f
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 58%

---

# 搜索{#searching}

AEM 的创作环境提供了多种内容搜索机制，具体取决于资源类型。

>[!NOTE]
>
>在创作环境之外，还可以搜索其他机制，如[查询生成器](/help/sites-developing/querybuilder-api.md)和[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)。

## 搜索基础知识 {#search-basics}

可从顶部工具栏中使用搜索功能：

![搜索](do-not-localize/chlimage_1-17.png)

使用搜索边栏可以：

* 搜索特定的关键字、路径或标记。
* 根据特定于资源的条件进行筛选，例如修改日期、页面状态、文件大小等。
* 根据以上条件定义并使用[保存的搜索](#saved-searches)。

>[!NOTE]
>
>显示搜索边栏时，还可以使用热键 `/`（正斜杠）调用搜索。

## 搜索和筛选 {#search-and-filter}

要搜索和筛选您的资源，请执行以下操作：

1. 打开&#x200B;**搜索**（使用工具栏中的放大镜）并输入您的搜索词。将提出建议并可进行选择：

   ![s-01](assets/s-01.png)

   默认情况下，搜索结果将被限制在您的当前位置（即控制台和相关资源类型）：

   ![screen_shot_2018-03-23at101445](assets/screen_shot_2018-03-23at101445.png)

1. 如有必要，您可以删除位置筛选器（在要删除的筛选器上选择&#x200B;**X**），以在所有控制台/资源类型之间进行搜索。
1. 结果会显示，并按控制台和相关的资源类型进行分组。

   您可以选择特定资源（用于进一步操作），或通过选择所需的资源类型向下展开；例如，**查看所有站点**：

   ![screen-shot_2019-03-05at101900](assets/screen-shot_2019-03-05at101900.png)

1. 如果您需要进一步向下展开，请选择“边栏”符号（左上方）以打开侧面板&#x200B;**过滤器和选项**。

   ![筛选器和选项](do-not-localize/screen_shot_2018-03-23at101542.png)

   根据资源类型，搜索将显示预定义的搜索/筛选条件选择。

   侧面板允许您选择：

   * 保存的搜索
   * 搜索目录
   * 标记
   * 搜索条件；例如，修改日期、Publish状态、LiveCopy状态。

   >[!NOTE]
   >
   >搜索条件可能会视情况而异：
   >
   >
   >
   >    * 具体视您选择的资源类型而定；例如，资源和社区条件理所当然是专用的；
   >    * 您可以自定义作为[搜索Forms](/help/sites-administering/search-forms.md)的实例(对应于在AEM中的位置)。
   >
   >

   ![screen-shot_2019-03-05at102509](assets/screen-shot_2019-03-05at102509.png)

1. 您还可以添加其他搜索词：

   ![screen-shot_2019-03-05at102613](assets/screen-shot_2019-03-05at102613.png)

1. 使用 **X**（右上方）关闭&#x200B;**搜索**。

>[!NOTE]
>
>在搜索结果中选择某个项目时，搜索条件会持续保留。
>
>当您在搜索结果页面上选择某个项目时，如果使用浏览器后退按钮返回到搜索页面，则搜索条件仍将存在。

## 保存的搜索 {#saved-searches}

除了按照多方面条件进行搜索以外，您还可以保存特定的搜索配置以供日后检索和使用：

1. 定义搜索条件，然后选择&#x200B;**保存**。

   ![screen-shot_2019-03-05at102613-1](assets/screen-shot_2019-03-05at102613-1.png)

1. 指定名称，然后使用&#x200B;**保存**&#x200B;进行确认。

   ![screen-shot_2019-03-05at102725](assets/screen-shot_2019-03-05at102725.png)

1. 在下次访问搜索面板时，您可以从选择器中选择保存的搜索：

   ![screen-shot_2019-03-05at102927](assets/screen-shot_2019-03-05at102927.png)

1. 在保存之后，您可以执行以下操作：

   * 使用 **x**（针对保存的搜索的名称）以开始新的查询（保存的搜索本身将不会被删除）。
   * **编辑保存的搜索**，更改搜索条件，然后再次&#x200B;**保存**。

通过选择保存的搜索并单击搜索面板底部的&#x200B;**编辑保存的搜索**，可以修改保存的搜索。

![screen-shot_2019-03-05at103010](assets/screen-shot_2019-03-05at103010.png)
