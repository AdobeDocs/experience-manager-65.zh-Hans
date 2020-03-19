---
title: 开发沙箱应用程序
seo-title: 开发沙箱应用程序
description: 使用基础脚本开发应用程序
seo-description: 使用基础脚本开发应用程序
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# 开发沙箱应用程序 {#develop-sandbox-application}

在本节中，既然模板已在初始应用程序部分中设置 [](initial-app.md)[](initial-content.md) ，而初始内容部分中创建的初始页面，则可以使用基础脚本开发应用程序，包括使用Communities组件进行创作的能力。 在本节结尾，网站将可正常运行。

## 使用基础页面脚本 {#using-foundation-page-scripts}

在添加呈现播放页模板的组件时创建的默认脚本将被修改以包括基础页面的head.jsp和本地body.jsp。

### 超级资源类型 {#super-resource-type}

第一步是向节点添加资源super type属性， `/apps/an-scf-sandbox/components/playpage` 以便它继承super类型的脚本和属性。

使用CRXDE Lite:

<!--Resolve steps below-->
    名称：`sling:resourceSuperType&#39;
    Type:“字符串”
    值：`foundation/components/page&#39;

1. 单击绿色 **[!UICONTROL [+添加]]**
1. 单击“ **[!UICONTROL 全部保存”]**

![chlimage_1-231](assets/chlimage_1-231.png)

### 头部和身体脚本 {#head-and-body-scripts}

1. 在 **CRXDE Lite** explorer窗格中，导览至文件， `/apps/an-scf-sandbox/components/playpage` 然后双击该文件以在编 `playpage.jsp` 辑窗格中将其打开。

#### /apps/an-scf-sandbox/components/playpage/playpage.jsp {#apps-an-scf-sandbox-components-playpage-playpage-jsp}

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

1. 要注意打开／关闭脚本标记，请替换“ // TODO ...” 包含用于&lt;html>的头部和正文部分的脚本。

   如果超类型为 `foundation/components/page`，则此文件夹中未定义的任何脚本将解析为文件夹中的脚本（如果存在），否则解析为文件夹中的脚 `/apps/foundation/components/page``/libs/foundation/components/page` 本。

#### /apps/an-scf-sandbox/components/playpage/playpage.jsp {#apps-an-scf-sandbox-components-playpage-playpage-jsp-1}

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

   要设置创作，请使用本 `body.jsp` 地脚本叠加并在正文中包含段落系统(parsys):

   1. 导航至 `/apps/an-scf-sandbox/components`
   1. 选择节 `playpage`点
   1. 右键单击并选择 `Create > Create File...`

      * 名称： **body.jsp**
   1. 单击“ **[!UICONTROL 全部保存”]**
   在以 `/apps/an-scf-sandbox/components/playpage/body.jsp` 下文本中打开并粘贴：

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

1. 单击“ **[!UICONTROL 全部保存”]**

**在编辑模式下在浏览器中查看页面：**

* 标准UI: [http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html](http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.md)

您不仅应看到“社区播 **放”标题**，还应看到用于编辑页面内容的UI。

当同时打开侧面板且窗口足够宽以便同时显示侧内容和页面内容时，会看到“资源／组件”侧面板。

![chlimage_1-232](assets/chlimage_1-232.png)

* 经典UI: [http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html](http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html)

以下是播放页面在经典UI中的显示方式，包括内容查找器(cf):

![chlimage_1-233](assets/chlimage_1-233.png)

## 社区组件 {#communities-components}

要启用Communities组件进行创作，请首先按照以下说明操作：

* [访问社区组件](basics.md#accessing-communities-components)

为便于此沙箱，请从以下 **Communities** 组件开始（通过选中该框启用）:

* 评论
* 论坛
* 评级
* 审核
* 审核摘要（显示）
* 投票

此外，选择“ **[!UICONTROL 常规]** ”组件，如

* 图像
* 表
* 文本
* 标题（基础）

>[!NOTE]
>
>为页面par启用的组件作为 `components`
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` 节点。

## 登录页面 {#landing-page}

在多语言环境中，根页面将包括一个脚本，该脚本将解析来自客户端的请求以确定首选语言。

在这个简单的示例中，将根页面静态设置为重定向到英语页面，该页面将来可能会开发为主登录页面，并带有指向播放页面的链接。

将浏览器URL更改为根页面： [http://localhost:4502/editor.html/content/an-scf-sandbox.html](https://locahost:4502/editor.html/content/an-scf-sandbox.html)

* 选择页面信息图标
* 选择 **[!UICONTROL 打开属性]**
* 在“高级”选项卡上

   * 对于重定向条目，请浏览到“网 **[!UICONTROL 站”>“SCF沙箱站点”>“SCF沙箱”]**
   * Click **[!UICONTROL OK]**

* Click **[!UICONTROL OK]**

发布站点后，浏览到发布实例上的根页面将重定向到英文页面。

播放社区SCF组件之前的最后一步是添加客户端库文件夹(clientlibs)。... [添加Clinelbs](add-clientlibs.md)