---
title: 自定义页面属性的视图
description: 每个页面都有一组可根据需要编辑的属性
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 43%

---

# 自定义页面属性的视图{#customizing-views-of-page-properties}

每个页面都有一组可供用户查看和编辑的[属性](/help/sites-authoring/editing-page-properties.md)；创建页面（创建视图）时需要某些属性，其他属性可在以后的阶段查看和编辑（编辑视图）。 这些页面属性由相应页面组件的对话框(`cq:dialog`)定义和提供。

>[!CAUTION]
>
>在经典UI中，无法自定义页面属性视图。

每个页面属性的默认状态是：

* 在创建视图中隐藏（例如，**创建页面**&#x200B;向导）

* 在编辑视图中可用（例如，**查看属性**）

如果需要任何更改，则必须专门配置字段。这是使用相应的节点属性完成的：

* 页面属性在创建视图中可用（例如，**创建页面**&#x200B;向导）：

   * 名称：`cq:showOnCreate`
   * 类型：`Boolean`

* 编辑视图中可用的页面属性（例如，**视图**/**编辑**）**属性**&#x200B;选项)：

   * 名称：`cq:hideOnEdit`
   * 类型：`Boolean`

例如，查看Foundation Page组件的&#x200B;**Basic**&#x200B;选项卡上&#x200B;**More Titles and Description**&#x200B;下分组的字段的设置。 这些内容在&#x200B;**创建页面**&#x200B;向导中可见，因为`cq:showOnCreate`已设置为`true`：

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>请参阅[扩展页面属性教程](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html?lang=zh-Hans)，查看有关自定义页面属性的指南。

## 配置页面属性 {#configuring-your-page-properties}

您还可以通过配置页面组件的对话框并应用相应的节点属性来配置可用字段。

例如，默认情况下&#x200B;[**创建页面**&#x200B;向导](/help/sites-authoring/managing-pages.md#creating-a-new-page)会显示在&#x200B;**更多标题和描述**&#x200B;中分组的字段。若要对其进行隐藏，您可以配置：

1. 在 `/apps` 下创建您的页面组件。
1. 为页面组件的 `basic` 部分创建一个覆盖（使用[&#x200B; Sling 资源合并器](/help/sites-developing/sling-resource-merger.md)提供的&#x200B;*对话框差异*）；例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >作为参考，请参阅：
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   >
   >但是，您&#x200B;***必须***&#x200B;不更改`/libs`路径中的任何内容。
   >
   >这是因为下次升级实例时`/libs`的内容会被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
   >
   >建议用于配置和其他更改的方法是：
   >
   >1. 在`/apps`下重新创建所需项（即`/libs`中存在的项）
   >1. 在`/apps`中进行任何更改

1. 将 `basic` 上的 `path` 属性设置为指向基本选项卡的覆盖（另请参阅下一步）。例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 在相应路径上创建 `basic`-`moretitles` 部分的覆盖；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 应用适当的节点属性：

   * **名称**：`cq:showOnCreate`
   * **类型**：`Boolean`
   * **值**：`false`

   **更多标题和描述**&#x200B;部分不会再在&#x200B;**创建页面**&#x200B;向导中显示。

>[!NOTE]
>
>配置用于活动副本的页面属性时，有关更多详细信息，请参阅[在页面属性上配置MSM锁定](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui)。

## 页面属性的示例配置 {#sample-configuration-of-page-properties}

此示例演示了[Sling资源合并器](/help/sites-developing/sling-resource-merger.md)的对话框比较技术；包括使用[`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties)。 它还说明了 `cq:showOnCreate` 和 `cq:hideOnEdit` 的用法。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* 在GitHub上[打开aem-authoring-extension-page-dialog项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
