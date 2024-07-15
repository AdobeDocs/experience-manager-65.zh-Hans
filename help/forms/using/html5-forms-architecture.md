---
title: HTML5表单的架构
description: HTML5表单作为包部署在嵌入式AEM实例中，并使用RESTful Apache Sling架构通过HTTP/S公开作为REST端点的功能。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: ed8349a1-f761-483f-9186-bf435899df7d
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1976'
ht-degree: 0%

---

# HTML5表单的架构{#architecture-of-html-forms}

## 架构 {#architecture}

HTML5表单功能作为包部署在嵌入式AEM实例中，并使用RESTful [Apache Sling架构](https://sling.apache.org/)通过HTTP/S公开为REST端点。

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### 使用Sling框架 {#using-sling-framework}

[Apache Sling](https://sling.apache.org/)以资源为中心。 它会使用请求URL首先解析资源。 每个资源都有一个&#x200B;**sling：resourceType**（或&#x200B;**sling：resourceSuperType**）属性。 然后，根据此属性、请求方法和请求URL的属性，选择sling脚本来处理请求。 此sling脚本可以是JSP或servlet。 对于HTML5表单，**配置文件**&#x200B;节点用作Sling资源，**配置文件渲染器**&#x200B;用作Sling脚本，用于处理使用特定配置文件渲染移动表单的请求。 **配置文件渲染器**&#x200B;是一个JSP，它从请求中读取参数并调用Forms OSGi服务。

有关REST端点和支持的请求参数的详细信息，请参阅[渲染表单模板](/help/forms/using/rendering-form-template.md)。

当用户从客户端设备(如iOS或Android™浏览器)发出请求时，Sling首先根据请求URL解析配置文件节点。 从该配置文件节点中，读取&#x200B;**sling：resourceSuperType**&#x200B;和&#x200B;**sling：resourceType**&#x200B;以确定可处理此表单渲染请求的所有可用脚本。 然后，它使用Sling请求选择器以及请求方法来识别最适合处理此请求的脚本。 请求到达配置文件渲染器JSP后，JSP会调用Forms OSGi服务。

有关Sling脚本解析的更多详细信息，请参阅[AEM Sling备忘单](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans)或[Apache Sling Url分解](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html)。

#### 典型的表单处理调用流程 {#typical-form-processing-call-flow}

HTML5表单缓存处理（呈现或提交）第一个请求中的表单所需的所有中间对象。 它不会缓存依赖于数据的对象，因为此类对象可能会发生更改。

Mobile Form维护两个不同的缓存级别：PreRender缓存和渲染缓存。 preRender缓存包含已解析模板的所有片段和图像，而渲染缓存包含HTML等渲染的内容。

![HTML5表单工作流](assets/cacheworkflow.png)

HTML5表单工作流

HTML5表单不会缓存缺少片段和图像引用的模板。 如果HTML5表单花费的时间超过正常时间，请检查服务器日志中是否有缺少的引用和警告。 同时确保未达到对象的最大大小。

Forms OSGi服务分两步处理请求：

* **布局和初始表单状态生成**： Forms OSGi渲染服务调用Forms缓存组件以确定表单是否已缓存且尚未失效。 如果表单已缓存且有效，则会从缓存中提供生成的HTML。 如果表单失效，Forms OSGi渲染服务会以XML格式生成初始表单布局和表单状态。 此XML由Forms OSGi服务转换为HTML布局和初始JSON表单状态，然后缓存以供后续请求使用。
* **预填充的Forms**：在渲染时，如果用户请求带有预填充数据的表单，则Forms OSGi渲染服务将调用Forms服务容器，并生成带有合并数据的新表单状态。 但是，由于布局已在上述步骤中生成，因此此调用比第一次调用更快。 此调用仅执行数据合并，并对数据运行脚本。

如果表单中有任何更新，或者表单内使用了任何资产，则表单缓存组件会检测到该更新，并且特定表单的缓存将失效。 Forms OSGi服务完成处理后，配置文件渲染器jsp会将JavaScript库引用和样式添加到此表单，并将响应返回到客户端。 此处可以使用诸如[Apache](https://httpd.apache.org/)之类的典型Web服务器并启用HTML压缩。 Web服务器将显着降低响应大小、网络流量以及在服务器和客户端计算机之间流式传输数据所需的时间。

当用户提交表单时，浏览器将表单的状态以JSON格式发送到[提交服务代理](../../forms/using/service-proxy.md)；然后提交服务代理使用JSON数据生成数据XML并提交该数据XML以提交端点。

## 组件 {#components}

您需要AEM Forms附加组件包才能启用HTML5表单。 有关安装AEM Forms附加组件包的信息，请参阅[安装和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。

### OSGi组件(adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**AdobeXFA Forms呈现器(com.adobe.livecycle.adobe-lc-forms-core)**&#x200B;是从Felix Admin Console (https://[host]：[port]/system/console/bundles)的捆绑包视图查看时，HTML5 forms OSGi捆绑包的显示名称。

此组件包含用于渲染、缓存管理和配置设置的OSGi组件。

#### Forms OSGi服务 {#forms-osgi-service}

此OSGi服务包含将XDP呈现为HTML的逻辑，并处理表单提交以生成数据XML。 此服务使用Forms服务容器。 Forms服务容器在内部调用执行处理的本机组件`XMLFormService.exe`。

如果收到渲染请求，此组件将调用Forms服务容器以生成布局和状态信息，这些信息将得到进一步处理以生成HTML和JSON表单DOM状态。

此组件还负责从提交的表单状态JSON生成数据XML。

#### 缓存组件 {#cache-component}

HTML5表单使用缓存来优化吞吐量和响应时间。 您可以配置缓存服务的级别，以优化性能和空间利用率之间的平衡。

<table>
 <tbody>
  <tr>
   <th>缓存策略</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>无</td>
   <td>不缓存项目<br /> </td>
  </tr>
  <tr>
   <td>保守</td>
   <td>仅缓存在表单（如包含内联片段和图像的模板）渲染之前生成的中间工件</td>
  </tr>
  <tr>
   <td>激进</td>
   <td>缓存渲染的HTML内容<br />缓存在保守级别缓存的所有项目。<br /> <strong>注意</strong>：此策略可产生最佳性能，但会消耗更多内存来存储缓存的项目。</td>
  </tr>
 </tbody>
</table>

HTML5表单使用LRU策略执行内存缓存。 如果缓存策略设置为“无”，将不会创建缓存并清除现有缓存数据（如果有）。 除了高速缓存策略之外，您还可以配置内存中的高速缓存总大小，这有助于使高速缓存大小达到最大界限，如果超过此界限，它将使用LRU模式释放高速缓存资源。

>[!NOTE]
>
>内存缓存不会在群集节点之间共享。

#### 配置服务 {#configuration-service}

配置服务允许调整HTML5表单的配置参数和缓存设置。

要更新这些设置，请转到CQ FelixAdmin Console(位于https://&lt;&#39;[server]：[port]&#39;/system/console/configMgr)，搜索并选择Mobile Forms配置。

可以使用配置服务配置高速缓存大小或禁用高速缓存。 您还可以使用“调试选项”参数启用调试。 有关调试表单的详细信息，可在[调试HTML5表单](/help/forms/using/debug.md)中找到。

### 运行时组件(adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

运行时包包含用于呈现HTML表单的客户端库。

**作为运行时包的一部分提供的重要组件：**

#### 脚本引擎 {#scripting-engine}

AdobeXFA实施支持两种脚本语言，以便在表单中启用用户定义的逻辑执行：JavaScript和FormCalc。

HTMLForms的脚本引擎是在JavaScript中编写的，用于支持使用这两种语言的XFA脚本API。

在渲染时，FormCalc脚本在服务器上转换（和缓存）到JavaScript中，对用户或设计者透明。

此脚本引擎使用ECMAScript5的某些功能，如Object.defineProperty。 引擎/库作为类别名称为&#x200B;**xfaforms.profile**&#x200B;的CQ客户端库提供。 它还提供&#x200B;**FormBridge API**&#x200B;以启用外部门户或应用程序与表单交互。 使用FormBridge，外部应用程序能够以编程方式隐藏某些元素、获取或设置其值或更改其属性。

有关更多详细信息，请参阅[表单Bridge](/help/forms/using/form-bridge-apis.md)一文。

#### 布局引擎 {#layout-engine}

HTML5表单的布局和可视化方面基于SVG1.1、jQuery、BackBone和CSS3功能。 生成表单的初始外观并将其缓存在服务器上。 该初始布局的调整以及对表单布局所做的任何进一步增量更改都在客户端中进行管理。 为实现此目的，运行时包包含使用JavaScript编写并基于jQuery/Backbone的布局引擎。 此引擎处理所有动态行为，如添加/删除可重复实例、可增长对象布局。 此布局引擎每次呈现一个表单页面。 最初，用户仅查看一个页面，而水平滚动条仅计入第一页。 但是，当用户向下滚动时，下一页开始渲染。 这种逐页呈现形式减少了在浏览器中呈现第一页所需的时间并增强了表单的感知性能。 此引擎/库是类别名称为&#x200B;**xfaforms.profile**&#x200B;的CQ客户端库的一部分。

布局引擎还包含一组用于从用户处捕获表单字段值的小组件。 这些小组件被建模为[jQuery UI小组件](https://api.jqueryui.com/jQuery.widget/)，这些小组件实现特定的附加合同以便与布局引擎无缝配合工作。

有关构件和相应合约的更多详细信息，请参阅[HTML5表单的自定义构件](/help/forms/using/introduction-widgets.md)。

#### 样式 {#styling}

与HTML元素关联的样式会内联添加或基于嵌入的CSS块添加。 某些不依赖于表单的常见样式包含在具有类别名称xfaforms.profile的CQ客户端库中。

除了默认样式属性外，每个表单元素还包含基于元素类型、名称和其他属性的特定CSS类。 使用这些类，可以通过指定元素自己的CSS来重新设置元素的样式。

有关默认样式和类的更多详细信息，请参阅[样式简介](/help/forms/using/css-styles.md)。

#### 服务器端脚本和Web服务 {#server-side-script-and-web-services}

任何标记为在服务器上运行或标记为调用Web服务的脚本（无论将其标记为执行的位置如何）始终在服务器上执行。

客户端脚本引擎：

1. 以JSON形式同步调用传递当前表单状态的服务器
1. 在服务器上执行脚本或Web服务
1. 生成新的JSON状态
1. 在返回响应时合并客户端上的新JSON状态。

#### 本地化资源包 {#localization-resource-bundles}

HTML5表单支持意大利语(it)、西班牙语(es)、巴西葡萄牙语(pt_BR)、简体中文(zh_CN)、繁体中文（仅限有限支持）(zh_TW)、朝鲜语(ko_KR)、英语(en_US)、法语(fr_FR)、德语(de_DE)和日语(ja)语言。 根据在请求标头中收到的区域设置，相应的资源包将发送到客户端。 此资源包作为类别名称为&#x200B;**xfaforms.I18N**&#x200B;的CQ客户端库添加到配置文件JSP中。 您可以覆盖在配置文件中选取区域设置包的逻辑。

### Sling组件(adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Sling包包含与配置文件和配置文件渲染器相关的内容。

#### 配置文件 {#profiles}

配置文件是sling中表示表单或Forms系列的资源节点。 在CQ级别，这些配置文件是JCR节点。 这些节点位于JCR存储库中的&#x200B;**/content**&#x200B;文件夹下，并且可以位于&#x200B;**/content**&#x200B;文件夹下的任何子文件夹中。

#### 配置文件渲染器 {#profile-renderers}

配置文件节点具有属性&#x200B;**sling：resourceSuperType**，其值为&#x200B;**xfaforms/profile**。 此属性在内部将请求转发到&#x200B;**/libs/xfaforms/profile**&#x200B;文件夹中配置文件节点的sling脚本。 这些脚本是JSP页，是HTML表单和所需JS/CSS工件的容器。 这些页面包括对以下内容的引用：

* **xfaforms.I18N。&lt;locale>**：此库包含本地化数据。
* **xfaforms.profile**：此库包含XFA脚本和布局引擎的实施。

这些库被建模为CQ客户端库，这些库利用CQ框架JavaScript库的自动连接、缩小和压缩功能。
有关CQ客户端库的详细信息，请参阅[CQ Clientlib文档](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans)。

如上所述，配置文件渲染器JSP通过sling include调用Forms服务。 此JSP还根据管理员配置或请求参数设置各种调试选项。

HTML5表单允许开发人员创建配置文件和配置文件渲染器以自定义表单的外观。 例如，利用HTML表单，开发人员可以将表单集成到现有HTML门户的面板或&lt;div>部分中。
有关创建自定义配置文件的更多详细信息，请参阅[创建自定义配置文件](/help/forms/using/custom-profile.md)。
