---
title: 将Forms渲染为HTML
seo-title: 将Forms渲染为HTML
description: 使用Forms服务将表单渲染为HTML，以响应来自Web浏览器的HTTP请求。 您可以使用Java API和Web服务API将表单渲染为HTML。
seo-description: 使用Forms服务将表单渲染为HTML，以响应来自Web浏览器的HTTP请求。 您可以使用Java API和Web服务API将表单渲染为HTML。
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4188'
ht-degree: 0%

---

# 将Forms渲染为HTML {#rendering-forms-as-html}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

Forms服务会响应来自Web浏览器的HTTP请求，将表单渲染为HTML。 将表单渲染为HTML的好处是客户端Web浏览器所在的计算机不需要Adobe Reader、Acrobat或Flash Player(对于表单指南（已弃用）)。

要将表单渲染为HTML，必须将表单设计另存为XDP文件。 另存为PDF文件的表单设计无法呈现为HTML。 在Designer中开发将呈现为HTML的表单设计时，请考虑以下条件：

* 请勿使用对象的边框属性在表单上绘制线条、框或网格。 某些浏览器可能无法像在预览中一样对边框进行排列。 对象可能显示为分层，也可能将其他对象推离其预期位置。
* 可以使用线条、矩形和圆来定义背景。
* 绘制的文本略大于容纳文本所需的文本。 某些Web浏览器无法清晰显示文本。

>[!NOTE]
>
>使用`FormServiceClient`对象的`(Deprecated) renderHTMLForm`和`renderHTMLForm2`方法渲染包含TIFF图像的表单时，在Internet Explorer或Mozilla Firefox浏览器中显示的已渲染HTML表单中，不显示TIFF图像。 这些浏览器不提供对TIFF图像的本机支持。

## HTML页面{#html-pages}

当表单设计呈现为HTML表单时，每个二级子表单都会呈现为HTML页面（面板）。 您可以在Designer中查看子表单的层次结构。 属于根子表单的子子表单（根子表单的默认名称为form1）是面板子表单。 以下示例显示表单设计的子表单。

```java
     form1
         Master Pages
         PanelSubform1
             NestedDynamicSubform
                 TextEdit1
         PanelSubform2
             TextEdit1
         PanelSubform3
             TextEdit1
         PanelSubform4
             TextEdit1
```

表单设计以HTML表单呈现时，面板不受任何特定页面大小的限制。 如果您有动态子表单，则应将它们嵌套在面板子表单中。 动态子表单可以扩展到无限数量的HTML页面。

表单呈现为HTML表单时，页面大小（将表单呈现为PDF时需要的页面大小）没有意义。 由于具有可流动布局的表单可以扩展到无限数量的HTML页面，因此避免出现主控页面上的页脚很重要。 主控页面上内容区域下方的页脚可能会覆盖流经页面边界的HTML内容。

必须使用`xfa.host.pageUp`和`xfa.host.pageDown`方法明确地从面板移动到面板。 您可以通过向Forms服务发送表单，并让Forms服务将表单渲染回客户端设备（通常是Web浏览器）来更改页面。

>[!NOTE]
>
>向Forms服务发送表单，然后让Forms服务将表单呈现回客户端设备的过程，称为向服务器发送往返数据。

>[!NOTE]
>
>如果要自定义HTML表单上HTML数字签名按钮的外观，则必须更改fscdigsig.css文件（在adobe-forms-ds.ear > adobe-forms-ds.war文件中）中的以下属性：

**.fsc-ds-ssb**:此样式表适用于空白符号字段的情况。

**.fsc-ds-ssv**:此样式表适用于“有效符号”字段。

**.fsc-ds-ssc**:此样式表适用于“有效符号”字段，但数据已更改的情况。

**.fsc-ds-ssi**:当符号字段无效时，此样式表适用。

**.fsc-ds-popup-bg**:不使用此样式表属性。

**.fsc-ds-popup-btn**:不使用此样式表属性。

## 运行脚本{#running-scripts}

表单作者指定脚本是在服务器还是客户端上执行。 Forms服务创建一个用于执行表单智能的分布式事件处理环境，该环境可以使用`runAt`属性在客户端和服务器之间分发。 有关此属性或在表单设计中创建脚本的信息，请参阅[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Forms服务可以在表单呈现时执行脚本。 因此，您可以通过连接到数据库或客户端上可能不可用的Web服务，来使用数据预填表单。 您还可以设置按钮的`Click`事件以在服务器上运行，以便客户端将数据往返到服务器。 这允许客户端在用户与表单交互时运行可能需要服务器资源（如企业数据库）的脚本。 对于HTML表单，只能在服务器上执行formcalc脚本。 因此，必须将这些脚本标记为在`server`或`both`运行。

您可以通过调用`xfa.host.pageUp`和`xfa.host.pageDown`方法来设计在页面（面板）之间移动的表单。 此脚本放置在按钮的`Click`事件中，并且`runAt`属性设置为`Both`。 您选择`Both`的原因是，Adobe Reader或Acrobat（对于呈现为PDF的表单）可以更改页面而不转到服务器，而HTML表单可以通过将数据往返到服务器来更改页面。 即，表单将发送到Forms服务，并且表单会以HTML形式呈现，并显示新页面。

建议您不要为脚本变量和表单字段指定与项目等相同的名称。 某些Web浏览器（如Internet Explorer）可能无法初始化与表单字段同名的变量，该变量会导致出现脚本错误。 最好为表单字段和脚本变量指定不同的名称。

在渲染同时包含页面导航功能和表单脚本的HTML表单时（例如，假设脚本每次渲染表单时都从数据库中检索字段数据），请确保表单脚本位于form:calculate event中，而不是form:readyevent中。

位于表单：ready事件中的表单脚本在表单的初始渲染期间仅执行一次，且不会为后续页面检索执行。 相反，会为呈现表单的每个页面导航执行表单：计算事件。

>[!NOTE]
在多页面表单上，如果您移动到其他页面，则JavaScript对页面所做的更改不会保留。

您可以在提交表单之前调用自定义脚本。 此功能适用于所有可用的浏览器。 但是，仅当用户呈现其`Output Type`属性设置为`Form Body`的HTML表单时，才能使用该属性。 当`Output Type`为`Full HTML`时，它将不起作用。 有关配置此功能的步骤，请参阅管理帮助中的配置表单。

必须先定义一个在提交表单之前调用的回调函数，其中该函数的名称为`_user_onsubmit`。 假定函数不会引发任何异常，或者如果引发了异常，则会忽略该异常。 建议将JavaScript函数放置在html的标题部分；但是，您可以在包含`xfasubset.js`的脚本标记结束前的任意位置声明它。

当formserver呈现包含下拉列表的XDP时，除了创建下拉列表之外，它还会创建两个隐藏的文本字段。 这些文本字段存储下拉列表的数据（一个存储选项的显示名称，而另一个存储选项的值）。 因此，每次用户提交表单时，都会提交下拉列表的整个数据。 假设您不想每次提交这么多数据，则可以编写一个自定义脚本来禁用该功能。 例如：下拉列表的名称为`drpOrderedByStateProv`，并将其封装在子表单标题下。 HTML输入元素的名称将为`header[0].drpOrderedByStateProv[0]`。 用于存储和提交下拉菜单数据的隐藏字段的名称具有以下名称：`header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

如果您不想发布数据，可以通过以下方式禁用这些输入元素。`var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```java
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```java
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## XFA子集{#xfa-subsets}

在创建要呈现为HTML的表单设计时，必须将脚本限制为JavaScript语言脚本的XFA子集。

在客户端上运行或在客户端和服务器上同时运行的脚本必须写入XFA子集中。 在服务器上运行的脚本可以使用完整的XFA脚本模型，也可以使用FormCalc。 有关使用JavaScript的信息，请参阅[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

在客户端上运行脚本时，只有当前显示的面板才能使用脚本；例如，当显示面板B时，您无法对面板A中的字段进行脚本编写。 在服务器上运行脚本时，可以访问所有面板。

在客户端上运行的脚本中使用脚本对象模型(SOM)表达式时，也必须谨慎。 在客户端上运行的脚本仅支持SOM表达式的简化子集。

## 事件时间{#event-timing}

XFA子集定义映射到HTML事件的XFA事件。 在计算和验证事件的时间上，行为略有不同。 在Web浏览器中，当您退出字段时，将执行完全计算事件。 当您更改字段值时，不会自动执行计算事件。 您可以通过调用`xfa.form.execCalculate`方法强制执行计算事件。

在Web浏览器中，仅当退出字段或提交表单时，才执行验证事件。 您可以使用`xfa.form.execValidate`方法强制执行验证事件。

Forms在Web浏览器中显示(与Adobe Reader或Acrobat相反)符合必填字段的XFA空测试（错误或警告）。

* 如果空测试生成错误，并且您在未指定值的情况下退出字段，则会显示一个消息框，并在单击“确定”后将您重新定位到该字段。
* 如果空测试生成警告，并且您在未指定值的情况下退出字段，则系统会提示您单击“确定”或“取消”，这样您就可以选择继续操作而不指定值，或者返回到字段以输入值。

有关空测试的更多信息，请参阅[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

## 表单按钮{#form-buttons}

单击提交按钮会将表单数据发送到Forms服务，并表示表单处理结束。 可以将`preSubmit`事件设置为在客户端或服务器上运行。 如果将`preSubmit`事件配置为在客户端上运行，则该事件会在表单提交之前运行。 否则，在表单提交期间，将在服务器上运行`preSubmit`事件。 有关`preSubmit`事件的更多信息，请参阅[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

如果按钮没有与其关联的客户端脚本，则数据会提交到服务器，在服务器上执行计算，并重新生成HTML表单。 如果按钮包含客户端脚本，则数据不会发送到服务器，并且客户端脚本会在Web浏览器中执行。

## HTML 4.0 Web浏览器{#html-4-0-web-browser}

仅支持HTML 4.0的Web浏览器不能支持XFA子集客户端脚本模型。 在创建表单设计以在HTML 4.0和MSDHTML或CSS2HTML中同时工作时，标记为在客户端运行的脚本将实际在服务器上运行。 例如，假设用户单击了位于HTML 4.0 Web浏览器中显示的表单上的按钮。 在这种情况下，表单数据会发送到执行客户端脚本的服务器。

建议将表单逻辑放置在计算事件中，该事件在HTML 4.0的服务器上运行，在MSDHTML或CSS2HTML的客户端上运行。

## 维护演示文稿更改{#maintaining-presentation-changes}

在HTML页面（面板）之间移动时，只会维护数据的状态。 不维护背景颜色或必填字段设置等设置（如果与初始设置不同）。 要维护显示状态，必须创建表示字段显示状态的字段（通常是隐藏的）。 如果向字段的`Calculate`事件中添加了一个脚本，该脚本会根据隐藏的字段值更改演示文稿，则当您在HTML页面（面板）之间来回移动时，将能够保留演示文稿状态。

以下脚本根据`hiddenField`的值维护字段的`fillColor`。 假设此脚本位于字段的`Calculate`事件中。

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
嵌套在表单元格内时，静态对象不会显示在渲染的HTML表单中。 例如，嵌套在表单元格内的圆形和矩形不会显示在渲染HTML表单中。 但是，当这些静态对象位于表外部时，这些静态对象会正确显示。

## 对HTML表单进行数字签名{#digitally-signing-html-forms}

如果HTML表单呈现为以下HTML转换之一，则无法对包含数字签名字段的HTML表单进行签名：

* AHTML
* HTML4
* 静态HTML
* NoScriptXHTML

有关对文档进行数字签名的信息，请参阅[数字签名和认证文档](/help/forms/developing/digitally-signing-certifying-documents.md)

## 呈现符合辅助功能准则的XHTML表单{#rendering-an-accessibility-guidelines-compliant-xhtml-form}

您可以渲染符合辅助功能准则的完整HTML表单。 即，表单呈现在完整HTML标记中，而不是呈现在body标记（不是完整的HTML页面）中的HTML表单。

## 验证表单数据{#validating-form-data}

建议在将表单渲染为HTML表单时限制对表单字段使用验证规则。 HTML表单可能不支持某些验证规则。 例如，当MM-DD-YYYY的验证模式应用于`Date/Time`字段（该字段位于以HTML形式呈现的表单设计中）时，即使输入了正确的日期，该模式也无法正常工作。 但是，此验证模式适用于以PDF呈现的表单。

>[!NOTE]
有关Forms服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤{#summary-of-steps}的摘要

要渲染HTML表单，请执行以下步骤：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 设置HTML运行时选项。
1. 渲染HTML表单。
1. 将表单数据流写入客户端Web浏览器。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

在以编程方式将数据导入PDF formClient API之前，您必须创建表单数据集成服务客户端。 在创建服务客户端时，您可以定义调用服务所需的连接设置。

**设置HTML运行时选项**

在渲染HTML表单时，可设置HTML运行时选项。 例如，您可以向HTML表单中添加工具栏，以允许用户选择位于客户端计算机上的文件附件，或检索使用HTML表单呈现的文件附件。 默认情况下，HTML工具栏处于禁用状态。 要向HTML表单添加工具栏，必须以编程方式设置运行时选项。 默认情况下，HTML工具栏包含以下按钮：

* `Home`:提供指向应用程序Web根目录的链接。
* `Upload`:提供用户界面以选择要附加到当前表单的文件。
* `Download`:提供用于显示附加文件的用户界面。

当HTML工具栏出现在HTML表单上时，用户最多可以选择十个要与表单数据一起提交的文件。 提交文件后，Forms服务便可以检索文件。

以HTML形式呈现表单时，可以指定用户代理值。 用户代理值提供浏览器和系统信息。 这是一个可选值，您可以传递空字符串值。 使用Java API渲染HTML表单快速入门演示了如何获取用户代理值并使用它将表单渲染为HTML。

将表单数据发布到的HTTP URL可以通过使用Forms服务客户端API设置目标URL来指定，也可以在XDP表单设计中包含的“提交”按钮中指定。 如果在表单设计中指定了目标URL，则不要使用Forms服务客户端API设置值。

>[!NOTE]
呈现带有工具栏的HTML表单是可选的。

>[!NOTE]
如果渲染AHTML表单，建议不要向表单添加工具栏。

**渲染HTML表单**

要渲染HTML表单，必须指定在Designer中创建并另存为XDP文件的表单设计。 还必须选择HTML转换类型。 例如，您可以指定为Internet Explorer 5.0或更高版本渲染动态HTML的HTML转换类型。

渲染HTML表单还需要值，例如渲染其他表单类型所需的URI值。

**将表单数据流写入客户端Web浏览器**

当Forms服务呈现HTML表单时，它会返回一个必须写入客户端Web浏览器的表单数据流。 写入客户端Web浏览器时，用户可以看到HTML表单。

**另请参阅**

[使用Java API将表单渲染为HTML](#render-a-form-as-html-using-the-java-api)

[使用Web服务API将表单渲染为HTML](#render-a-form-as-html-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入门](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈现交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[使用自定义工具栏渲染HTML Forms](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API {#render-a-form-as-html-using-the-java-api}将表单渲染为HTML

使用Forms API(Java)渲染HTML表单：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`FormsServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 设置HTML运行时选项

   * 使用`HTMLRenderSpec`对象的构造函数创建对象。
   * 要呈现带有工具栏的HTML表单，请调用`HTMLRenderSpec`对象的`setHTMLToolbar`方法并传递`HTMLToolbar`枚举值。 例如，要显示垂直HTML工具栏，请传递`HTMLToolbar.Vertical`。
   * 要设置HTML表单的区域设置值，请调用`HTMLRenderSpec`对象的`setLocale`方法，并传递指定区域设置值的字符串值。 （这是一个可选设置。）
   * 要在完整HTML标记中呈现HTML表单，请调用`HTMLRenderSpec`对象的`setOutputType`方法并传递`OutputType.FullHTMLTags`。 （这是一个可选设置。）

   >[!NOTE]
   当`StandAlone`选项为`true`且`ApplicationWebRoot`引用托管AEM Forms的J2EE应用程序服务器以外的服务器时，Forms无法在HTML中成功呈现（`ApplicationWebRoot`值使用传递到`FormsServiceClient`对象`(Deprecated) renderHTMLForm`方法的`URLSpec`对象指定）。 当`ApplicationWebRoot`是托管AEM Forms的另一台服务器时，管理控制台中Web根URI的值需要设置为表单的Web应用程序URI值。 可以通过以下方法完成此操作：登录到管理控制台，单击服务> Forms，并将Web根URI设置为https://server-name:port/FormServer 。 然后，保存您的设置。

1. 渲染HTML表单

   调用`FormsServiceClient`对象的`(Deprecated) renderHTMLForm`方法并传递以下值：

   * 指定表单设计名称（包括文件扩展名）的字符串值。 如果您引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定HTML首选项类型的`TransformTo`枚举值。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定`TransformTo.MSDHTML`。
   * `com.adobe.idp.Document`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递一个空的`com.adobe.idp.Document`对象。
   * 存储HTML运行时选项的`HTMLRenderSpec`对象。
   * 指定`HTTP_USER_AGENT`标头值的字符串值；例如，`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * `URLSpec`对象，用于存储呈现HTML表单所需的URI值。
   * 用于存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，可以指定`null`。

   `(Deprecated) renderHTMLForm`方法返回一个`FormsResult`对象，该对象包含可写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调用`FormsResult`对象“s `getOutputContent`”方法创建`com.adobe.idp.Document`对象。
   * 通过调用`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型来设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个`javax.servlet.ServletOutputStream`对象，用于将表单数据流写入客户端Web浏览器。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数传递，创建一个字节数组并用表单数据流填充该数组。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递到`write`方法。

**另请参阅**

[将Forms渲染为HTML](#rendering-forms-as-html)

[快速入门（SOAP模式）：使用Java API渲染HTML表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#render-a-form-as-html-using-the-web-service-api}将表单渲染为HTML

使用Forms API（Web服务）渲染HTML表单：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms客户端API对象

   创建`FormsService`对象并设置身份验证值。

1. 设置HTML运行时选项

   * 使用`HTMLRenderSpec`对象的构造函数创建对象。
   * 要呈现带有工具栏的HTML表单，请调用`HTMLRenderSpec`对象的`setHTMLToolbar`方法并传递`HTMLToolbar`枚举值。 例如，要显示垂直HTML工具栏，请传递`HTMLToolbar.Vertical`。
   * 要设置HTML表单的区域设置值，请调用`HTMLRenderSpec`对象的`setLocale`方法，并传递指定区域设置值的字符串值。 有关更多信息，请参阅[AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 要在完整HTML标记中呈现HTML表单，请调用`HTMLRenderSpec`对象的`setOutputType`方法并传递`OutputType.FullHTMLTags`。

   >[!NOTE]
   当`StandAlone`选项为`true`且`ApplicationWebRoot`引用托管AEM Forms的J2EE应用程序服务器以外的服务器时，Forms无法在HTML中成功呈现（`ApplicationWebRoot`值使用传递到`FormsServiceClient`对象`(Deprecated) renderHTMLForm`方法的`URLSpec`对象指定）。 当`ApplicationWebRoot`是托管AEM Forms的另一台服务器时，管理控制台中Web根URI的值需要设置为表单的Web应用程序URI值。 可以通过以下方法完成此操作：登录到管理控制台，单击服务> Forms，并将Web根URI设置为https://server-name:port/FormServer 。 然后，保存您的设置。

1. 渲染HTML表单

   调用`FormsService`对象的`(Deprecated) renderHTMLForm`方法并传递以下值：

   * 指定表单设计名称（包括文件扩展名）的字符串值。 如果您引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定HTML首选项类型的`TransformTo`枚举值。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定`TransformTo.MSDHTML`。
   * `BLOB`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递`null`。 (请参阅[使用可流动布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)。)
   * 存储HTML运行时选项的`HTMLRenderSpec`对象。
   * 指定`HTTP_USER_AGENT`标头值的字符串值；例如，`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。 如果不想设置此值，可以传递空字符串。
   * `URLSpec`对象，用于存储呈现HTML表单所需的URI值。 （请参阅[指定URI值](/help/forms/developing/rendering-interactive-pdf-forms.md)。）
   * 用于存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，可以指定`null`。 （请参阅[将文件附加到表单](/help/forms/developing/rendering-interactive-pdf-forms.md)。）
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 此参数值存储呈现的表单。
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 此参数将存储输出XML数据。
   * 由方法填充的空`javax.xml.rpc.holders.LongHolder`对象。 此参数将以表单存储页数。
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 此参数将存储区域设置值。
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 此参数将存储所用的HTML呈现值。
   * 将包含此操作结果的空`com.adobe.idp.services.holders.FormsResultHolder`对象。

   `(Deprecated) renderHTMLForm`方法使用必须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的`com.adobe.idp.services.holders.FormsResultHolder`对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过获取`com.adobe.idp.services.holders.FormsResultHolder`对象`value`数据成员的值，创建`FormResult`对象。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建包含表单数据的`BLOB`对象。
   * 通过调用`getContentType`方法获取`BLOB`对象的内容类型。
   * 通过调用`setContentType`方法并传递`BLOB`对象的内容类型来设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个`javax.servlet.ServletOutputStream`对象，用于将表单数据流写入客户端Web浏览器。
   * 创建一个字节数组，并通过调用`BLOB`对象的`getBinaryData`方法来填充该数组。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递到`write`方法。

**另请参阅**

[将Forms渲染为HTML](#rendering-forms-as-html)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
