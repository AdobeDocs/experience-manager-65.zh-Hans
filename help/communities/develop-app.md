---
title: 开发沙盒应用程序
description: 了解如何开发一个沙盒应用程序，该应用程序使用基础脚本，并能够通过Communities组件启用创作。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 4%

---

# 开发沙盒应用程序  {#develop-sandbox-application}

在此部分中，现在，模板在[初始应用程序](initial-app.md)部分中设置，初始页面在[初始内容](initial-content.md)部分中建立，您可以开发应用程序。 为此，您需要使用基础脚本，这些脚本包含启用通过社区组件进行创作的功能。 在此部分末尾，您有一个功能齐全的网站。

## 使用基础页脚本 {#using-foundation-page-scripts}

默认脚本是在添加了呈现播放页模板的组件时创建的，该脚本经过修改后包括基础页的head.jsp和本地body.jsp。

### 超级资源类型 {#super-resource-type}

第一步是向`/apps/an-scf-sandbox/components/playpage`节点添加一个资源超级类型属性，以便它继承该超级类型的脚本和属性。

使用CRXDE Lite：

1. 选择节点`/apps/an-scf-sandbox/components/playpage`。
1. 在属性选项卡中，输入具有以下值的新属性：

   名称：`sling:resourceSuperType`

   类型：`String`

   值： `foundation/components/page`

1. 单击绿色&#x200B;**[!UICONTROL +添加]**&#x200B;按钮。
1. 单击&#x200B;**[!UICONTROL 全部保存]**。

   ![page-script](assets/page-script.png)

### Head和body脚本 {#head-and-body-scripts}

1. 在&#x200B;**CRXDE Lite**&#x200B;资源管理器窗格中，导航到`/apps/an-scf-sandbox/components/playpage`并双击文件`playpage.jsp`以在编辑窗格中将其打开。

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
     An SCF Sandbox Play Component component.
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
    // TODO add your code here
   %>
   ```

1. 意识到打开/关闭脚本标记，将“ // TODO ...”替换为&lt;html>的head和body部分的`includes`个脚本。

   使用`foundation/components/page`的超类型，未在此同一文件夹中定义的任何脚本都将解析为`/apps/foundation/components/page`文件夹中的脚本（如果存在），否则解析为`/libs/foundation/components/page`文件夹中的脚本。

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: playpage.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <html>
     <cq:include script="head.jsp"/>
     <cq:include script="body.jsp"/>
   </html>
   ```

1. 不必覆盖基础脚本`head.jsp`，但基础脚本`body.jsp`为空。

   要设置进行创作，请使用本地脚本叠加`body.jsp`，并在正文中包含段落系统(parsys)：

   1. 导航到 `/apps/an-scf-sandbox/components`。
   1. 选择`playpage`节点。
   1. 右键单击并选择`Create > Create File...`

      * 名称： **body.jsp**

   1. 单击&#x200B;**[!UICONTROL 全部保存]**。

   打开`/apps/an-scf-sandbox/components/playpage/body.jsp`并粘贴以下文本：

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: body.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <body>
       <h2>Community Play</h2>
       <cq:include path="par" resourceType="foundation/components/parsys" />
   </body>
   ```

1. 单击&#x200B;**[!UICONTROL 全部保存]**。

**在浏览器中以编辑模式查看页面：**

* 标准UI： `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

您应该不仅看到标题&#x200B;**社区播放**，而且还看到用于编辑页面内容的UI。

当两侧面板均切换打开并且窗口足够宽以便显示侧内容和页面内容时，会看到Assets/组件侧面板。

![查看页面](assets/view-page.png)

* 经典UI： `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

以下是“播放”页面在经典UI中的显示方式，包括使用content finder (cf)：

![播放页面查看](assets/play-page-view.png)

## Communities组件 {#communities-components}

要启用社区组件进行创作，请按照以下说明开始操作：

* [访问社区组件](basics.md#accessing-communities-components)

对于此沙盒，从这些&#x200B;**Communities**&#x200B;组件开始（通过选中该框启用）：

* 评论
* 论坛
* 评分
* 审核
* 审核摘要（显示）
* 投票

此外，选择&#x200B;**[!UICONTROL 常规]**&#x200B;组件，例如

* 图像
* 表
* 文本
* 标题（基础）

>[!NOTE]
>
>为页面par启用的组件作为`components`属性的值存储在存储库中。
>
>节点`/etc/designs/an-scf-sandbox/jcr:content/playpage/par`。

## 登录页面 {#landing-page}

在多语言环境中，根页面将包含一个脚本，该脚本将解析来自客户端的请求以确定首选语言。

在此示例中，将根页面静态设置为重定向到英语页面，该页面将来可能会发展为带有播放页面链接的主登陆页面。

将浏览器URL更改为根页面： `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* 选择页面信息图标
* 选择&#x200B;**[!UICONTROL 打开属性]**
* 在高级选项卡上

   * 对于重定向条目，请浏览到&#x200B;**[!UICONTROL 网站]** > **[!UICONTROL SCF沙盒站点]** > **[!UICONTROL SCF沙盒]**
   * 单击&#x200B;**[!UICONTROL 确定]**

* 单击&#x200B;**[!UICONTROL 确定]**

发布站点后，在发布实例上浏览到根页面时，会重定向到英文页面。

播放Communities SCF组件之前的最后一步是添加客户端库文件夹(clientlibs) .... [添加Clientlibs](add-clientlibs.md)
