---
title: 进程报告中的临时查询
description: 创建自定义查询以在Process Reporting中搜索AEM Forms on JEE流程和任务详细信息
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: a096eea0-b2fb-4d86-b729-ca47611135b2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---

# 进程报告中的临时查询{#ad-hoc-queries-in-process-reporting}

## 进程报告中的临时查询 {#ad-hoc-queries-in-process-reporting-1}

通过Process Reporting中的临时查询，可创建自定义查询，用于搜索在AEM Forms环境中定义的AEM Forms流程实例的流程和任务详细信息。

此外，可以使用进程和任务属性过滤器定义临时查询。 然后，可以保存这些过滤器，并用于在以后运行报表。

[**进程搜索**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p)：使用基于进程属性的用户定义的搜索筛选器搜索进程实例。

[**进程详细信息**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p)：通过指定进程ID查看进程实例的详细信息。

**任务搜索**：使用用户定义的基于任务属性的搜索筛选器搜索任务实例。

**任务详细信息**：通过指定任务ID查看任务实例的详细信息。

### 流程和任务 {#processes-and-tasks}

为流程详细信息创建筛选器和运行查询所遵循的步骤与为任务执行的步骤相同。

这意味着“进程搜索”和“任务搜索”的用户界面仅在可搜索的字段和搜索结果中返回的字段上有所不同。 这只是因为，尽管许多字段是相同的，但某些字段是特定于流程的，而某些字段是特定于任务的。

本文详细介绍了“流程/任务搜索”和“流程/任务详细信息”部分。 在适当的位置，任何具体的差异都将被特别指出。

## 进程/任务搜索 {#process-task-search}

您可以使用“进程/任务搜索”来定义用于查询进程/任务实例的筛选器。

### 创建流程/任务搜索查询 {#to-create-a-process-task-search-query}

1. 要查看已保存的进程/任务搜索查询或创建查询，请单击&#x200B;**临时查询**，然后单击&#x200B;**进程/任务搜索**。

   ![搜索节点](assets/search_nodes.png)

   树视图右侧显示&#x200B;**我的筛选器**&#x200B;面板。

   在&#x200B;**我的筛选器**&#x200B;面板中，您可以创建新的临时查询，然后单击以执行以前保存的查询。

   ![my_filters_panel](assets/my_filters_panel.png)

1. 要执行现有查询，只需单击&#x200B;**我的筛选器**&#x200B;面板中的查询即可。
1. 要创建查询，请单击&#x200B;**添加** (+)。

   此时会显示&#x200B;**创建筛选器**&#x200B;面板。

   ![create_filter_panel](assets/create_filter_panel.png)

   查询由一个或多个查询筛选器组成。 要创建筛选器，请向查询添加筛选器行。 默认情况下，会向查询添加一个筛选器行。

   **定义筛选器**

   1. 选择一个字段。

      ![filter_field](assets/filter_field.png)

      >[!NOTE]
      >
      >字段列表包含特定于AEM Forms流程/任务的字段。

   1. 选择条件。

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >列出的条件取决于选择进行筛选的属性。

   1. 输入一个值。

      ![filter_value](assets/filter_value.png)

   1. 若要向查询中添加其他筛选器，请单击筛选器行右侧的&#x200B;**添加(+)**。

      要从查询中删除筛选器，请单击筛选器行右侧的&#x200B;**删除(-)**。

      ![filter_add_del](assets/filter_add_del.png)

创建查询后，使用&#x200B;**创建过滤器**&#x200B;面板右上角的选项可以：

* **取消**：取消更改并返回&#x200B;**我的筛选器**&#x200B;面板。
* **运行**：执行当前查询以查看和/或验证结果。 在这种情况下，您无需在执行查询之前保存查询。 您可以验证结果，必要时进行更改，然后在您对输出感到满意时保存查询。
* **保存**：保存筛选器。 然后可以从&#x200B;**我的筛选器**&#x200B;面板查看和执行筛选器。

### “我的筛选器”面板中的选项 {#options-in-my-filters-panel}

使用&#x200B;**我的筛选器**&#x200B;面板中的选项以&#x200B;**添加** ![lc_pr_add_filter](assets/lc_pr_add_filter.png)、**编辑** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png)或&#x200B;**删除** ![lc_pr_edit_filter](assets/lc_pr_edit_filter.png)即席查询。

![my_filters_options](assets/my_filters_options.png)

### 执行搜索查询 {#to-execute-a-search-query}

1. 若要执行查询，请单击“**我的筛选器**”面板中的筛选器，如果要创建或编辑筛选器，请单击“**运行**”按钮。
1. 查询的结果显示在&#x200B;**进程报告**&#x200B;窗口的&#x200B;**报告**&#x200B;面板中。

   ![process_search_result](assets/process_search_result.png)

   您可以借助报表底部显示的分页面板对搜索结果进行分页。

   ![process_result_pgn](assets/process_result_pgn.png)

   在&#x200B;**显示**&#x200B;下拉列表中，选择每页显示的结果数。

   在&#x200B;**Page**&#x200B;文本框中，输入一个页码以直接转到该页面。

1. “进程搜索”结果中将显示以下字段：

   * **进程ID**：进程的ID。 该字段为超链接。 如果单击此字段中的进程ID，您将被重定向到该进程的&#x200B;**[!UICONTROL 进程详细信息]**&#x200B;面板。
   * **启动器**：启动进程实例的AEM Forms用户
   * **创建时间**：进程实例的启动日期和时间
   * **完成时间**：进程实例完成的日期和时间
   * **持续时间**：流程实例从开始到完成的持续时间
   * **状态**：进程实例的当前状态。

   默认情况下，结果按进程ID排序。 但是，要按任意字段对结果进行排序，请单击字段标题。

   由于排序操作是切换操作，因此单击列标题可对结果进行升序排序，再次单击列标题可对结果进行降序排序。

   同样，以下字段显示在“任务搜索”结果中：

   * **任务ID**：任务的标识。 该字段为超链接。 如果单击此字段中的任务ID，您将被重定向到该任务的&#x200B;**[!UICONTROL 任务详细信息]**&#x200B;面板。
   * **启动器**：启动进程实例的AEM Forms用户
   * **创建时间**：进程实例的启动日期和时间
   * **完成时间**：进程实例完成的日期和时间
   * **持续时间**：流程实例从开始到完成的持续时间
   * **状态**：进程实例的当前状态。

   默认情况下，结果按任务ID排序。 但是，要按任意字段对结果进行排序，请单击字段标题。 结果按列排序，该列由列标题旁边的深色箭头指示。

   由于排序是切换操作，请单击字段标题对结果进行升序排序，然后再次单击该标题对结果进行降序排序。 当前排序顺序（升序/降序）由列标题旁边的变暗箭头方向指示。

   ![task_search_result](assets/task_search_result.png)

1. 单击左上角的边栏按钮![lc_pr_rail_button](assets/lc_pr_rail_button.png)以折叠&#x200B;**我的筛选器**&#x200B;窗格并展开&#x200B;**报表**&#x200B;面板的可用空间。
1. 使用&#x200B;**报表**&#x200B;面板右上角的选项对查询结果执行操作。

   * **刷新**：使用存储中的最新数据刷新报告

   * **导出到CSV**：将报表数据导出到以逗号分隔的文件。

   >[!NOTE]
   >
   >导出报告时，搜索结果的整个结果将导出到CSV文件，而不仅仅是当前页面

## 流程/任务详细信息 {#process-task-details}

您可以使用&#x200B;**进程详细信息**&#x200B;面板查看特定进程的详细信息。

同样，您可以使用&#x200B;**任务详细信息**&#x200B;面板查看特定任务的详细信息。

### 查看流程/任务详细信息 {#to-view-process-task-details}

您可以查看特定AEM Forms流程/任务的详细信息：

* **来自进程/任务搜索结果**
* **在“进程/任务详细信息”面板中输入进程/任务ID**

#### 从进程/任务搜索结果 {#from-a-process-task-search-result}

1. 执行进程/任务搜索。 有关详细信息，请参阅[执行进程搜索查询](#to-execute-a-search-query)。

   请注意，在结果中返回的显示的进程ID是超链接的。

   ![process_id_list](assets/process_id_list.png)

1. 单击列表中的进程ID可在&#x200B;**进程详细信息**&#x200B;面板中查看此进程的详细信息。

   **进程/任务详细信息**&#x200B;查询结果显示进程/任务中包含的任务/表单的详细信息。

   默认情况下，结果按任务/表单ID排序。 但是，要按任意字段对结果进行排序，请单击字段标题。 对结果排序所依据的列由列标题旁边的深色箭头指示。

   由于排序是切换操作，请单击字段标题对结果进行升序排序，然后再次单击该标题对结果进行降序排序。 当前排序顺序（升序/降序）由列标题旁边的变暗箭头方向指示。

   **进程详细信息结果**

   ![process_details](assets/process_details.png)

   **左侧面板：**&#x200B;显示所选进程的以下详细信息：

   * 进程名称
   * 流程创建日期时间
   * 流程完成日期时间
   * 处理持续时间
   * 进程状态
   * 进程发起者

   **右上面板：**&#x200B;显示组成所选进程的任务的以下详细信息：

   * 任务编号
   * 任务名称
   * 任务所有者
   * 任务创建日期时间
   * 任务更新日期时间
   * 任务完成日期时间
   * 任务持续时间
   * 任务状态

   **右下方面板：**&#x200B;显示所选进程的进程历史记录的以下详细信息：

   * 进程名称
   * 进程发起者
   * 流程更新日期时间
   * 流程完成日期时间
   * 进程状态

   **任务详细信息结果**

   ![任务详细信息](assets/task_details.png)

   **左侧面板：**&#x200B;显示所选任务的以下详细信息：

   * 任务名称
   * 此任务所属的进程的ID
   * 任务描述
   * 任务创建日期时间
   * 任务完成日期时间
   * 任务持续时间
   * 任务状态
   * 选定的任务路由

   **右上角面板：**&#x200B;显示构成所选任务的表单的以下详细信息：

   * 文件夹ID
   * 表单创建日期时间
   * 表单更新日期时间
   * 表单模板URL

   **右下方面板：**&#x200B;显示选定任务的进程历史记录的以下详细信息：

   * 任务分配类型
   * 任务所有者
   * 任务分配创建日期时间
   * 任务更新日期时间

1. 单击&#x200B;**返回进程/任务搜索**&#x200B;可返回从中细化进程/任务详细信息的搜索结果。

   ![back_to_search](assets/back_to_search.png)

   但是，如果通过输入特定进程/任务ID找到进程/任务详细信息，则单击“返回进程/任务搜索”将返回&#x200B;**进程/任务搜索**，而不显示任何搜索结果。

#### 在“流程/任务详细信息”面板中输入流程/任务ID {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. 转到&#x200B;**进程/任务详细信息**&#x200B;面板。

   ![details_nodes](assets/details_nodes.png)

1. 在“流程/任务ID”文本框中，输入流程/任务ID。

   ![process_details-1](assets/process_details-1.png)

   **进程/任务详细信息**&#x200B;查询结果中的字段是特定于AEM Forms进程/任务的字段。

   对于进程，查询结果将显示该进程中所包含任务的详细信息。

   对于任务，查询结果将显示任务中包含的表单的详细信息。
