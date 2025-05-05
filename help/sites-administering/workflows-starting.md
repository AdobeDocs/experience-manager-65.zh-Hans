---
title: 启动工作流
description: 了解如何管理Adobe Experience Manager中的工作流，以便您可以使用各种方法（手动或自动）启动它们。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 84a1964c-4121-4763-b946-9eee6093747d
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%

---

# 启动工作流{#starting-workflows}

管理工作流时，您可以使用各种方法启动它们：

* 手动:

   * 来自[工作流模型](#workflow-models)。
   * 正在使用工作流包进行[批次处理](#workflow-packages-for-batch-processing)。

* 自动：

   * 响应节点更改；[使用启动器](#workflows-launchers)。

>[!NOTE]
>
>作者也可以使用其他方法；有关完整的详细信息，请参阅：
>
>* [将工作流应用到页面](/help/sites-authoring/workflows-applying.md)
>* [如何将工作流应用于DAM资源](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [翻译项目](/help/sites-administering/tc-manage.md)
>

## 工作流模型 {#workflow-models}

您可以基于“工作流模型”控制台上列出的模型[&#128279;](/help/sites-administering/workflows.md#workflow-models-and-instances)启动工作流。 唯一强制提供的信息是有效负载，不过也可以添加标题和/或评论。

## 工作流启动器 {#workflows-launchers}

工作流启动器监控内容存储库中的更改，从而根据已更改节点的位置和资源类型启动工作流。

使用&#x200B;**启动器**，您可以：

* 请参阅已为特定节点启动的工作流。
* 选择在创建/修改/删除特定节点/节点类型时要启动的工作流。
* 删除现有的工作流与节点关系。

可以为任何节点创建启动器。 但是，对某些节点所做的更改不会启动工作流。 对以下路径下的节点所做的更改不会导致工作流启动：

* `/var/workflow/instances`
* 位于`/home/users`分支中任意位置的任何工作流收件箱节点
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * 异常：对`/var/statistics/tracking` *do*&#x200B;下的节点所做的更改会导致工作流启动。

标准安装包含各种定义。 这些资源用于数字资产管理和社会协作任务：

![wf-100](assets/wf-100.png)

## 用于批处理的工作流包 {#workflow-packages-for-batch-processing}

工作流包是可作为有效负荷传递到工作流以供处理的包，从而允许处理多个资源。

工作流包：

* 包含指向一组资源（如页面、资产）的链接。
* 保存文件包信息，例如创建日期、创建文件包的用户以及简短说明。
* 使用专用页面模板定义；此类页面允许用户指定包中的资源。
* 可以多次使用。
* 可以在工作流实例实际运行时由用户更改（添加或删除资源）。

## 从模型控制台启动工作流 {#starting-a-workflow-from-the-models-console}

1. 使用&#x200B;**工具**、**工作流**&#x200B;和&#x200B;**模型**&#x200B;导航到&#x200B;**模型**&#x200B;控制台。
1. 选择工作流（根据控制台视图）；如有必要，您还可以使用搜索（左上方）：

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >**[临时](/help/sites-developing/workflows.md#transient-workflows)**&#x200B;指示器显示未保留工作流历史记录的工作流。

1. 从工具栏中选择&#x200B;**启动工作流**。
1. “运行工作流”对话框打开，您可以指定：

   * **有效负荷**

     这可以是页面、节点、资产、包和其他资源。

   * **标题**

     帮助标识此实例的可选标题。

   * **评论**

     帮助指示此实例详细信息的可选注释。

   ![wf-104](assets/wf-104.png)

## 创建启动器配置 {#creating-a-launcher-configuration}

1. 使用&#x200B;**工具**、**工作流**，然后使用&#x200B;**启动器**&#x200B;导航到&#x200B;**工作流启动器**&#x200B;控制台。
1. 选择&#x200B;**创建**，然后选择&#x200B;**添加启动器**&#x200B;以打开对话框：

   ![wf-105](assets/wf-105.png)

   * **事件类型**

     启动工作流的事件类型：

      * 已创建
      * 修改时间
      * 已删除

   * **节点类型**

     工作流启动器应用的节点类型。

   * **路径**

     工作流启动器应用的路径。

   * **运行模式**

     工作流启动器应用于的服务器的类型。 选择&#x200B;**作者**、**Publish**&#x200B;或&#x200B;**作者与Publish**。

   * **条件**

     节点值的条件列表，在评估后用于确定是否启动工作流。 例如，如果节点的属性名称值为User，则以下条件会导致启动工作流：

     名称==用户

   * **功能**

     要启用的功能列表。 使用下拉选择器选择所需的功能。

   * **已禁用的功能**

   要禁用的功能列表。 使用下拉选择器选择所需的功能。

   * **工作流模型**

     当事件类型发生在定义条件下的节点类型和/或路径上时要启动的工作流。

   * **描述**

     您自己的文本，用于描述和标识启动器配置。

   * **激活**

     控制是否激活工作流启动器：

      * 选择&#x200B;**启用**&#x200B;以在满足配置属性时启动工作流。
      * 选择&#x200B;**当工作流不应执行时禁用**（即使满足配置属性时也不应执行）。

   * **排除列表**

     这指定在确定是否应触发工作流时要排除的任何JCR事件（即忽略）。

     此启动器属性是以逗号分隔的项目列表：&#39;&#39;

      * `property-name`忽略在指定的属性名称上触发的任何`jcr`事件。&quot;
      * `event-user-data:<*someValue*>`忽略任何包含通过[`ObservationManager` API](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String))设置的`*<someValue*`> `user-data`的事件。

     例如：

     `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

     此功能可用于通过添加排除项来忽略由其他工作流进程触发的任何更改：

     `event-user-data:changedByWorkflowProcess`

1. 选择&#x200B;**创建**&#x200B;以创建启动器并返回到控制台。

   当发生相应的事件时，将触发启动器，并启动工作流。

## 管理启动器配置 {#managing-a-launcher-configuration}

创建启动器配置后，您可以使用同一控制台选择实例，然后&#x200B;**查看属性**（并进行编辑）或&#x200B;**删除**。
