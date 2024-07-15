---
title: 初始沙盒应用程序
description: 了解如何使用用于创建内容页面的内容模板以及用于呈现网站页面的组件和脚本。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---

# 初始沙盒应用程序 {#initial-sandbox-application}

在此部分中，您将创建以下内容：

* 用于在示例网站中创建内容页面的&#x200B;**[模板](#createthepagetemplate)**。
* 用于呈现网站页面的&#x200B;**[组件和脚本](#create-the-template-s-rendering-component)**。

## 创建内容模板 {#create-the-content-template}

模板用于定义新页面的默认内容。 复杂的网站可能使用多个模板在站点中创建不同类型的页面。 此外，该模板集可以成为用于将更改转出到服务器集群的蓝图。

在本练习中，所有页面都基于一个简单的模板。

1. 在CRXDE Lite的资源管理器窗格中：

   * 选择`/apps/an-scf-sandbox/templates`
   * **[!UICONTROL 创建]** > **[!UICONTROL 创建模板]**

1. 在“创建模板”对话框中，键入以下值，然后单击&#x200B;**[!UICONTROL 下一步]**：

   * 标签： `playpage`
   * 标题： `An SCF Sandbox Play Template`
   * 描述： `An SCF Sandbox template for play pages`
   * 资源类型： `an-scf-sandbox/components/playpage`
   * 排名： &lt;保留为默认值>

   标签用于节点名称。

   资源类型作为属性`sling:resourceType`显示在`playpage`的`jcr:content`节点上。 它标识在浏览器请求时呈现内容的组件（资源）。

   在本例中，使用`playpage`模板创建的所有页面均由`an-scf-sandbox/components/playpage`组件渲染。 按照约定，组件的路径是相对路径，允许Sling先在`/apps`文件夹中搜索资源，如果未找到，则在`/libs`文件夹中搜索资源。

   ![create-content-template](assets/create-content-template-1.png)

1. 如果使用复制/粘贴，请确保“资源类型”值没有前导或尾随空格。

   单击&#x200B;**[!UICONTROL 下一步]**。

1. “允许的路径”是指使用此模板的页面的路径，因此该模板将列在&#x200B;**[!UICONTROL 新页面]**&#x200B;对话框中。

   要添加路径，请单击加号按钮`+`并在显示的文本框中键入`/content(/.&ast;)?`。 如果使用复制/粘贴，请确保没有前导或尾随空格。

   注意：允许的路径属性的值是&#x200B;*正则表达式*。 路径与表达式匹配的内容页面可以使用模板。 在这种情况下，正则表达式与&#x200B;**/content**&#x200B;文件夹及其所有子页面的路径匹配。

   当作者在`/content`下创建页面时，标题为“SCF沙盒页面模板”的`playpage`模板出现在要使用的可用模板列表中。

   从模板创建根页面后，可以通过编辑属性以在正则表达式中包含根路径来限制此网站对该模板的访问。

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在&#x200B;**[!UICONTROL 允许的父项]**&#x200B;面板中单击&#x200B;**[!UICONTROL 下一步]**。

   在&#x200B;**[!UICONTROL 允许的子项]**&#x200B;面板中单击&#x200B;**[!UICONTROL 下一步]**。

   单击&#x200B;**[!UICONTROL 确定]**。

1. 单击“确定”并完成模板创建后，请注意新`playpage`模板的“属性”选项卡值的角上显示的红色三角形。 这些红色三角形表示尚未保存的编辑。

   单击&#x200B;**[!UICONTROL 全部保存]**&#x200B;以将新模板保存到存储库。

   ![verify-content-template](assets/verify-content-template.png)

### 创建模板的渲染组件 {#create-the-template-s-rendering-component}

创建&#x200B;*组件*&#x200B;以定义内容并呈现基于[播放页面模板](#createthepagetemplate)创建的任何页面。

1. 在CRXDE Lite中，右键单击&#x200B;**`/apps/an-scf-sandbox/components`**，然后单击&#x200B;**[!UICONTROL 创建>组件]**。
1. 通过将节点名称（标签）设置为&#x200B;*播放页面*，组件的路径为

   `/apps/an-scf-sandbox/components/playpage`

   （可选）减去路径的初始&#x200B;**`/apps/`**&#x200B;部分。

   在&#x200B;**[!UICONTROL 创建组件]**&#x200B;对话框中，键入以下属性值：

   * 标签： **播放页面**
   * 标题： **SCF沙盒播放组件**
   * 描述： **这是用于呈现SCF沙盒页面内容的组件。**
   * 超级类型： *&lt;留空>*
   * 组： *&lt;留空>*

   ![create-template-component](assets/create-template-component.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**，直到显示对话框的&#x200B;**[!UICONTROL 允许的子项]**&#x200B;面板：

   * 单击&#x200B;**[!UICONTROL 确定]**。
   * 单击&#x200B;**[!UICONTROL 全部保存]**。

1. 验证组件的路径与模板的resourceType是否匹配。

   >[!CAUTION]
   >
   >播放页面组件的路径与播放页面模板的`sling:resourceType`属性之间的对应关系对于网站的正确运行至关重要。

   ![verify-template-component](assets/verify-template-component.png)
