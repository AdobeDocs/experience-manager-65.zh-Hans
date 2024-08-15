---
title: 为登陆页面扩展和配置设计导入程序
description: 了解如何为登陆页面配置设计导入程序。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 1b8c6075-13c6-4277-b726-8dea7991efec
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 0%

---

# 为登陆页面扩展和配置设计导入程序{#extending-and-configuring-the-design-importer-for-landing-pages}

本节介绍如何配置，并根据需要扩展登陆页面的设计导入程序。 导入后使用登陆页面包含在[登陆页面中。](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**使设计导入程序提取您的自定义组件**

以下是使设计导入程序识别您的自定义组件的逻辑步骤

1. 创建TagHandler

   * 标记处理程序是一个POJO，用于处理特定类型的HTML标记。 您的TagHandler可以处理的HTML标签的“种类”是通过TagHandlerFactory的OSGi属性“tagpattern.name”定义的。 此OSGi属性本质上是一个正则表达式，它应该匹配您要处理的输入html标记。 所有嵌套的标记将被抛到标记处理程序中以供处理。 例如，如果注册包含嵌套&lt;p>标记的div，&lt;p>标记也会被抛到TagHandler中，具体取决于您要如何进行处理。
   * 标记处理程序界面类似于SAX内容处理程序界面。 它会接收每个html标记的SAX事件。 作为标记处理程序提供程序，您需要实施某些生命周期方法，这些方法由设计导入程序框架自动调用。

1. 创建其对应的TagHandlerFactory。

   * 标记处理程序工厂是一个OSGi组件(singleton)，负责派生标记处理程序的实例。
   * 标记处理程序工厂必须公开名为“tagpattern.name”的OSGi属性，该属性的值与输入html标记匹配。
   * 如果有多个标记处理程序与输入的html标记匹配，则选择排名较高的处理程序。 排名本身作为OSGi属性&#x200B;**service.ranking**&#x200B;公开。
   * TagHandlerFactory是OSGi组件。 要提供给TagHandler的任何引用都必须通过此工厂进行。

1. 如果要覆盖默认值，请确保TagHandlerFactory的排名更好。

>[!CAUTION]
>
>AEM 6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features)已弃用用于导入登陆页面的设计导入程序[。

## 准备HTML以进行导入 {#preparing-the-html-for-import}

创建导入程序页面后，您可以导入完整的HTML登录页面。 要导入HTML登陆页面，您需要先将其内容压缩到设计包中。 设计包包含您的HTML登陆页面以及引用的资产（图像、css、图标、脚本等）。

下面的备忘单提供了一个示例，介绍如何准备HTML以进行导入：

登陆页备忘单

[获取文件](assets/cheatsheet.zip)

### Zip文件布局和要求 {#zip-file-layout-and-requirements}

>[!NOTE]
>
>此时，ZIP文件只能包含一个HTML页面或页面的一部分。

zip文件布局示例如下：

* /index.html >登陆页面HTML文件
* /css >以添加到CSS clientlib
* /img >所有图像和资产
* /js >以添加到JS clientlib中

布局基于HTML5样板最佳实践布局。 有关详细信息，请访问[https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>设计包&#x200B;**必须**&#x200B;至少包含根级别的&#x200B;**index.html**&#x200B;文件。 如果要导入的登陆页面也具有移动设备版本，则zip文件必须在根级别包含&#x200B;**mobile.index.html**&#x200B;以及&#x200B;**index.html**。

### 准备登录页面HTML {#preparing-the-landing-page-html}

为了能够导入HTML，您需要向登陆页面HTML添加画布div。

画布div是带有`id="cqcanvas"`的html **div**，必须插入到HTML`<body>`标记中，并且必须包含要进行转换的内容。

添加画布div后登陆页面HTML的示例片段如下所示：

```xml
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
  <meta name="description" content="">
</head>
<body>
 <div id="cqcanvas">
  <!-- HTML content intended for conversion -->
 </div>
</body>
</html>
```

### 准备HTML以包含可编辑的AEM组件 {#preparing-the-html-to-include-editable-aem-components}

导入登陆页面时，您可以选择按原样导入页面，这意味着在导入登陆页面后，您无法在AEM中编辑任何导入的项目(您仍然可以在页面上添加其他AEM组件)。

在导入登陆页面之前，您可能需要转换登陆页面的某些部分，以便它们是可编辑的AEM组件。 这样，即使用户在导入了登陆页面设计之后，也可以快速编辑登陆页面的各个部分。

要执行此操作，您需要将`data-cq-component`添加到所导入HTML文件中的相应组件。

以下部分将介绍如何编辑HTML文件，以便将登陆页面的某些部分转换为其他可编辑的AEM组件。 在[登陆页面组件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)中详细描述了组件。

>[!NOTE]
>
>用于将部分登录页转换为AEM组件的HTML标记同时具有长格式和简写标签声明。 对每个组件都进行了描述。

### 限制 {#limitations}

在导入之前，请注意以下限制：

### 不保留应用于&amp;amp；lt；body>标记的任何属性，如类或id {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

如果对body标记（例如`<body id="container">`）应用了id或类等任何属性，则在导入后不会保留该属性。 因此，要导入的设计不应与`<body>`标记上应用的属性有任何依赖关系。

### 拖放zip文件 {#drag-and-drop-zip}

Internet Explorer和Firefox 3.6及更早版本不支持拖放zip上传。 要在使用这些浏览器时上传设计，请单击放置文件区域以打开文件上传对话框，然后使用该对话框上传您的设计。

支持设计zip文件“拖放”的浏览器包括Chrome、Safari5.x、Firefox 4及更高版本。

### 不支持现代化程序 {#modernizr-is-not-supported}

`Modernizr.js`是一个基于JavaScript的工具，可检测浏览器的本机功能，并检测它们是否适用于html5元素。 设计使用Modernizer增强对不同浏览器的旧版本中的支持，可能会导致登陆页面解决方案中出现导入问题。 设计导入程序不支持`Modernizr.js`脚本。

### 导入设计包时未保留页面属性 {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

导入设计包之前，为页面（使用空白登陆页面模板）设置的任何页面属性（例如，自定义域、强制实施HTTPS等）在导入设计包后都将丢失。 因此，建议的做法是在导入设计包之后设置页面属性。

### 假定仅HTML标记 {#html-only-markup-assumed}

导入时，由于安全原因，将清理标记，以避免导入和发布无效的标记。 这假定仅HTML标记以及所有其他形式的元素(例如内联SVG或Web组件)将被过滤掉。

### 文本 {#text}

HTML标记可在设计包内的HTML中插入文本组件(`foundation/components/text`)：

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

在HTML中包含上述标记，会执行以下操作：

* 在导入设计包后创建的登陆页中创建一个可编辑的AEM文本组件(`sling:resourceType=foundation/components/text`)。
* 将已创建文本组件的`text`属性设置为`div`内包含的HTML。

**简写组件标记声明**：

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**包含列表的文本**

添加带有列表的文本：

* 第1
* 2nd

可以在RTE编辑器中编辑的内容：

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**带颜色的文本**

要添加可在RTE编辑器中编辑的带颜色（粉红色）的文本，请执行以下操作：

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### 标题 {#title}

HTML标记，在设计包的HTML中插入标题组件(`wcm/landingpage/components/title`)：

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

在HTML中包含上述标记，会执行以下操作：

* 在导入设计包后创建的登陆页中创建一个可编辑的AEM标题组件(`sling:resourceType=wcm/landingpage/components/title`)。
* 将创建的标题组件的`jcr:title`属性设置为封装在div中的标题标记中的文本。
* 将`type`属性设置为标题标记，在本例中为`h1`。

标题组件支持七种类型 — `h1, h2, h3, h4, h5, h6`和`default`。

**简写组件标记声明**：

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### 图像 {#image}

HTML标记，可在设计包内的HTML中插入图像组件(foundation/components/image)：

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

在HTML中包含上述标记，会执行以下操作：

* 在导入设计包后创建的登陆页面中创建可编辑的AEM图像组件(`sling:resourceType=foundation/components/image`)。
* 将已创建图像组件的`fileReference`属性设置为导入src属性中指定的图像的路径。
* 将`alt`属性设置为img标记中alt属性的值。
* 将`title`属性设置为img标记中title属性的值。
* 将`width`属性设置为img标记中width属性的值。
* 将`height`属性设置为img标记中height属性的值。

**简写组件标记声明：**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### 图像组件Div中不支持绝对URL img src {#absolute-url-img-src-not-supported-within-image-component-div}

如果尝试使用具有绝对URL src的`<img>`标记进行组件转换，则会引发相应的&#x200B;**UnsupportedTagContentException**。 例如，不支持以下内容：

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

否则，图像组件div之外的图像标记支持绝对URL图像。

### 行动号召组件 {#call-to-action-components}

您可以将导入的登陆页面部分标记为“可编辑的行动号召组件” — 在导入登陆页面后，可以编辑此类导入的行动号召组件。 AEM包含以下CTA组件：

* 点进链接 — 允许您添加文本链接，在单击该链接时，会将访客导向到目标URL。
* 图形链接 — 允许您添加图像，单击该图像可将访客转到目标URL。

#### 点进链接 {#click-through-link}

此CTA组件可用于在登陆页面上添加文本链接。

支持的属性

* 标签，带粗体、斜体和下划线选项
* 目标URL，支持第三方和AEM URL
* 页面渲染选项（同一窗口、新窗口等）

HTML标记，用于在导入的zip文件中包含点进组件。 此处href映射到目标URL，“查看产品详细信息”映射到标签，等等。

```xml
<div id="cqcanvas">
.
.
                <div data-cq-component="clickThroughLink">
        <a href="/content/we-retail/us/en/products/equipment/snow-sports/flying-snowboard.html">View Product Details  ></a>
  </div>
.
.
</div>
```

此组件可用于任何独立应用程序或从zip导入。

**简写组件标记声明**：

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### 图形链接 {#graphical-link}

此CTA组件可用于添加登陆页面上带有链接的任何图形图像。 图像可以是简单的按钮，也可以是作为背景的任何图形图像。 单击图像时，用户将被带入组件属性中指定的目标URL。 它是“行动号召”小组的一部分。

支持的属性

* 图像裁剪、旋转
* 悬停文本、说明、大小（以像素为单位）
* 目标URL，支持第三方和AEM URL
* 页面渲染选项（同一窗口、新窗口等）

HTML标记，以在导入的zip文件中包含图形链接组件。 此处href映射到目标url，img src是渲染图像，“title”作为悬停文本，依此类推。

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**简写组件标记声明**：

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>要创建点进图形链接，您需要将锚标记和图像标记包裹在具有`data-cq-component="clickthroughgraphicallink"`属性的div中。
>
>例如，`<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>不支持使用CSS将图像与锚标记关联的其他方法。 例如，以下标记不起作用：
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>具有关联的`css .hasbackground { background-image: pathtoimage }`
>

### 潜在客户表单 {#lead-form}

商机表单是用于收集访客/商机的配置文件信息的表单。 此信息可以存储并用于以后根据此信息执行有效的营销。 此信息通常包括标题、姓名、电子邮件、出生日期、地址、兴趣等。 它是“CTA潜在客户表单”组的一部分。

**支持的功能**

* 预定义的潜在客户字段 — 名字、姓氏、地址、dob、性别、关于、用户ID、电子邮件ID、提交按钮在Sidekick中可用。 只需将所需的组件拖放到潜在客户表单中。
* 借助这些组件，作者可以设计独立的潜在客户表单，这些字段对应于潜在客户表单字段。 在独立或导入的zip应用程序中，用户可以使用cq：form或cta潜在客户表单字段添加额外的字段和名称，并根据要求进行设计。
* 使用CTA潜在客户表单的特定预定义名称映射潜在客户表单字段，例如，潜在客户表单中的名字使用firstName等。
* 未映射到潜在客户表单的字段将映射到cq：form组件 — 文本、单选、复选框、下拉列表、隐藏、密码。
* 用户可以使用“label”标记提供标题，也可以使用样式属性“class”提供样式(仅适用于CTA潜在客户表单组件)。
* 感谢页面和订阅列表可作为表单的隐藏参数提供（显示在index.htm中），也可以从“潜在客户表单开始”的编辑栏添加/编辑

  &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

  &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* 可以通过编辑每个组件的配置来提供所需的约束，例如 — 。

HTML标记，以在导入的zip文件中包含图形链接组件。 此处“firstName”映射到潜在客户表单firstName，依此类推，但复选框除外 — 这两个复选框映射到cq：form下拉组件。

```xml
<div id="cqcanvas">
   <div id="form_wrapper">
    <h2>NEWSLETTER SIGN UP</h2>
       <div data-cq-component="leadFormGeneration">
       <form method="post" action="#" onsubmit="return popupBox()">
       <label for="firstName" class="checkText">
        FIRST NAME
       </label><br />
       <input name="firstName" class="text pink" type="text" /><br />
       <label for="lastName" class="checkText">
        LAST NAME
       </label><br />
       <input name="lastName" class="text pink" type="text" /><br />
       <label for="emailId" class="checkText">
        EMAIL ADDRESS
       </label><br />
       <input name="emailId" class="text pink" type="text" /><br />

       <div class="checkboxes">
       <input type="checkbox" class="check" name="send_news" /> <label for="send_news" class="checkText">Send me the latest We.Retail news and announcements.</label><br />
       <input type="checkbox" class="check" name="send_offers" /> <label for="send_offers" class="checkText">Send me We.Retail deals and special offers.</label><br />
       </div>
       <input type="submit" name="submit" class="submit pink" value="Sign Up >" />
       </form>
     </div>
   </div>
```

### Parsys {#parsys}

AEM Parsys组件是可以包含其他AEM组件的容器组件。 可以在导入的HTML中添加Parsys组件。 这允许用户向登陆页面添加/删除可编辑的AEM组件，即使是在已导入之后。

段落系统使用户能够使用Sidekick添加组件。

在设计包的HTML中插入Parsys组件(`foundation/components/parsys`)的HTML标记：

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

在HTML中包含上述标记会执行以下操作：

* 在导入设计包后创建的登陆页中插入AEM Parsys组件(foundation/components/parsys)。
* 使用默认组件初始化sidekick。 通过将组件从Sidekick拖到Parsys组件上，可以将新组件添加到登陆页面。
* 两个标题组件也是Parsys的一部分。

### 目标 {#target}

目标组件显示页面上某个体验的内容。 可以在营销活动中创建许多体验，并且目标组件可以动态地向访问页面的各种用户显示不同体验的内容。

用于插入Target组件并在营销活动中创建不同体验的HTML标记：

```xml
<div data-cq-component="target">
 <section data-cq-component="experience" data-cq-experience="default">
  <p data-cq-component="text">Default content. Select this campaign in client context to view other experiences</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="over-30">
  <p data-cq-component="text">Content for Over 30</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="under-30">
  <p data-cq-component="text">Content for Under 30</p>
 </section>
</div>
```

## 其他导入选项 {#additional-importing-options}

除了指定导入的组件是否为可编辑的AEM组件之外，您还可以在导入设计包之前配置以下内容：

* 通过提取在导入的HTML中定义的元数据来设置页面属性。
* 指定HTML中的charset编码。
* 覆盖导入程序页面模板。

### 通过提取导入的HTML中定义的元数据来设置页面属性 {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

设计导入程序应提取并保留在导入HTML的头中声明的以下元数据，作为属性“jcr：description”：

* &lt;meta name=&quot;description&quot; content=&quot;>

设计导入程序应提取并保留HTML标记中设置的Lang属性作为属性“jcr：language”

* &lt;html lang=&quot;en&quot;>

### 指定html中的charset编码 {#specifying-the-charset-encoding-in-the-html}

设计导入程序会读取在导入的HTML中指定的编码。 编码可按如下方式指定：

`<meta charset="UTF-8">`

*或*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

如果在导入的HTML中未指定编码，则设计导入程序设置的默认编码为UTF-8。

### 覆盖模板 {#overlaying-template}

通过在以下位置创建一个空白登陆页面模板，可以对该模板进行叠加： `/apps/<appName>/designimporter/templates/<templateName>`

在[模板](/help/sites-developing/templates.md)下说明了在AEM中创建模板的步骤。

### 从登陆页面引用组件 {#referring-a-component-from-landing-page}

假设您有一个组件，且您要使用data-cq-component属性在HTML中引用该组件，这样设计导入器就会在此处呈现一个组件include 。 例如，您要引用表组件(`resourceType = /libs/foundation/components/table`)。 需要在HTML中添加以下内容：

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

data-cq-component中的路径应为组件的resourceType。

### 最佳实践 {#best-practices}

对于在导入时标记为组件转换的元素，不建议使用类似于以下内容的CSS选择器。

| E > F | E元素的F元素子项 | [子组合器](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | F元素前面紧跟一个E元素 | [相邻的同级组合器](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | F元素，前面有E元素 | [常规同级组合器](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E：root | E元素，文档的根 | [构造伪类](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E：nth-child(n) | E元素，其父元素的第n个子元素 | [构造伪类](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E：nth-last-child(n) | E元素，其父项的第n个子项，从最后一个元素开始计数 | [构造伪类](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E：nth-of-type(n) | E元素，其类型的第n个同级 | [构造伪类](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E：nth-last-of-type(n) | E元素（其类型的第n个同级），从最后一个元素开始计数 | [构造伪类](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

这是因为其他html元素（如&lt;div>标记）在导入后会添加到生成的Html。

* 此外，对于标记为转换为AEM组件的元素，也不建议使用依赖上述结构的脚本。
* 不建议在标记标记上使用样式进行组件转换，如&lt;div data-cq-component=&quot;&amp;amp；ast；&quot;>。
* 设计布局应遵循HTML5样板中的最佳实践。 阅读更多内容：[https://html5boilerplate.com/](https://html5boilerplate.com/)。

## 配置OSGI模块 {#configuring-osgi-modules}

用于公开可通过OSGI控制台配置的属性的组件如下所示：

* 登陆页面设计导入程序
* 登陆页面生成器
* 移动设备登陆页面生成器
* 登陆页面条目预处理程序

下表简要描述了以下属性：

<table>
 <tbody>
  <tr>
   <td><strong>组件</strong></td>
   <td><strong>属性名称</strong></td>
   <td><strong>属性说明 </strong></td>
  </tr>
  <tr>
   <td>登陆页面设计导入程序</td>
   <td>提取筛选器</td>
   <td>用于从提取中筛选文件的正则表达式的列表。 从提取中排除与任何指定模式匹配的<br />个Zip条目</td>
  </tr>
  <tr>
   <td>登陆页面生成器</td>
   <td>文件模式</td>
   <td>登陆页面生成器可以配置为处理与由文件模式定义的正则表达式匹配的HTML文件。</td>
  </tr>
  <tr>
   <td>移动设备登陆页面生成器</td>
   <td>文件模式</td>
   <td>登陆页面生成器可以配置为处理与由文件模式定义的正则表达式匹配的HTML文件。</td>
  </tr>
  <tr>
   <td> </td>
   <td>设备组</td>
   <td>要支持的设备组的列表。</td>
  </tr>
  <tr>
   <td>登陆页面条目预处理程序</td>
   <td>搜索模式 </td>
   <td>存档条目内容中要搜索的模式。 此正则表达式与条目内容逐行匹配。 匹配后，匹配的文本将替换为指定的替换模式。<br /> <br />请参阅下面有关登陆页面条目预处理程序的当前限制的注释。</td>
  </tr>
  <tr>
   <td> </td>
   <td>替换图案</td>
   <td>替换找到的匹配项的模式。 您可以使用正则表达式组引用，如$1、$2。 此外，此模式支持在导入期间使用实际值解析的关键字，如{designPath}。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**登陆页面条目预处理程序的当前限制：**
>如果需要更改搜索模式，则打开felix属性编辑器时，需要手动添加反斜杠字符以转义正则表达式元字符。 如果不手动添加反斜杠字符，则正则表达式被视为无效，且不会替换旧正则表达式。
>
>例如，如果默认配置为
>
>>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>您需要将`CQ_DESIGN_PATH`替换为搜索模式中的`VIPURL`，则您的搜索模式应如下所示：
>
>`/\* *VIPURL *\*/ *(['"])`

## 疑难解答 {#troubleshooting}

在导入设计包时，您可能会遇到多个错误，如本节所述。

### 使用登陆页面相关组件初始化Sidekick {#initialization-of-sidekick-with-landing-page-relevant-components}

如果设计包包含Parsys组件标记，则在导入后，Sidekick将开始显示与登陆页面相关的组件。 您可以将新组件拖放到登陆页面中的Parsys组件上。 您还可以转到设计模式并将新组件添加到Sidekick。

### 导入期间显示的错误消息 {#error-messages-displayed-during-import}

如果有任何错误（例如，导入的包不是有效的zip文件），则设计导入不会导入包。 而是会在页面顶部拖放框的上方显示一条错误消息。 此处列出了错误情况的示例。 更正错误后，您可以将更新后的zip文件重新导入到同一个空白登陆页面上。 抛出错误的不同情况如下：

* 导入的设计包不是有效的zip存档。
* 导入的设计包在顶级不包含index.html。

### 导入后显示的警告 {#warnings-displayed-after-import}

如果出现任何警告(例如，HTML是指包中不存在的图像)，则设计导入程序会导入zip文件，但同时会在结果窗格中显示问题/警告列表，单击问题链接将显示警告列表，并指出设计包中的任何问题。 设计导入程序捕获并显示警告的不同情况如下：

* HTML是指包中不存在的图像。
* HTML是指包中不存在的脚本。
* HTML是指包中不存在的样式。

### ZIP文件的文件存储在AEM中的什么位置？ {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

导入登陆页面后，设计包中的文件（图像、css、js等）将存储在AEM的以下位置：

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

假设登陆页面是在营销活动`We.Retail`下创建的，且登陆页面的名称为&#x200B;**myBlankLandingPage**，则Zip文件的存储位置如下所示：

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### 未保留格式 {#formatting-not-preserved}

创建CSS时，请注意以下限制：

如果文本和（可编辑的）图像如下所示：

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

对`box`类应用了CSS，如下所示：

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

然后，在设计导入程序中使用`box img`，生成的登陆页面似乎未保留格式。 要解决此问题，AEM会在CSS中添加div标记，并相应地重写代码。 否则，某些CSS规则将无效。

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
>
>设计器应仅由导入器识别&#x200B;**id=cqcanvas**&#x200B;标记内的代码，否则不保留设计。
