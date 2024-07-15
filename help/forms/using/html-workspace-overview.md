---
title: 使用AEM Forms工作区
description: 通过流程工作流的此快速概述开始使用AEM Forms工作区。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# 使用AEM Forms工作区{#working-with-aem-forms-workspace}

## 简介 {#introduction}

AEM Forms工作区是AEM Forms的一部分。 除了PDF forms之外，Workspace还促进了HTMLForms的演绎版。 现在，您可以从移动界面和Web应用程序参与业务流程。

此外，AEM Forms工作区可通过使用标准HTML和JavaScript™开发方法进行高度自定义。 它是一个基于组件的软件，可轻松与其他Web应用程序集成。

有关详细信息，请参阅[AEM Forms工作区简介](/help/forms/using/introduction-html-workspace.md)。

## 熟悉 {#getting-familiar}

要熟悉创建表单应用程序以实现业务流程自动化的端到端过程，请按照以下步骤进行操作。 按照演练后的步骤，您可以使用Workbench、Designer和AEM Forms工作区创建、管理和测试应用程序。 有关实施详细信息，请参阅[创建您的第一个AEM Forms应用程序](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html)。

## 功能概述 {#functional-overview}

您可以使用AEM Forms工作区执行以下任务：

**启动业务流程：** AEM Forms工作区将您的流程分类为由您的组织设计和设置的流程。 您可以将经常使用的类别添加到收藏夹，以便快速访问这些类别。 启动流程时，通常会填写表单以启动构成工作流控制的业务流程。 有关详细信息，请参阅[启动进程](/help/forms/using/starting-processes.md)。

**查看任务并对其执行操作：**&#x200B;查看您的待办事项列表时，您会看到业务流程中分配给您、您所属的任何组或其他用户的共享任务。 您可以根据需要打开、处理和完成任务。 通常，完成任务需要提供信息、批准表单或拒绝表单。 有关详细信息，请参阅[处理待办事项列表](/help/forms/using/todo-lists.md)。

**跟踪任务**：要跟踪您的任务，请使用AEM Forms工作区的“跟踪”选项卡。 您可以搜索已启动或参与的活动或已完成的流程。 您可以查看作为流程一部分的任务、分配和表单。 您也可以使用之前启动的流程的表单数据启动新流程。 有关详细信息，请参阅[跟踪进程](/help/forms/using/tracking-processes.md)。

## AEM Forms工作区的新增功能 {#new-offering-of-aem-forms-workspace}

**支持批量批准任务**：

您可以批准同一类型的多个任务。 选择一个任务进行批准后，只有具有相同流程、相同任务名称和相同路由选项的任务才会保持启用状态。 有关实施详细信息，请参阅[处理待办事项列表](/help/forms/using/todo-lists.md)。

## 从Flex Workspace迁移到AEM Forms工作区 {#migrating-from-flex-workspace-to-aem-forms-workspace}

AEM Forms客户不支持Flex Workspace。 所有使用Flex Workspace的客户都应迁移到AEM Forms Workspace。

在AEM Forms工作区中，与XDP表单关联的默认操作配置文件中的默认呈现和提交服务已更改，并且引入了新服务。 有关详细信息，请参阅[新渲染和提交服务](/help/forms/using/new-render-submit-service.md)。 若要迁移与XDP表单一起使用的现有流程，若要使用这些服务，您可以执行[这些步骤](new-render-submit-service.md)。

**将Flex Workspace自定义项映射到AEM Forms工作区**

两个工作区中各种自定义项之间的映射如下所示。

<table>
 <tbody>
  <tr>
   <td><strong>自定义类型 </strong></td>
   <td><strong>自定义项已覆盖 </strong></td>
   <td><strong>相应的AEM Forms工作区自定义方案</strong></td>
  </tr>
  <tr>
   <td>本地化自定义</td>
   <td>
    <ol>
     <li>更改Workspace的区域设置</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">更改AEM Forms工作区区域设置</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>主题自定义</td>
   <td>
    <ol>
     <li>替换图像</li>
     <li>修改颜色</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">更改组织徽标</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">更改颜色方案</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>版面自定义</td>
   <td>
    <ol>
     <li>简化Workspace用户界面<br /> </li>
     <li>创建新的登录屏幕</li>
     <li>创建自定义审批容器</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">使用可重用组件</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">创建登录屏幕</a></li>
     <li>审批容器已弃用。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Flex WorkspaceAEM Forms工作区中未提供的某些功能包括：消息和通知、欢迎页面、审批容器以及管理列标题的选项。 有关完整列表，请参阅[Flex Workspace在AEM Forms工作区中不可用的功能](/help/forms/using/features-flex-workspace-available-html.md)。

## 使用AEM Forms工作区进行开发 {#developing-with-aem-forms-workspace}

### 架构 {#architecture}

AEM Forms工作区是托管在CRX™上的基于HTML和JavaScript™的Web应用程序。 在浏览器中打开Workspace URL时，将访问CRX™资源，并在浏览器中将应用程序呈现为HTML页面。 JavaScript库和自定义JavaScript代码可管理应用程序的内部和外部行为，例如用户界面、用户交互和与AEM Forms服务器的通信。 有关详细信息，请参阅AEM Forms工作区[架构](/help/forms/using/html-workspace-architecture.md)。

### AEM Forms工作区自定义 {#aem-forms-workspace-customization}

AEM Forms工作区支持各种自定义设置，以便更新用户界面的布局、外观、功能等。 自定义项涉及更新以下一项或多项内容：

* 用户界面的外观
* 使用语义自定义的功能
* 在其他Web应用程序中重用HTML组件

[自定义](introduction-customizing-html-workspace.md#types-of-customizations)文章说明了此类自定义的类型。

### 设置开发人员环境 {#set-up-the-developer-environment}

AEM Forms工作区交付项包括部署在CRX上的CRX包、包含完整源代码的SDK存档、第三方JavaScript库以及AEM Forms工作区的构建脚本。 使用这些内容设置开发人员环境，以执行上述自定义项。 有关更多详细信息，请参阅[构建AEM Forms工作区代码](introduction-customizing-html-workspace.md#building-html-workspace-code)。

您可以自定义界面和核心功能的主要部分，如字体、颜色方案、徽标、登录屏幕、错误对话框、与第三方应用程序的集成以及第三方应用程序中组件的重用。 您还可以增强“任务摘要”页面上显示的内容，显示任务路由操作的图像，甚至修改用于创建AEM Forms工作区应用程序的低级骨干模型和视图。

### XDP Forms的HTML渲染 {#html-rendering-of-xdp-forms}

默认情况下，对于新流程，XDP表单在桌面上以PDF格式呈现，在平板电脑上以HTML格式呈现。 可以始终以HTML格式呈现XDP表单。 有关详细信息，请参阅[新渲染和提交服务](/help/forms/using/new-render-submit-service.md)。

[移动Forms](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html)功能，它与[配置文件](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html)配合使用，可启用XDP表单的HTML演绎版。 默认情况下，“渲染新HTML表单”使用`default.html`配置文件，您可以更改该配置文件。 您还可以添加在以HTML格式呈现XDP表单之前发生的自定义更改。

## AEM Forms工作区应用程序 {#aem-forms-workspace-app}

要在移动设备上处理您的业务流程，您可以使用AEM Forms的AEM Forms工作区应用程序产品。 有关详细信息，请参阅[AEM Forms工作区应用程序概述](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html)。
