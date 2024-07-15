---
title: 在设计模式下配置默认组件
description: 在设计模式下配置Adobe Experience Manager组件。
exl-id: 5e232886-75c1-4f0f-b359-4739ae035fd3
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 10%

---

# 在设计模式下配置默认组件{#configuring-components-in-design-mode}

现成安装AEM实例后，组件浏览器中会立即显示一组组件选项。

除此之外，还可以使用各种其他组件。 您可以使用设计模式[启用/禁用此类组件](#enable-disable-components)。 启用并位于您的页面后，您可以使用设计模式通过编辑属性参数来[配置组件设计的各个方面](#configuring-the-design-of-a-component)。

>[!NOTE]
>
>编辑这些组件时务必谨慎。 设计设置通常是整个网站设计不可分割的一部分，因此只应由具有适当权限和经验的人进行更改，通常是管理员或开发人员。 有关详细信息，请参阅[开发组件](/help/sites-developing/components.md)。

>[!NOTE]
>
>设计模式仅适用于静态模板。 使用可编辑模板创建的模板应使用[模板编辑器](/help/sites-authoring/templates.md)进行编辑。

>[!NOTE]
>
>设计模式仅适用于作为(`/etc`)下的内容存储的设计配置。
>
>从AEM 6.4开始，建议将设计作为配置数据存储在`/apps`下，以支持连续部署方案。 存储在`/apps`下的设计在运行时不可编辑，并且此类模板的非管理员用户将无法使用设计模式。

这涉及添加或删除在页面的段落系统中允许的组件。 段落系统(`parsys`)是包含所有其他段落组件的复合组件。 段落系统允许作者向页面添加不同类型的组件，因为它包含所有其他段落组件。 每个段落类型都表示为一个组件。

例如，产品页面的内容可能包含包含以下内容的段落系统：

* 产品的图像（采用图像或文本段落的形式）
* 产品描述（作为文本段落）
* 带有技术数据的表格（作为表格段落）
* 表单用户填写（作为表单开头、表单元素和表单结束段落）

>[!NOTE]
>
>有关`parsys`的详细信息，请参阅[开发组件](/help/sites-developing/components.md)和[使用模板和组件的准则](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components)。

>[!CAUTION]
>
>使用本文中介绍的设计模式编辑设计是定义静态模板设计的推荐方法
>
>例如，在CRX DE中修改设计不是最佳实践，此类设计的应用可能与预期行为有所不同。 有关详细信息，请参阅开发人员文档[页面模板 — 静态](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied)。

## 启用/禁用组件 {#enable-disable-components}

启用或禁用组件：

1. 选择&#x200B;**设计**&#x200B;模式。

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. 单击组件。 选中后，组件具有蓝色边框。

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. 单击&#x200B;**父项**&#x200B;图标。

   ![父项](do-not-localize/screen_shot_2018-03-22at103204.png)

   这将选择包含当前组件的段落系统。

1. 段落系统的&#x200B;**配置**&#x200B;图标显示在父级的操作栏中。

   ![配置](do-not-localize/screen_shot_2018-03-22at103256.png)

   选择此项以显示对话框。

1. 使用对话框可定义在编辑当前页面时在组件浏览器中可用的组件。

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   该对话框有两个选项卡：

   * 允许的组件
   * 设置

   **允许的组件**

   在&#x200B;**允许的组件**&#x200B;选项卡上，定义哪些组件可用于parsys。

   * 这些组件按其组件组分组，各组可以展开和折叠。
   * 可以通过选中组名称选择整个组，通过取消选中全部取消选择。
   * 减号表示至少选中了组中的一个而并非所有项目。
   * 可按名称进行搜索来筛选组件。
   * 无论是否应用了过滤器，组件组名称右侧列出的数字都表示这些组中选定组件的总数。

   您可以为每个页面组件定义配置。 如果子页面使用相同的模板和/或页面组件（通常对齐），则相同的配置将应用于相应的段落系统。

   >[!NOTE]
   >
   >自适应表单组件可在自适应表单容器中工作以使用Forms生态系统。 因此，这些组件必须仅在自适应表单编辑器中使用，在站点页面编辑器中不起作用。

   **设置**

   在&#x200B;**设置**&#x200B;选项卡上，您可以定义其他选项，例如，为每个组件绘制锚点，以及定义每个容器的单元格边距。

1. 选择&#x200B;**完成**&#x200B;以保存您的配置。

## 配置组件设计 {#configuring-the-design-of-a-component}

1. 选择&#x200B;**设计**&#x200B;模式。

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. 单击带有蓝色边框的组件。 在此示例中，选择了主页图像组件。

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. 使用&#x200B;**配置**&#x200B;图标打开对话框。

   ![配置图标](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   在“设计”对话框中，您可以根据可用的设计参数配置组件。

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   该对话框有三个选项卡：

   * 主要
   * 功能
   * 样式

   **属性**

   通过&#x200B;**属性**&#x200B;选项卡，可以配置组件的重要设计参数。 例如，对于图像组件，您可以定义允许的最大和最小图像大小。

   **功能**

   通过&#x200B;**功能**&#x200B;选项卡，您可以启用或禁用该组件的其他功能。 例如，对于图像组件，您可以定义图像的方向、可用的裁切选项以及是否可以上传图像。

   **样式**

   **样式**&#x200B;选项卡允许您定义要用于组件的CSS类和样式。

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   使用&#x200B;**添加**&#x200B;按钮向多条目对话框列表添加其他条目。

   ![添加其他条目](assets/chlimage_1-94.png)

   使用&#x200B;**删除**&#x200B;图标从多条目对话框列表中删除条目。

   ![删除](do-not-localize/screen_shot_2018-03-22at103809.png)

   使用&#x200B;**移动**&#x200B;图标重新排列多条目对话框列表中的条目顺序。

   ![移动](do-not-localize/screen_shot_2018-03-22at103816.png)

1. 单击&#x200B;**完成**&#x200B;图标以保存并关闭对话框。
