---
title: 将AEM表单工作区与Microsoft Office SharePoint Server集成
description: 您可以将AEM表单工作区与Microsoft Office SharePoint Server集成。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
exl-id: d080932f-d5fb-482d-9329-62da5df10362
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 将AEM表单工作区与Microsoft Office SharePoint Server集成{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**— 要求**

**必备知识**
在将AEM Forms Workspace添加到SharePoint服务器之前，您必须拥有对具有适当权限的SharePoint服务器的访问权限，并且必须知道用于访问Workspace的URL。 以下步骤假定您熟悉SharePoint Server。 有关SharePoint服务器中Web部件的详细信息，请参阅Windows SharePoint服务中的Web部件。

**用户级别**
开始

您可以在AEM Forms Workspace Office SharePoint Server(例如，Microsoft Office SharePoint Server 2007)中将Microsoft用作Web部件。 用户可以通过使用Web浏览器连接到您的AEM Forms Workspace服务器来访问SharePoint，以提供统一的体验。 在本文中，您将了解在AEM Forms Office SharePoint Server中将Microsoft Workspace显示为Web部件的基本步骤。 您可以执行本文中所述的步骤来提供统一的体验，以便连接到SharePoint服务器的用户可以从同一端口访问AEM Forms Workspace。

>[!NOTE]
>
>本文中列出的步骤特定于Microsoft SharePoint Server 2007。 您还可以将HTML Workspace与其他受支持的Microsoft SharePoint版本一起配置。

## 将AEM Forms Workspace与Microsoft Office SharePoint Server 2007集成 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

执行以下步骤以将AEM Forms Workspace集成到Web部件中：

1. 在Web浏览器中，导航到SharePoint站点，例如`https://[myMOSSserver]:44299/default.aspx`，其中`[myMOSSserver]`是Sharepoint服务器的名称或IP地址。

   >[!NOTE]
   >
   >44299是SharePoint服务器的默认端口号。 端口号取决于您安装的SharePoint Server。

1. 在网页的右上角，单击&#x200B;**网站操作**&#x200B;并选择&#x200B;**编辑页面**。
1. 单击&#x200B;**添加Web部件**&#x200B;按钮。
1. 在“添加Web部件 — 网页”对话框的“其他”下，选择&#x200B;**页面查看器Web部件**，然后单击&#x200B;**添加**。
1. 在“页面查看器Web部件”框中，单击&#x200B;**编辑**&#x200B;并选择&#x200B;**修改共享Web部件**。

   >[!NOTE]
   >
   >页面查看器Web部件框显示在您在步骤3中单击的&#x200B;**添加Web部件**&#x200B;按钮下方，如下图所示（图1）：

   Microsoft Office SharePoint Server中的![页面查看器Web部件框。](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   图1. - Microsoft Office SharePoint Server中的“页面查看器Web部件”框。

1. 在“页面查看器”页上，执行以下任务：

   1. 在链接框中，键入AEM Forms Workspace的URL，如`https://[AEM_forms_Server]:8080/lc/ws`，其中`[AEM_forms_Server]`表示AEM Forms服务器的IP或名称。
   1. 单击&#x200B;**外观**&#x200B;并修改高度、宽度和标题，以便您可以查看整个Workspace用户界面。 例如，可以将高度和宽度分别设置为6英寸和11英寸。
   1. 单击&#x200B;**测试链接**。 将出现一个新的Web浏览器窗口，其中显示Workspace。
   1. （可选）单击&#x200B;**布局**&#x200B;并修改Web部件中Workspace的布局。
   1. （可选）单击&#x200B;**高级**&#x200B;并修改其他设置，如说明以及Web部件中的Workspace是否可以最小化或关闭。

      单击&#x200B;**应用**。

1. 单击&#x200B;**退出编辑模式**&#x200B;并验证您是否可以访问Workspace。

完成上述步骤后，您的SharePoint网站外观类似于下图（图2）：

![AEM Forms Workspace与Microsoft Office SharePoint Server集成](assets/aem-forms-workspace.jpg)

图2 - AEM Forms Workspace与Microsoft Office SharePoint Server集成
