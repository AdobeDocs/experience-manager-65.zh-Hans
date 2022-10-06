---
title: 开发沙盒应用程序
seo-title: Develop Sandbox Application
description: 使用基础脚本开发应用程序
seo-description: Develop application using foundation scripts
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 5%

---

# 开发沙盒应用程序  {#develop-sandbox-application}

在本节中，由于模板已在 [初始应用](initial-app.md) ，以及 [初始内容](initial-content.md) 部分，可以使用基础脚本来开发应用程序，其中包括启用使用社区组件进行创作的功能。 在本节的末尾，网站将正常运行。

## 使用Foundation页面脚本 {#using-foundation-page-scripts}

默认脚本（在添加呈现播放页模板的组件时创建）将被修改以包含基础页的head.jsp和本地body.jsp。

### 超级资源类型 {#super-resource-type}

第一步是向 `/apps/an-scf-sandbox/components/playpage` 节点，以便继承超类型的脚本和属性。

使用 CRXDE Lite:

1. 选择节点 `/apps/an-scf-sandbox/components/playpage`.
1. 在“属性”选项卡中，输入具有以下值的新属性：

   名称: `sling:resourceSuperType`

   类型: `String`

   值: `foundation/components/page`

1. 单击绿色 **[!UICONTROL +添加]** 按钮。
1. 单击 **[!UICONTROL 全部保存]**.

   ![page-script](assets/page-script.png)

### 头部和身体脚本 {#head-and-body-scripts}

1. 在 **CRXDE Lite** 浏览器窗格，导航到 `/apps/an-scf-sandbox/components/playpage` 并双击该文件 `playpage.jsp` ，以在编辑窗格中将其打开。

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

1. 请注意打开/关闭脚本标记，请替换“ // TODO ...” 包含用于 &lt;html>.

   超级类型的 `foundation/components/page`，该文件夹中未定义的任何脚本都将解析为 `/apps/foundation/components/page` 文件夹（如果存在）， `/libs/foundation/components/page` 文件夹。

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

1. 基础脚本 `head.jsp` 不需要覆盖，但基础脚本 `body.jsp` 为空。

   要设置以进行创作，请叠加 `body.jsp` ，并在正文中包含段落系统(parsys):

   1. 导航到 `/apps/an-scf-sandbox/components`。
   1. 选择 `playpage` 节点。
   1. 右键单击并选择 `Create > Create File...`

      * 名称： **body.jsp**
   1. 单击 **[!UICONTROL 全部保存]**.

   打开 `/apps/an-scf-sandbox/components/playpage/body.jsp` 并粘贴以下文本：

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

1. 单击 **[!UICONTROL 全部保存]**.

**在编辑模式下在浏览器中查看页面：**

* 标准 UI: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

您不应仅看到标题 **社区游戏**，还有用于编辑页面内容的UI。

当两个侧面板都切换为打开，并且窗口足够宽以便同时显示侧内容和页面内容时，会看到资产/组件侧面板。

![查看页面](assets/view-page.png)

* 经典 UI: `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

以下是播放页面在经典UI中的显示方式，包括内容查找器(cf):

![play-page-view](assets/play-page-view.png)

## 社区组件 {#communities-components}

要启用社区组件进行创作，请首先按照以下说明操作：

* [访问社区组件](basics.md#accessing-communities-components)

出于此沙盒的目的，请首先 **社区** 组件（通过选中框启用）：

* 评论
* 论坛
* 评级
* 审核
* 审核摘要（显示）
* 投票

此外，选择 **[!UICONTROL 常规]** 组件，例如

* 图像
* 表
* 文本
* 标题 (Foundation)

>[!NOTE]
>
>为页面段落启用的组件作为 `components` 属性
>
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` 节点。

## 登录页面 {#landing-page}

在多语言环境中，根页面将包含一个脚本，该脚本将解析来自客户端的请求以确定首选语言。

在这个简单的示例中，正在静态设置根页面以重定向到英语页面，该页面将来可能会开发为包含播放页面链接的主登陆页面。

将浏览器URL更改为根页面： `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* 选择页面信息图标
* 选择 **[!UICONTROL 打开属性]**
* 在“高级”选项卡上

   * 对于重定向条目，请浏览至 **[!UICONTROL 网站]** > **[!UICONTROL SCF沙盒站点]** > **[!UICONTROL SCF沙盒]**
   * 单击 **[!UICONTROL 确定]**

* 单击 **[!UICONTROL 确定]**

网站发布后，浏览到发布实例上的根页面将重定向到英文页面。

播放社区SCF组件之前的最后一步是添加客户端库文件夹(clientlibs)。... [添加Clienlibs](add-clientlibs.md)
