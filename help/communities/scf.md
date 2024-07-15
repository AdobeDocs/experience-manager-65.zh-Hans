---
title: 社交组件框架
description: 社交组件框架(SCF)简化了配置、自定义和扩展社区组件的过程
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 0%

---

# 社交组件框架 {#social-component-framework}

社交组件框架(SCF)简化了服务器端和客户端上配置、自定义和扩展Communities组件的过程。

框架的好处包括：

* **功能性**：开箱即用的轻松集成，对80%的用例很少自定义或没有自定义。
* **Skinnable**：一致地使用CSS样式的HTML属性。
* **可扩展**：组件实现是面向对象的并且业务逻辑较轻 — 易于在服务器上添加增量业务登录。
* **灵活**：易于叠加和自定义的简单无逻辑JavaScript模板。
* **可访问**： HTTP API支持从任何客户端（包括移动应用程序）发布内容。
* **可移植**：集成/嵌入到基于任何技术构建的任何网页中。

使用交互式[社区组件指南](components-guide.md)浏览创作或发布实例。

## 概述 {#overview}

在SCF中，组件由SocialComponent POJO、Handlebars JS模板（用于呈现组件）和CSS（用于设置组件样式）组成。

Handlebars JS模板可以扩展模型/视图JS组件，以处理用户与客户端上的组件的交互。

如果组件必须支持数据修改，则可以编写SocialComponent API的实施以支持编辑/保存类似于传统Web应用程序中模型/数据对象的数据。 此外，可以添加操作（控制器）和操作服务来处理操作请求、执行业务逻辑以及调用模型/数据对象上的API。

可以扩展SocialComponent API以提供客户端对视图层或HTTP客户端所需的数据。

### 如何为客户端呈现页面 {#how-pages-are-rendered-for-client}

![scf-page-rendering](assets/scf-overview.png)

### 组件自定义和扩展 {#component-customization-and-extension}

要自定义或扩展组件，您只需将叠加和扩展写入/apps目录，这可以简化升级到未来版本的过程。

* 对于外观设计：
   * 仅[CSS需要编辑](client-customize.md#skinning-css)。
* 外观：
   * 更改JS模板和CSS。
* 对于Look、Feel和UX：
   * 更改JS模板、CSS和[扩展/覆盖JavaScript](client-customize.md#extending-javascript)。
* 要修改JS模板或GET端点可用的信息，请执行以下操作：
   * 扩展[SocialComponent](server-customize.md#socialcomponent-interface)。
* 要在操作期间添加自定义处理，请执行以下操作：
   * 编写[OperationExtension](server-customize.md#operationextension-class)。
* 要添加自定义操作，请执行以下操作：
   * 创建[Sling Post操作](server-customize.md#postoperation-class)。
   * 根据需要使用现有[OperationServices](server-customize.md#operationservice-class)。
   * 添加JavaScript代码以根据需要从客户端调用您的操作。

## 服务器端框架 {#server-side-framework}

该框架提供API来访问服务器上的功能，并支持客户端与服务器之间的交互。

### Java™ API {#java-apis}

Java™ API提供了易于继承或子类的抽象类和接口。

在[服务器端自定义](server-customize.md)页面上描述了主类。

访问[存储资源提供程序概述](srp.md)，了解有关使用UGC的信息。

### HTTP API {#http-api}

HTTP API支持对PhoneGap应用程序、本机应用程序以及其他集成和混合的客户端平台进行轻松自定义和选择。 此外，HTTP API允许社区站点作为服务运行，而无需客户端，这样框架组件可以集成到基于任何技术构建的任何网页中。

### HTTP API -GET请求 {#http-api-get-requests}

对于每个SocialComponent，该框架都提供一个基于HTTP的API端点。 通过向资源发送GET请求来访问端点，该资源具有“.social.json”选择器+扩展。 使用Sling将请求传递给`DefaultSocialGetServlet`。

**`DefaultSocialGetServlet`**

1. 将资源(resourceType)传递到`SocialComponentFactoryManager`并接收能够选择表示该资源的`SocialComponent`的SocialComponentFactory。

1. 调用工厂并接收能够处理资源和请求的`SocialComponent`。
1. 调用`SocialComponent`，它将处理请求并返回结果的JSON表示形式。
1. 向客户端返回JSON响应。

**`GET Request`**

默认的GETservlet监听.social.json请求，SocialComponent使用可自定义的JSON对这些请求进行响应。

![scf-framework](assets/scf-framework.png)

### HTTP API -POST请求 {#http-api-post-requests}

除了GET（读取）操作外，框架还定义端点模式以启用组件上的其他操作，包括创建、更新和删除。 这些端点是HTTP API，它们接受输入并使用HTTP状态代码或JSON响应对象进行响应。

此框架端点模式使得CUD操作具有可扩展、可重用和可测试性。

**`POST Request`**

每个SocialComponent操作都有一个SlingPOST：operation。 每个操作的业务逻辑和维护代码都封装在OperationService中，该服务可通过HTTP API或从其他位置作为OSGi服务访问。 提供了用于操作前/操作后支持可插拔操作扩展的挂接。

![scf-post-request](assets/scf-post-request.png)

### 存储资源提供程序(SRP) {#storage-resource-provider-srp}

要了解如何处理[社区内容存储](working-with-srp.md)中存储的UGC，请参阅：

* [存储资源提供程序概述](srp.md) — 简介和存储库使用情况概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP API实用工具方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md) — 编码准则。

### 服务器端自定义 {#server-side-customizations}

访问[服务器端自定义](server-customize.md)，了解有关自定义服务器端的Communities组件的业务逻辑和行为的信息。

## Handlebars JS模板语言 {#handlebars-js-templating-language}

新框架中比较值得注意的变化之一是使用`Handlebars JS` (HBS)模板语言，这是一种用于服务器 — 客户端渲染的常用开源技术。

HBS脚本简单、无逻辑，在服务器和客户端都可编译，易于叠加和自定义，并且可自然绑定到客户端UX，因为HBS支持客户端渲染。

框架提供了在开发SocialComponents时有用的多个[Handlebars帮助程序](handlebars-helpers.md)。

在服务器上，当Sling解析GET请求时，它会标识用于响应请求的脚本。 如果脚本是HBS模板(.hbs)，Sling会将请求委派给Handlebars引擎。 然后，Handlebars引擎将从相应的SocialComponentFactory获取SocialComponent，构建上下文并渲染HTML。

### 无访问限制 {#no-access-restriction}

Handlebars (HBS)模板文件(.hbs)类似于.jsp和.html模板文件，但它们可用于在客户端浏览器和服务器上渲染。 因此，请求客户端模板的客户端浏览器从服务器接收.hbs文件。

这要求Sling搜索路径中的所有HBS模板（/libs/或/apps下的任何.hbs文件）均可由任何用户从创作或发布中获取。

可能无法禁止对.hbs文件的HTTP访问。

### 添加或包含社区组件 {#add-or-include-a-communities-component}

大多数社区组件必须&#x200B;*添加*&#x200B;为Sling可寻址资源。 选定的几个Communities组件可能在模板中作为非现有资源&#x200B;*包含*，以允许动态包含和自定义写入用户生成内容(UGC)的位置。

在任一情况下，组件的[必需的客户端库](clientlibs.md)也必须存在。

**添加组件**

添加组件是指添加资源（组件）实例的过程，例如从组件浏览器(sidekick)拖动到创作编辑模式下的页面上的过程。

结果是par节点下的JCR子节点，该节点是Sling可寻址的。

**包含组件**

包含组件是指在模板中添加对[“不存在”资源](srp.md#for-non-existing-resources-ners)（无JCR节点）的引用的过程，例如使用脚本语言。

自Adobe Experience Manager (AEM) 6.1起，如果组件是动态包含而不是添加的，则可以在创作&#x200B;*设计*&#x200B;模式下编辑该组件的属性。

只能动态包含少量AEM Communities组件。 它们是：

* [评论](essentials-comments.md)
* [评分](rating-basics.md)
* [审核](reviews-basics.md)
* [投票](essentials-voting.md)

[社区组件指南](components-guide.md)允许将不可包含组件从添加更改为包含。

**使用Handlebars**&#x200B;模板语言时，使用[include帮助程序](handlebars-helpers.md#include)通过指定其resourceType来包含不存在的资源：

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**使用JSP**&#x200B;时，使用标记[cq：include](../../help/sites-developing/taglib.md#lt-cq-include)包含资源：

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>若要将组件动态添加到页面，而不是在模板中添加或包含该组件，请参阅[组件旁加载](sideloading.md)。

### Handlebars帮助程序 {#handlebars-helpers}

有关SCF中可用的自定义帮助程序的列表和说明，请参阅[SCF Handlebars帮助程序](handlebars-helpers.md)。

## 客户端框架 {#client-side-framework}

### 模型视图JavaScript框架 {#model-view-javascript-framework}

该框架包括[Backbone.js](https://backbonejs.org/)的扩展，这是一个模型视图JavaScript框架，用于促进开发丰富的交互式组件。 面向对象的性质支持可扩展/可重用的框架。 HTTP API简化了客户端和服务器之间的通信。

框架使用服务器端Handlebars模板来呈现客户端的组件。 这些模型基于HTTP API生成的JSON响应。 视图将自己绑定到Handlebars模板生成的HTML并提供交互性。

### CSS约定 {#css-conventions}

以下是定义和使用CSS类的推荐约定：

* 使用命名空间明确的CSS类选择器名称并避免使用通用名称，如“标题”和“图像”。
* 定义特定的类选择器样式，以便CSS样式表可以很好地与页面上的其他元素和样式配合使用。 例如：`.social-forum .topic-list .li { color: blue; }`
* 对于由JavaScript驱动的UX，将用于样式的CSS类与CSS类分开。

### 客户端自定义 {#client-side-customizations}

要自定义客户端上Communities组件的外观和行为，请参考[客户端自定义项](client-customize.md)，其中包含有关以下项的信息：

* [叠加](client-customize.md#overlays)
* [扩展名](client-customize.md#extensions)
* [HTML标记](client-customize.md#htmlmarkup)
* [为CSS设置外观](client-customize.md#skinning-css)
* [扩展JavaScript](client-customize.md#extending-javascript)
* [适用于SCF的Clientlibs](client-customize.md#clientlibs-for-scf)

## 功能和组件要点 {#feature-and-component-essentials}

[功能和组件要点](essentials.md)部分介绍了开发人员的基本信息。

可以在[编码准则](code-guide.md)部分中找到其他开发人员信息。

## 疑难解答 {#troubleshooting}

常见问题和已知问题在[疑难解答](troubleshooting.md)部分中进行了说明。
