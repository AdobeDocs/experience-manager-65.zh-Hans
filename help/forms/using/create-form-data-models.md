---
title: 创建表单数据模型
description: 了解如何在不配置数据源的情况下创建表单数据模型。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
docset: aem65
feature: Form Data Model
exl-id: 7f5978c3-6c9f-4ce4-b0fb-660ac1d49244
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 1%

---

# 创建表单数据模型{#create-form-data-model}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/create-form-data-models.html) |
| AEM 6.5 | 本文 |


![hero-image](do-not-localize/data-integration.png)

AEM Forms数据集成提供了一个直观的用户界面，用于创建和使用表单数据模型。 表单数据模型依赖于数据源进行数据交换；但是，您可以创建具有或不具有数据源的表单数据模型。 根据您是否配置了数据源，可使用两种方法从数据模型创建：

* **使用预配置的数据源**：如果您已按照中的说明配置数据源 [配置数据源](../../forms/using/configure-data-sources.md)，您可以在创建表单数据模型时选择它们。 它提供选定数据源中的所有数据模型对象、属性和服务，可用于表单数据模型。

* **无数据源**：如果尚未为表单数据模型配置数据源，则仍可以创建它而不使用数据源。 您可以使用表单数据模型创作自适应表单和交互式通信，并使用示例数据测试它们。 当数据源可用时，您可以将表单数据模型与数据源绑定，数据源会自动反映在关联的自适应表单和交互式通信中。

>[!NOTE]
>
>您必须同时是这两个角色的成员 **fdm-author** 和 **forms-user** 组才能创建和使用表单数据模型。 请联系您的AEM管理员以成为组的成员。

## 创建表单数据模型 {#data-sources}

请确保已配置要在表单数据模型中使用的数据源，如中所述 [配置数据源](../../forms/using/configure-data-sources.md). 执行以下操作以基于配置的数据源创建表单数据模型：

1. 在AEM创作实例中，导航到 **[!UICONTROL Forms >数据集成]**.
1. 选择 **[!UICONTROL 创建>表单数据模型]**.
1. 在创建表单数据模型对话框中：

   * 指定表单数据模型的名称。
   * (**可选**)指定表单数据模型的标题、描述和标记。
   * (**可选，并且仅在配置了数据源时适用**)选择旁边的勾号图标 **[!UICONTROL 数据源配置]** 字段并选择您要使用的数据源的云服务所在的配置节点。 它将在下一页上可供选择的数据源列表限制为所选配置节点中的可用数据源列表。 但是，默认情况下会列出所有JDBC数据库和AEM用户配置文件数据源。 如果不选择配置节点，则会列出所有配置节点的数据源。

   选择&#x200B;**[!UICONTROL 下一步]**。

1. (**仅在配置了数据源时适用**) **[!UICONTROL 选择数据源]** 屏幕列出了可用的数据源（如果有）。 选择要在表单数据模型中使用的数据源。
1. 选择 **[!UICONTROL 创建]** 在确认对话框中，选择 **[!UICONTROL 打开]** 以打开表单数据模型编辑器。

让我们查看表单数据模型编辑器UI的不同组件。

![具有三个数据源的表单数据模型 — RESTful服务、AEM用户配置文件和RDBMS](assets/fdm-ui.png)

**A.数据源** 列出表单数据模型中的数据源。 展开数据源以查看其数据模型对象和服务。

**B.刷新数据源定义** 从配置的数据源中获取数据源定义中的任何更改，并在表单数据模型编辑器的“数据源”选项卡中更新它们。

**C.模式** 显示添加的数据模型对象的内容区域。

**D.服务** 显示添加的数据源操作或服务的内容区域。

**E.工具栏** 用于处理表单数据模型的工具。 工具栏根据表单数据模型中选定的对象显示更多选项。

**F.添加选定项** 将选定的数据模型对象和服务添加到表单数据模型。

有关表单数据模型编辑器以及如何使用它来编辑和配置表单数据模型的更多信息，请参阅 [使用表单数据模型](../../forms/using/work-with-form-data-model.md).

## 更新数据源 {#update}

执行以下操作以将数据源添加或更新到现有表单数据模型。

1. 转到 **[!UICONTROL Forms >数据集成]**，选择要添加或更新数据源的表单数据模型，然后选择 **[!UICONTROL 属性]**.
1. 在表单数据模型属性中，转到 **[!UICONTROL 更新源]** 选项卡。

   在“更新源”选项卡中：

   * 选择中的浏览图标 **[!UICONTROL 上下文感知配置]** 字段并选择配置节点，您要添加的数据源的云配置驻留在该配置节点上。 如果不选择节点，则仅驻留在 `global` 选择时列出节点 **[!UICONTROL 添加源]**.

   * 要添加新数据源，请选择 **[!UICONTROL 添加源]** 并选择要添加到表单数据模型的数据源。 在中配置的所有数据源 `global` 并显示选定的配置节点（如果有）。

   * 要使用相同类型的另一个数据源替换现有数据源，请选择 **[!UICONTROL 编辑]** 图标并从可用数据源列表中选择。
   * 要删除现有数据源，请选择 **[!UICONTROL 删除]** 图标来访问。 如果将数据源中的数据模型对象添加到表单数据模型中，则“删除”图标将被禁用。

   ![fdm-properties](assets/fdm-properties.png)

1. 选择 **[!UICONTROL 保存并关闭]** 以保存更新。

>[!NOTE]
>
>在表单数据模型中添加新数据源或更新现有数据源后，请确保在使用更新后的表单数据模型的自适应表单和交互式通信中相应地更新绑定引用。

## 后续步骤 {#next-steps}

现在，您拥有一个添加了数据源的表单数据模型。 接下来，可以编辑表单数据模型以添加和配置数据模型对象和服务，添加数据模型对象之间的关联，编辑属性，添加自定义数据模型对象和属性，生成示例数据等。

有关更多信息，请参阅 [使用表单数据模型](../../forms/using/work-with-form-data-model.md).
