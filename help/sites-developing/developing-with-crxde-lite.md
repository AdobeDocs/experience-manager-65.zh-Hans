---
title: 使用CRXDE Lite进行开发
description: CRXDE Lite会嵌入到Adobe Experience Manager (AEM)中，使您能够在该浏览器中执行标准开发任务
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '2114'
ht-degree: 1%

---

# 使用CRXDE Lite进行开发{#developing-with-crxde-lite}

本节介绍如何使用CRXDE Lite来开发Adobe Experience Manager (AEM)应用程序。

有关可用的不同开发环境的更多信息，请参阅概述文档。

CRXDE Lite会嵌入到AEM中，使您能够在该浏览器中执行标准开发任务。 使用CRXDE Lite，您可以在日志记录时创建项目、创建和编辑文件(如.jsp和.java)、文件夹、模板、组件、对话框、节点、属性和捆绑包。
当您无法直接访问AEM服务器时，建议进行CRXDE Lite。 或者，在通过扩展或修改现成组件和Java™捆绑包来开发应用程序时，或者在不需要专用调试器时，代码完成和语法突出显示。

>[!NOTE]
>
>从AEM 6.5.5.0开始，无法再匿名访问CRXDE Lite。
>用户将被重定向到登录屏幕。


>[!NOTE]
>
>Adobe建议您在项目开发期间使用[AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md)和[AEM HTL Brackets扩展](/help/sites-developing/aem-brackets.md)。

## CRXDE Lite快速入门 {#getting-started-with-crxde-lite}

要开始使用CRXDE Lite，请按照以下步骤操作：

1. 安装AEM。
1. 在浏览器中输入`https://<host>:<port>/crx/de`。 默认情况下，它为`https://localhost:4502/crx/de`。
1. 输入您的&#x200B;**用户名**&#x200B;和&#x200B;**密码**。 默认情况下，该值为`admin`和`admin`。

1. 单击&#x200B;**确定**。

CRXDE Lite用户界面在浏览器中如下所示：

![chlimage_1-18](assets/crx-interface.jpg)

您现在可以使用CRXDE Lite来开发应用程序。

## 用户界面概述 {#overview-of-the-user-interface}

CRXDE Lite提供以下功能：

<table>
 <tbody>
  <tr>
   <td>顶部切换器栏</td>
   <td>在CRXDE Lite、包管理器和包共享之间快速切换。</td>
  </tr>
  <tr>
   <td>节点路径小组件</td>
   <td><p>显示选定节点的路径。</p> <p>也可以使用它来跳转到节点，方法是手动输入路径，或从其他位置粘贴路径，然后点击Enter。</p> <p>它还支持查找具有特定节点名称的节点。 输入要查找并等待的节点的名称（或单击右侧的搜索符号）。 例如，您可以尝试在构件中输入字符串<em>oak</em>以查看其工作原理。 如果将给定的一个或多个节点加载到资源管理器窗格中，则会显示列表，您可以选择路径并按Enter以导航到它。 它仅适用于浏览器中加载到CRXDE客户端应用程序的节点。 如果要搜索整个存储库，请使用工具，然后使用查询。</p> </td>
  </tr>
  <tr>
   <td>资源管理器窗格</td>
   <td><p>显示存储库中所有节点的树。</p> <p>单击某个节点，以便在<strong>属性</strong>选项卡中显示其属性。 单击节点后，您可以在工具栏中选择操作。 再次单击该节点可对其进行重命名。</p> <p>树导航过滤器（双目图标）：用于过滤存储库中名称包含输入文本的节点。 它仅适用于已在本地加载的节点。<br /> </p> </td>
  </tr>
  <tr>
   <td>编辑窗格</td>
   <td><p><strong>主页</strong>选项卡：允许您搜索内容和/或文档并访问开发人员资源（文档、开发人员博客、知识库）和支持(Adobe主页和支持中心)。<br /> </p> <p>双击<strong>资源管理器</strong>窗格中的文件，以便显示其内容。 例如，.jsp或.java文件。 然后，您可以修改它并保存更改。</p> <p>在<strong>编辑</strong>窗格中编辑文件后，工具栏上有以下工具： <br /> </p> - <strong>在树中显示： </strong>在存储库树中显示文件。<br /> - <strong>搜索/替换……</strong>：执行搜索或替换。<br /> <br />双击<strong>编辑</strong>窗格的状态行打开<strong>转到行</strong>对话框，以便输入要转到的特定行号。<br /> </td>
  </tr>
  <tr>
   <td>“属性”选项卡<br /> </td>
   <td>显示所选节点的属性。 您可以添加新属性或删除现有属性。<br /> </td>
  </tr>
  <tr>
   <td>“访问控制”选项卡</td>
   <td><p>根据路径、存储库级别或主体显示权限。</p> <p>权限划分为</p> <p>- <strong>适用的访问控制策略</strong>：可以应用于选择的策略。</p> <p>- <strong>本地访问控制策略</strong>：策略已本地应用于选择。</p> <p>- <strong>有效的访问控制策略</strong>：应用于选择的策略可以本地设置，也可以从父节点继承。</p> <p>注意。 为了能够查看访问控制信息，登录到CRXDE Lite的用户必须对ACL条目具有读取权限。 匿名用户默认看不到此信息 — 例如，以管理员身份登录以查看此信息。</p> </td>
  </tr>
  <tr>
   <td>“复制”选项卡</td>
   <td><p>显示节点的复制状态。 您可以复制和删除节点。</p> </td>
  </tr>
  <tr>
   <td>控制台选项卡<br /> </td>
   <td><p><strong>服务器日志</strong>：</p> <p>显示日志消息。 您可以配置日志级别、清除控制台、固定到选定的滚动位置，以及启用或禁用消息的显示。<br /> </p> <p><strong>版本控制</strong>：</p> <p>显示版本控制消息。<br /> </p> </td>
  </tr>
  <tr>
   <td>“生成信息”选项卡<br /> </td>
   <td>在生成捆绑包时显示信息。<br /> </td>
  </tr>
  <tr>
   <td>刷新<br /> </td>
   <td>刷新所选内容。 来自其他用户的更改将在您对存储库的视图中更新。 您所做的更改不受影响。<br /> </td>
  </tr>
  <tr>
   <td>全部保存</td>
   <td><p><strong>全部保存</strong>：<br /> </p> <p>保存所做的所有更改。 在单击“保存”之前，更改是临时的，当您退出控制台时，这些更改将丢失。</p> <p><strong>还原</strong>：</p> <p>放弃自上次保存操作以来在选定节点上所做的所有更改，然后重新加载选定节点的存储库状态。</p> <p><strong>全部还原</strong>：</p> <p>放弃自上次保存操作以来对整个存储库所做的所有更改，然后重新加载存储库的状态。</p> </td>
  </tr>
  <tr>
   <td>创建……<br /> </td>
   <td><p>在所选节点下创建以下内容的下拉菜单：<br /> </p> <p>- <strong>节点</strong>：具有任意节点类型的节点<br /> </p> <p>- <strong>文件</strong>： nt：file节点及其nt：resource子节点</p> <p>- <strong>文件夹</strong>： nt：folder节点</p> <p>- <strong>模板</strong>： AEM模板</p> <p>- <strong>组件</strong>： AEM组件</p> <p>- <strong>对话框</strong>： AEM对话框</p> </td>
  </tr>
  <tr>
   <td>删除<br /> </td>
   <td>删除所选节点。<br /> </td>
  </tr>
  <tr>
   <td>复制</td>
   <td>复制所选节点。<br /> </td>
  </tr>
  <tr>
   <td>粘贴<br /> </td>
   <td>将复制的节点粘贴到所选节点下。<br /> </td>
  </tr>
  <tr>
   <td>移动……<br /> </td>
   <td>将所选节点移动到通过对话框设置的节点。</td>
  </tr>
  <tr>
   <td>重命名……<br /> </td>
   <td>重命名所选节点。<br /> </td>
  </tr>
  <tr>
   <td>Mixin ...<br /> </td>
   <td>用于向节点类型添加mixin类型。 mixin类型主要用于向节点添加高级功能，例如版本控制、访问控制、引用和锁定。</td>
  </tr>
  <tr>
   <td>工具<br /> </td>
   <td><p>下拉菜单及以下工具：</p> <p>- <strong>服务器配置……</strong>：用于访问Felix控制台。</p> <p>- <strong>查询……</strong>：查询存储库。</p> <p>- <strong>权限……</strong>：打开权限管理，您可以在其中查看和添加权限。</p> <p>- <strong>测试访问控制……</strong>：可在其中测试特定路径和/或主体的权限的位置。</p> <p>- <strong>导出节点类型</strong>：将系统中的节点类型导出为cnd表示法。</p> <p>- <strong>导入节点类型……</strong>：使用cnd表示法导入节点类型。</p> <p>- <strong>安装SiteCatalyst调试器……</strong>：有关如何安装Analytics调试器的说明。</p> </td>
  </tr>
  <tr>
   <td>登录小组件<br /> </td>
   <td><p>显示已登录的用户及其登录的工作区，例如admin@crx.default。</p> <p>单击以登录或以特定用户身份重新登录。 如果您没有指定要登录的工作区，则会登录到默认工作区crx.default。</p> <p>如果要以匿名用户身份浏览存储库，请使用<strong>匿名</strong>作为登录名，并使用任何密码（例如，空格或点）。<br /> </p> <p>如果您的授权不再有效（例如，已过期），则登录构件显示“<strong>未授权 — 登录……</strong>”。 单击以再次登录。</p> </td>
  </tr>
 </tbody>
</table>

## 创建文件夹 {#creating-a-folder}

要创建具有CRXDE Lite的文件夹，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，右键单击要在其下创建文件夹的文件夹，选择&#x200B;**创建……**，然后选择&#x200B;**创建文件夹……**。

1. 输入文件夹&#x200B;**名称**&#x200B;并单击&#x200B;**确定**。

1. 单击&#x200B;**全部保存**&#x200B;将更改保存在服务器上。

## 创建模板 {#creating-a-template}

要使用CRXDE Lite创建模板，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，右键单击要创建模板的文件夹，选择&#x200B;**创建……**，然后选择&#x200B;**创建模板……**。

1. 输入模板的&#x200B;**标签**、**标题**、**描述**、**资源类型**&#x200B;和&#x200B;**排名**。 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置&#x200B;**允许的路径**。 单击&#x200B;**下一步**

1. 此步骤是可选的：设置&#x200B;**允许的父项**。 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置&#x200B;**允许的子项**。 单击&#x200B;**确定**。

1. 单击&#x200B;**全部保存**&#x200B;将更改保存在服务器上。

它会创建：

* 具有模板属性的类型为`cq:Template`的节点

* 具有页面内容属性的类型为`cq:PageContent`的子节点

您可以将属性添加到模板：请参阅[创建属性](#creating-a-property)部分。

## 创建组件 {#creating-a-component}

此处介绍的功能仅在安装了CQ5时才可用，即节点类型`cq:Component`在存储库中可用。

要创建具有CRXDE Lite的组件，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，右键单击要在其中创建组件的文件夹，选择&#x200B;**创建……**，然后选择&#x200B;**创建组件……**。

1. 输入组件的&#x200B;**标签**、**标题**、**描述**、**超级资源类型**&#x200B;和&#x200B;**组**。 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置组件属性&#x200B;**Is Container、** **无修饰**、**单元格名称**&#x200B;和&#x200B;**对话框路径**。 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置组件属性&#x200B;**允许的父项**。 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置组件属性&#x200B;**Allowed Children**。 单击&#x200B;**确定**。

1. 单击&#x200B;**全部保存**&#x200B;将更改保存在服务器上。

它会创建：

* `cq:Component`类型的节点
* 组件属性
* 组件.jsp脚本

## 创建对话框 {#creating-a-dialog}

要创建带有CRXDE Lite的对话框，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，右键单击要创建对话框的组件，选择&#x200B;**创建……**，然后选择&#x200B;**创建对话框……**。

1. 输入&#x200B;**标签**&#x200B;和&#x200B;**标题**。 单击&#x200B;**确定**。

1. 单击&#x200B;**保存所有** l以保存服务器上的更改。

它创建一个具有以下结构的对话框：

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

您现在可以通过修改属性或创建节点来调整对话框以满足您的需求。

也可以使用对话框编辑器来编辑对话框。 双击CRXDE Lite中的对话框节点可打开编辑器。 有关详细信息，请参阅[对话框编辑器](/help/sites-developing/dialog-editor.md)。

## 创建节点 {#creating-a-node}

要创建具有CRXDE Lite的节点，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，右键单击要在其中创建节点的节点，选择&#x200B;**创建……**，然后选择&#x200B;**创建节点……**。
1. 输入&#x200B;**名称**&#x200B;和&#x200B;**类型**。 单击&#x200B;**确定**。
1. 单击&#x200B;**全部保存**&#x200B;将更改保存在服务器上。

您现在可以通过修改属性或创建节点来调整节点，以满足您的需求。

>[!NOTE]
>
>大多数编辑操作（包括“创建节点”）会将所有更改保存在内存中，并且仅在保存时将其存储在存储库中（通过“全部保存”按钮）。 但是，某些操作（如移动）会自动保留。
>
>在保存更改时，JCR存储库还会首先验证父节点的节点类型是否允许新创建的节点。 如果在保存节点时收到错误消息，请检查内容结构是否有效（例如，无法创建`nt:unstructured`节点作为`nt:folder`节点的子节点）。

## 创建资产 {#creating-a-property}

要创建具有CRXDE Lite的资产，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，选择要添加新属性的节点。
1. 在底部窗格的&#x200B;**属性**&#x200B;选项卡中，输入&#x200B;**名称**、**类型**&#x200B;和&#x200B;**值**。 单击&#x200B;**添加**。

1. 单击&#x200B;**全部保存**&#x200B;将更改保存在服务器上。

## 创建脚本 {#creating-a-script}

要创建脚本，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，右键单击要创建脚本的组件，选择&#x200B;**创建……**，然后选择&#x200B;**创建文件……**。

1. 输入文件&#x200B;**名称**，包括其扩展名。 单击&#x200B;**确定**。

1. 新文件将在“编辑”窗格中作为选项卡打开。
1. 编辑文件。
1. 单击&#x200B;**全部保存**&#x200B;以保存更改。

## 导出和导入节点类型 {#exporting-and-importing-node-types}

使用CRXDE Lite，您可以以[CND （压缩命名空间和节点类型定义）表示法](https://jackrabbit.apache.org/jcr/node-type-notation.html)导入和/或导出节点类型定义。

要导出节点类型定义，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 选择所需的节点。
1. 选择&#x200B;**工具**，然后选择&#x200B;**导出节点类型**。

1. 定义（用符号表示）显示在浏览器中。 保存信息（如有必要）。

要导入节点类型定义，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 选择&#x200B;**工具**，然后选择&#x200B;**导入节点类型……**。

1. 在文本框中输入定义的CND表示法。
1. 如果要更新现有定义，请选中&#x200B;**允许更新**。
1. 单击&#x200B;**导入**。

## 日志记录 {#logging}

通过CRXDE Lite，您可以显示文件系统上位于`<crx-install-dir>/crx-quickstart/server/logs`的文件`error.log`，并使用适当的日志级别对其进行筛选。 按照以下步骤操作：

1. 在浏览器中打开CRXDE Lite。
1. 在窗口底部的&#x200B;**控制台**&#x200B;选项卡中，从右侧的下拉菜单中选择&#x200B;**服务器日志**。

1. 单击&#x200B;**停止**&#x200B;图标以显示消息。

您可以：

* 通过单击&#x200B;**日志记录配置**&#x200B;图标，调整Felix控制台中的日志参数。
* 通过单击&#x200B;**画笔**&#x200B;图标清除消息。
* 通过单击&#x200B;**固定**&#x200B;图标，将邮件固定到选定位置。
* 通过单击&#x200B;**停止**&#x200B;图标启用或禁用消息的显示。

## 访问控制 {#access-control}

>[!NOTE]
>
>有关详细信息，请参阅[用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md)。
