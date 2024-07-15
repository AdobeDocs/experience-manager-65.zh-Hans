---
title: 用于管理任务的收件箱
description: 使用Adobe Experience Manager 6.5中的收件箱管理您的任务。
exl-id: 80b7f179-b011-4f90-b5ab-9ef8a669d271
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 39%

---

# 您的收件箱{#your-inbox}

您可以从AEM的各个区域接收通知，包括工作流和项目；例如，关于：

* 任务：

   * 这些任务也可以在AEM UI的不同位置创建，例如，在&#x200B;**项目**&#x200B;下，
   * 这些任务可以是工作流&#x200B;**创建任务**&#x200B;或&#x200B;**创建项目任务**&#x200B;步骤的产物。

* 工作流程：

   * 表示您需要对页面内容执行的操作的工作项；

      * 这些是工作流&#x200B;**参与者**&#x200B;步骤的产物

   * 失败项目，以允许管理员重试失败的步骤。

您可以在自己的收件箱中接收这些通知，以便查看并采取相应操作。

>[!NOTE]
>
>现成的AEM预先加载了分配给管理员用户组的管理任务。 有关详细信息，请参阅[现成管理任务](#out-of-the-box-administrative-tasks)。

>[!NOTE]
>
>有关这些项目类型的更多信息，另请参阅：
>
>* [项目](/help/sites-authoring/touch-ui-managing-projects.md)
>* [项目 – 处理任务](/help/sites-authoring/task-content.md)
>* [工作流程](/help/sites-authoring/workflows.md)
>* [Forms](/help/forms/using/introduction-aem-forms.md)
>

## 标题中的收件箱 {#inbox-in-the-header}

任何控制台的标题中都会显示收件箱中的当前项目数。也可以打开指示器，以提供对需要操作的页面的快速访问或对收件箱的访问：

![wf-80](assets/wf-80.png)

>[!NOTE]
>
>某些操作也将显示在[相应资源的卡片视图](/help/sites-authoring/basic-handling.md#card-view)中。

## 开箱即用的管理任务  {#out-of-the-box-administrative-tasks}

现成的AEM预加载了分配给管理员用户组的四个任务。

* [配置分析和定位](/help/sites-administering/opt-in.md)
* [应用 AEM 安全核对清单](/help/sites-administering/security-checklist.md)
* 收集汇总的使用情况统计数据
* [配置 HTTPS](/help/sites-administering/ssl-by-default.md)

## 打开收件箱 {#opening-the-inbox}

打开 AEM 通知收件箱：

1. 单击工具栏中的指示器。

1. 选择&#x200B;**查看全部**。**AEM收件箱**&#x200B;打开。 收件箱会显示工作流程、项目和任务中的项目。
1. 默认视图为[列表视图](#inbox-list-view)，但您也可以切换到[日历视图](#inbox-calendar-view)。这是通过视图选择器（工具栏，右上方）完成的。

   对于这两个视图，您还可以定义[视图设置](#inbox-view-settings)；可用选项取决于当前视图。

   ![wf-79](assets/inbox-list-view.png)

>[!NOTE]
>
>收件箱作为控制台运行，因此当您完成操作后，可使用[全局导航](/help/sites-authoring/basic-handling.md#global-navigation)或[搜索](/help/sites-authoring/search.md)导航到其他位置。

### 收件箱 – 列表视图 {#inbox-list-view}

此视图列出所有项目以及关键相关信息：

![wf-82](assets/wf-82.png)

### 收件箱 – 日历视图 {#inbox-calendar-view}

此视图根据项目在日历中的位置以及您选择的精确视图显示项目：

![wf-93](assets/wf-93.png)

您可以：

* 选择特定视图；**时间线**，**列**，**列表**

* 指定要根据&#x200B;**计划**&#x200B;显示的任务；**全部**，**计划**，**进行中**，**即将到期**，**已过期**

* 深入查看有关项目的更多详细信息
* 选择日期范围以集中显示视图：

![wf-91](assets/wf-91.png)

### 收件箱 — 设置 {#inbox-view-settings}

对于这两个视图（列表和日历），您可以定义设置：

* **日历视图**

  对于&#x200B;**日历视图**，您可以配置：

   * **分组依据**
   * **计划**&#x200B;或&#x200B;**无**
   * **卡片大小**

  ![wf-92](assets/wf-92.png)

* **列表视图**

  对于&#x200B;**列表视图**，您可以配置排序机制：

   * **排序字段**
   * **排序顺序**

  ![wf-83](assets/inbox-settings.png)

### 收件箱 — 管理员控制 {#inbox-admin-control}

Admin Control选项允许管理员：

* 自定义AEM收件箱列

* 自定义标题文本和徽标

* 控制标题中可用的导航链接的显示

“管理员控制”选项仅对`administrators`或`workflow-administrators`组的成员可见。

* **列自定义**：自定义AEM收件箱以更改列的默认标题、重新排序列的位置并根据工作流的数据显示其他列。
   * **添加列**：选择要在AEM收件箱中添加的列。
   * **编辑列**：将鼠标悬停在列标题上，并选择![编辑](assets/edit.svg)图标以输入列显示名称。
   * **删除列**：选择![删除](assets/delete_updated.svg)图标以从AEM收件箱中删除该列。
   * **移动列**：拖动![移动](assets/move_updated.svg)图标以将列移动到AEM收件箱中的新位置。

  ![admin-control](assets/admin-control-column-customize.png)

* **品牌自定义**

   * **自定义标题文本：**&#x200B;指定要显示在标题中的文本以替换默认的&#x200B;**Adobe Experience Manager**&#x200B;文本。

   * **自定义徽标：**&#x200B;指定要在标题中显示的图像为徽标。 在数字资产管理(DAM)中上传图像，并在字段中引用该图像。

* **用户导航**
   * **隐藏导航选项：**&#x200B;选择此选项可隐藏标题中可用的导航选项。 导航选项包括指向其他解决方案的链接、帮助链接，以及点按Adobe Experience Manager徽标或文本时可用的创作选项。
* **保存：**&#x200B;单击此选项可保存设置。

## 对某个项目执行操作 {#taking-action-on-an-item}

>[!NOTE]
>
>尽管可以选择多个项目，但一次只能对一个项目执行操作。


1. 要对某个项目执行操作，请选择相应项目的缩略图。工具栏中显示适用于该项目的操作图标：

   ![wf-84](assets/wf-84.png)

   这些操作适用于该项目，具体包括：

   * **完成**&#x200B;操作；例如，任务或工作流项目。
   * **重新分配**/**代理**&#x200B;项目。
   * **打开**&#x200B;项目；根据项目类型，此操作可以：

      * 显示项目属性
      * 打开相应的功能板或向导以执行进一步操作
      * 打开相关文档

   * **回退**&#x200B;到上一步。
   * 查看工作流的有效负荷。
   * 从该项创建项目。

   >[!NOTE]
   >
   >有关更多信息，请参阅：
   >
   >* 工作流项目 – [参与工作流](/help/sites-authoring/workflows-participating.md)

1. 根据所选项目，将启动操作；例如：

   * 将打开与操作对应的对话框。
   * 将启动操作向导。
   * 将打开文档页面。

   例如，**重新分配**&#x200B;将打开一个对话框：

   ![wf-85](assets/wf-85.png)

   根据是否已打开对话框、向导和文档页面，您可以：

   * 确认相应的操作；例如，重新分配。
   * 取消操作。
   * 后退箭头；例如，如果操作向导或文档页面已打开，则可以返回收件箱。

## 创建任务 {#creating-a-task}

您可以从收件箱中创建任务：

1. 选择&#x200B;**创建**，然后选择&#x200B;**任务**。
1. 完成&#x200B;**基本**&#x200B;和&#x200B;**高级**&#x200B;选项卡中的必需字段；只有&#x200B;**标题**&#x200B;是必填项，所有其他字段都是可选的：

   * **基本**:

      * **标题**
      * **项目**
      * **被分派人**
      * **内容**；与有效负荷类似，这是从任务到存储库中位置的引用
      * **描述**
      * **任务优先级**
      * **开始日期**
      * **到期日期**

   ![wf-86](assets/wf-86.png)

   * **高级**

      * **名称**：用于构成URL；如果留空，它将基于&#x200B;**标题**。

   ![wf-87](assets/wf-87.png)

1. 选择&#x200B;**提交**。

## 创建项目 {#creating-a-project}

对于某些任务，您可以创建一个基于该任务的[项目](/help/sites-authoring/projects.md)：

1. 通过点按/单击缩略图选择相应的任务。

   >[!NOTE]
   >
   >只有使用&#x200B;**收件箱**&#x200B;的&#x200B;**创建**&#x200B;选项创建的任务才能用于创建项目。
   >
   >工作项（来自工作流）不能用于创建项目。

1. 从工具栏中选择“**创建项目**”以打开向导。
1. 选择相应的模板，然后选择&#x200B;**下一步**。
1. 指定所需属性：

   * **基本**

      * **标题**
      * **描述**
      * **开始日期**
      * **到期日期**
      * **用户**&#x200B;和角色

   * **高级**

      * **名称**

   >[!NOTE]
   >
   >有关完整信息，请参阅[创建项目](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project)。

1. 选择&#x200B;**创建**&#x200B;以确认操作。

## 筛选 AEM 收件箱中的项目 {#filtering-items-in-the-aem-inbox}

您可以筛选列出的项目：

1. 打开 **AEM 收件箱**。

1. 打开过滤器选择器：

   ![wf-88](assets/wf-88.png)

1. 您可以根据一系列条件筛选列出的项目，其中许多条件可以进行细化；例如：

   ![wf-89](assets/wf-89.png)

   >[!NOTE]
   >
   >通过[视图设置](#inbox-view-settings)，您还可以在使用[列表视图](#inbox-list-view)时配置排序顺序。
