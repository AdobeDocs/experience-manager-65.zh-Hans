---
title: 将表单渲染为HTML
seo-title: 将表单渲染为HTML
description: 'null'
seo-description: 'null'
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
translation-type: tm+mt
source-git-commit: 9f3129aff8a3e389231b0fe0973794e5d34480a0

---


# 将表单渲染为HTML {#rendering-forms-as-html}

Forms服务将表单渲染为HTML以响应来自Web浏览器的HTTP请求。 将表单渲染为HTML的好处是客户端Web浏览器所在的计算机不需要Adobe Reader、Acrobat或Flash Player(用于表单指南（已弃用）)。

要将表单渲染为HTML，必须将表单设计另存为XDP文件。 保存为PDF文件的表单设计无法呈现为HTML。 在设计器中开发将呈现为HTML的表单设计时，请考虑以下条件：

* 请勿使用对象的边框属性在表单上绘制线条、框或网格。 某些浏览器可能无法像预览中那样排列边框。 对象可能显示为分层，也可能将其他对象推离其预期位置。
* 可以使用线条、矩形和圆形定义背景。
* 绘制的文本略大于容纳文本所需的文本。 某些Web浏览器无法清晰显示文本。

>[!NOTE]
>
>当使用对象和方法渲染包含TIFF图 `FormServiceClient` 像的表单时， `(Deprecated) renderHTMLForm``renderHTMLForm2` 在Internet explorer或Mozilla Firefox浏览器中显示的渲染后的HTML表单中不显示TIFF图像。 这些浏览器不提供对TIFF图像的本机支持。

## HTML页面 {#html-pages}

当表单设计呈现为HTML表单时，每个二级子表单都呈现为HTML页面（面板）。 您可以在Designer中查看子表单的层次结构。 属于根子表单的子子表单（根子表单的默认名称是form1）是面板子表单。 以下示例展示了表单设计的子表单。

```as3
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

当表单设计呈现为HTML表单时，面板不会限制为任何特定页面大小。 如果您有动态子表单，则它们应嵌套在面板子表单中。 动态子表单能够扩展到无限数量的HTML页面。

当表单呈现为HTML表单时，页面大小（将表单呈现为PDF时需要）毫无意义。 由于具有可流动布局的表单可以扩展到无限数量的HTML页面，因此避免主页上的页脚很重要。 主页上内容区域下方的页脚可覆盖流经页面边界的HTML内容。

必须使用和方法在面板之间显式 `xfa.host.pageUp` 移动 `xfa.host.pageDown` 面板。 您可以通过向Forms服务发送表单并让Forms服务将表单渲染回客户端设备（通常是Web浏览器）来更改页面。

>[!NOTE]
>
>将表单发送到Forms服务，然后让Forms服务将表单呈现回客户端设备的过程称为向服务器发送往返数据。

>[!NOTE]
>
>如果要自定义HTML表单上“HTML数字签名”按钮的外观，则必须更改fscdigsig.css文件（在adobe-forms-ds.ear > adobe-forms-ds.war文件中）中的以下属性：

**.fsc-ds-ssb**:此样式表适用于空白符号字段的情况。

**.fsc-ds-ssv**:此样式表适用于有效符号字段的情况。

**.fsc-ds-ssc**:此样式表适用于有效符号字段但数据已更改的情况。

**.fsc-ds-ssi**:此样式表适用于签名字段无效的情况。

**.fsc-ds-popup-bg**:不使用此样式表属性。

**.fsc-ds-popup-btn**:不使用此样式表属性。

## 运行脚本 {#running-scripts}

表单作者指定脚本是在服务器上还是在客户端上执行。 Forms服务创建用于执行表单智能的分布式事件处理环境，该表单智能可以通过使用属性在客户端和服务器之间分 `runAt` 发。 有关此属性或在表单设计中创建脚本的信息，请参阅 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

在呈现表单时，Forms服务可以执行脚本。 因此，您可以通过连接到数据库或客户端上可能不可用的Web服务，用数据预填充表单。 您还可以设置一个按钮事 `Click` 件以在服务器上运行，以便客户端将数据往返到服务器。 这允许客户端在用户与表单交互时运行可能需要服务器资源（如企业数据库）的脚本。 对于HTML表单，只能在服务器上执行表单计算脚本。 因此，您必须标记这些脚本才能在或 `server` 运行 `both`。

您可以通过调用和方法设计在页面（面板）之间移动 `xfa.host.pageUp` 的表 `xfa.host.pageDown` 单。 此脚本被放置在按钮的事 `Click` 件中，并且 `runAt` 属性设置为 `Both`。 您选择的原因 `Both` 是，Adobe Reader或Acrobat（对于呈现为PDF的表单）可以更改页面而不转到服务器，而HTML表单可以通过往返将数据转到服务器来更改页面。 即，表单将发送到表单服务，并且表单将呈现为HTML并显示新页面。

建议不要为脚本变量和表单字段提供与项目等名称相同的名称。 某些Web浏览器（如Internet Explorer）可能无法初始化与表单字段同名的变量，这会导致脚本错误。 最好为表单字段和脚本变量指定不同的名称。

在呈现同时包含页面导航功能和表单脚本的HTML表单时（例如，假设每次呈现表单时脚本都从数据库检索字段数据），请确保表单脚本位于form:calculate事件中，而不是form:readyevent中。

位于form:ready事件中的表单脚本在表单的初始渲染期间仅执行一次，而不会对后续页面检索执行。 相反，对于呈现表单的每个页面导航，将执行表单：计算事件。

>[!NOTE]
在多页表单上，如果移到其他页面，则JavaScript对页面所做的更改不会保留。

您可以在提交表单之前调用自定义脚本。 此功能适用于所有可用的浏览器。 但是，仅当用户呈现其属性设置为的HTML表单时，才 `Output Type` 能使用它 `Form Body`。 当是时，它将不起 `Output Type` 作用 `Full HTML`。 有关配置此功能的步骤，请参阅管理帮助中的配置表单。

必须首先定义在提交表单之前调用的回调函数，其中函数的名称为 `_user_onsubmit`。 假定该函数不会引发任何异常，或如果它引发异常，则将忽略该异常。 建议将JavaScript函数放在html的head部分；但是，您可以在包含脚本标签的末尾之前的任何地方声明它 `xfasubset.js`。

当formserver呈现包含下拉列表的XDP时，除了创建下拉列表外，它还会创建两个隐藏的文本字段。 这些文本字段存储下拉列表的数据（一个存储选项的显示名称，另一个存储选项的值）。 因此，每次用户提交表单时，都会提交下拉列表的整个数据。 如果您不希望每次提交这么多数据，您可以编写自定义脚本来禁用它。 例如：下拉列表的名称为， `drpOrderedByStateProv` 并且包含在子表单标题下。 HTML输入元素的名称将为 `header[0].drpOrderedByStateProv[0]`。 存储和提交下拉列表数据的隐藏字段的名称具有以下名称： `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

如果不希望发布数据，可以通过以下方式禁用这些输入元素。 `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```as3
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```as3
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## XFA子集 {#xfa-subsets}

创建表单设计以呈现为HTML时，必须将脚本限制为javascript语言脚本的XFA子集。

在客户端上运行或同时在客户端和服务器上运行的脚本必须写入XFA子集中。 在服务器上运行的脚本可以使用完整的XFA脚本模型，也可以使用FormCalc。 有关使用JavaScript的信息，请参阅 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

在客户端运行脚本时，只有当前显示的面板才能使用脚本；例如，当显示面板B时，您无法针对位于面板A中的字段编写脚本。 在服务器上运行脚本时，可以访问所有面板。

在客户端上运行的脚本中使用脚本对象模型(SOM)表达式时，您还必须小心。 客户端上运行的脚本只支持简化的SOM表达式子集。

## 事件计时 {#event-timing}

XFA子集定义映射到HTML事件的XFA事件。 在计算和验证事件的定时上，行为略有不同。 在Web浏览器中，当您退出字段时，将执行一个完全计算事件。 当您对字段值进行更改时，不会自动执行计算事件。 可以通过调用方法强制执行计算事 `xfa.form.execCalculate` 件。

在Web浏览器中，仅当退出字段或提交表单时，才执行验证事件。 可以使用方法强制执行validate事 `xfa.form.execValidate` 件。

在Web浏览器中显示的表单（与Adobe reader或Acrobat相对）符合必填字段的XFA空值测试（错误或警告）。

* 如果空测试生成错误，而您退出字段而没有指定值，则会显示一个消息框，单击“确定”后，您将重新定位到该字段。
* 如果空测试生成警告，而您退出字段时未指定值，则系统会提示您单击“确定”或“取消”，这样您就可以选择继续操作而不指定值，或者返回字段以输入值。

有关空测试的详细信息，请参阅 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

## 表单按钮 {#form-buttons}

单击提交按钮会将表单数据发送到Forms服务并表示表单处理结束。 该 `preSubmit` 事件可以设置为在客户端或服务器上运行。 如果 `preSubmit` 将事件配置为在客户端运行，则该事件会在表单提交之前运行。 否则，在 `preSubmit` 提交表单期间，该事件在服务器上运行。 有关活动的详细信 `preSubmit` 息，请参 [阅Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

如果按钮没有与其关联的客户端脚本，则数据会提交到服务器，计算会在服务器上执行，并重新生成HTML表单。 如果按钮包含客户端脚本，则数据不会发送到服务器，客户端脚本在Web浏览器中执行。

## HTML 4.0 web浏览器 {#html-4-0-web-browser}

仅支持HTML 4.0的Web浏览器不支持XFA子集客户端脚本模型。 创建表单设计以在HTML 4.0和MSDHTML或CSS2HTML中工作时，标记为在客户端运行的脚本将实际在服务器上运行。 例如，假定用户单击位于HTML 4.0 web浏览器中显示的表单上的按钮。 在这种情况下，表单数据将发送到执行客户端脚本的服务器。

建议将表单逻辑放在计算事件中，这些事件在HTML 4.0中的服务器上运行，在MSDHTML或CSS2HTML的客户端上运行。

## 维护演示文稿更改 {#maintaining-presentation-changes}

在HTML页面（面板）之间移动时，只保留数据的状态。 不保留背景颜色或必填字段设置等设置（如果不同于初始设置）。 要保持演示文稿状态，必须创建表示字段演示文稿状态的字段（通常为隐藏字段）。 如果向某个字段的事件中添加了一个脚本，该脚本会根据隐藏字段值更改演示文稿，则在HTML页面（面板）之间来回移动时，您可以保留演示文稿状态。 `Calculate`

以下脚本根据 `fillColor` 的值维护字段的值 `hiddenField`。 假定此脚本位于字段的事 `Calculate` 件中。

```as3
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
当对象嵌套在表单元格中时，静态对象不会显示在呈现的HTML表单中。 例如，嵌套在表单元格中的圆和矩形不会显示在渲染HTML表单中。 但是，当这些相同的静态对象位于表之外时，它们会正确显示。

## 对HTML表单进行数字签名 {#digitally-signing-html-forms}

如果表单呈现为以下HTML转换之一，则无法对包含数字签名字段的HTML表单进行签名：

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

有关对文档进行数字签名的信息，请参 [阅对文档进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md)

## 渲染符合辅助功能准则的XHTML表单 {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

您可以渲染符合辅助功能准则的完整HTML表单。 也就是说，表单在完整的HTML标记中呈现，而HTML表单在正文标记（不是完整的HTML页面）中呈现。

## 验证表单数据 {#validating-form-data}

建议在将表单呈现为HTML表单时限制对表单字段的验证规则的使用。 HTML表单可能不支持某些验证规则。 例如，当MM-DD-YYYY的验证模式应用于表单设计中作为HTML表单呈现的字段时，即使日期输入正确，该模式也无法正常工作。 `Date/Time` 但是，此验证模式适用于以PDF形式呈现的表单。

>[!NOTE]
有关Forms服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤摘要 {#summary-of-steps}

要渲染HTML表单，请执行以下步骤：

1. 包括项目文件。
1. 创建Forms Client API对象。
1. 设置HTML运行时选项。
1. 渲染HTML表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Forms Client API对象**

在以编程方式将数据导入PDF formClient API之前，必须创建Form Data Integration服务客户端。 创建服务客户端时，您定义调用服务所需的连接设置。

**设置HTML运行时选项**

在渲染HTML表单时，可设置HTML运行时选项。 例如，可以向HTML表单添加一个工具栏，使用户能够选择位于客户端计算机上的文件附件或检索使用HTML表单呈现的文件附件。 默认情况下，HTML工具栏处于禁用状态。 要向HTML表单添加工具栏，必须以编程方式设置运行时选项。 默认情况下，HTML工具栏由以下按钮组成：

* `Home`:提供指向应用程序Web根目录的链接。
* `Upload`:提供一个用户界面，用于选择要附加到当前表单的文件。
* `Download`:提供用于显示附加文件的用户界面。

当HTML表单上显示HTML工具栏时，用户最多可以选择要提交的十个文件以及表单数据。 提交文件后，Forms服务可以检索文件。

在将表单呈现为HTML时，可以指定用户代理值。 用户代理值提供浏览器和系统信息。 这是一个可选值，您可以传递空字符串值。 使用Java API快速入门渲染HTML表单演示如何获取用户代理值并使用它将表单渲染为HTML。

可以使用Forms Service Client API设置目标URL来指定发布表单数据的HTTP URL，也可以在XDP表单设计中包含的“提交”按钮中指定。 如果在表单设计中指定了目标URL，则不要使用Forms Service Client API设置值。

>[!NOTE]
使用工具栏渲染HTML表单是可选的。

>[!NOTE]
如果您渲染AHTML表单，建议不要向表单添加工具栏。

**渲染HTML表单**

要渲染HTML表单，必须指定在Designer中创建并另存为XDP文件的表单设计。 还必须选择HTML转换类型。 例如，可指定用于为Internet Explorer 5.0或更高版本渲染动态HTML的HTML转换类型。

渲染HTML表单还需要值，如渲染其他表单类型所需的URI值。

**将表单数据流写入客户端Web浏览器**

当Forms服务呈现HTML表单时，它会返回一个表单数据流，您必须将该数据流写入客户端Web浏览器。 当写入客户端Web浏览器时，用户可看到HTML表单。

**另请参阅**

[使用Java API将表单渲染为HTML](#render-a-form-as-html-using-the-java-api)

[使用Web服务API将表单渲染为HTML](#render-a-form-as-html-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入门](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF表单](/help/forms/developing/rendering-interactive-pdf-forms.md)

[使用自定义工具栏渲染HTML表单](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[创建呈现表单的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API将表单渲染为HTML {#render-a-form-as-html-using-the-java-api}

使用Forms API(Java)渲染HTML表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms Client API对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `FormsServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 设置HTML运行时选项

   * 使用对 `HTMLRenderSpec` 象的构造函数创建对象。
   * 要使用工具栏渲染HTML表单，请调 `HTMLRenderSpec` 用对象的方 `setHTMLToolbar` 法并传递枚 `HTMLToolbar` 举值。 例如，要显示垂直HTML工具栏，请传递 `HTMLToolbar.Vertical`。
   * 要设置HTML表单的区域设置值，请调用对 `HTMLRenderSpec` 象的方法并 `setLocale` 传递一个指定区域设置值的字符串值。 （这是一个可选设置。）
   * 要在完整的HTML标签中呈现HTML表单，请调 `HTMLRenderSpec` 用对象的方 `setOutputType` 法并传递 `OutputType.FullHTMLTags`。 （这是一个可选设置。）
   >[!NOTE]
   当选项为并引用承载AEM Forms的J2EE应用程序服务器以外的服务器( `StandAlone` 该值是使用传递给对象方法的对象 `true` 指定的)时，表 `ApplicationWebRoot` 单在HTML中不 `ApplicationWebRoot``URLSpec``FormsServiceClient``(Deprecated) renderHTMLForm` 会成功呈现。 如果是 `ApplicationWebRoot` 承载AEM表单的另一台服务器，则需要将管理控制台中的Web根URI的值设置为表单的Web应用程序URI值。 这可以通过登录到管理控制台，单击“服务”>“表单”，然后将Web根URI设置为https://server-name:port/FormServer来完成。 然后，保存设置。

1. 渲染HTML表单

   调用对 `FormsServiceClient` 象的方 `(Deprecated) renderHTMLForm` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是表单应用程序的一部分，请确保指定完整路径，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定 `TransformTo` HTML首选项类型的enum值。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定 `TransformTo.MSDHTML`。
   * 包含 `com.adobe.idp.Document` 要与表单合并的数据的对象。 如果不想合并数据，请传递空对 `com.adobe.idp.Document` 象。
   * 存 `HTMLRenderSpec` 储HTML运行时选项的对象。
   * 指定标题值的字 `HTTP_USER_AGENT` 符串值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * 存储 `URLSpec` 呈现HTML表单所需的URI值的对象。
   * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。
   该方 `(Deprecated) renderHTMLForm` 法返回一个对 `FormsResult` 象，该对象包含可写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过 `com.adobe.idp.Document` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
   * 通过调用对象的方 `com.adobe.idp.Document` 法获取对象的内容 `getContentType` 类型。
   * 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `com.adobe.idp.Document` 类型。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象通过调用该对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
   * 通过 `java.io.InputStream` 调用对象的方 `com.adobe.idp.Document` 法创建对 `getInputStream` 象。
   * 创建一个字节数组，并通过调用对象的方法并将字节数 `InputStream` 组作为参数传 `read` 递，用表单数据流填充它。
   * 调用对 `javax.servlet.ServletOutputStream` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

**另请参阅**

[将表单渲染为HTML](#rendering-forms-as-html)

[快速入门（SOAP模式）:使用Java API渲染HTML表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API将表单渲染为HTML {#render-a-form-as-html-using-the-web-service-api}

使用Forms API（Web服务）渲染HTML表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms Client API对象

   创建对 `FormsService` 象并设置身份验证值。

1. 设置HTML运行时选项

   * 使用对 `HTMLRenderSpec` 象的构造函数创建对象。
   * 要使用工具栏渲染HTML表单，请调 `HTMLRenderSpec` 用对象的方 `setHTMLToolbar` 法并传递枚 `HTMLToolbar` 举值。 例如，要显示垂直HTML工具栏，请传递 `HTMLToolbar.Vertical`。
   * 要设置HTML表单的区域设置值，请调用对 `HTMLRenderSpec` 象的方法并 `setLocale` 传递一个指定区域设置值的字符串值。 有关详细信息，请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 要在完整的HTML标签中呈现HTML表单，请调 `HTMLRenderSpec` 用对象的方 `setOutputType` 法并传递 `OutputType.FullHTMLTags`。
   >[!NOTE]
   当选项为并引用承载AEM Forms的J2EE应用程序服务器以外的服务器( `StandAlone` 该值是使用传递给对象方法的对象 `true` 指定的)时，表 `ApplicationWebRoot` 单在HTML中不 `ApplicationWebRoot``URLSpec``FormsServiceClient``(Deprecated) renderHTMLForm` 会成功呈现。 如果是 `ApplicationWebRoot` 承载AEM表单的另一台服务器，则需要将管理控制台中的Web根URI的值设置为表单的Web应用程序URI值。 这可以通过登录到管理控制台，单击“服务”>“表单”，然后将Web根URI设置为https://server-name:port/FormServer来完成。 然后，保存设置。

1. 渲染HTML表单

   调用对 `FormsService` 象的方 `(Deprecated) renderHTMLForm` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是表单应用程序的一部分，请确保指定完整路径，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定 `TransformTo` HTML首选项类型的enum值。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定 `TransformTo.MSDHTML`。
   * 包含 `BLOB` 要与表单合并的数据的对象。 如果您不想合并数据，请传递 `null`。 (请参阅 [使用可流式布局预填充表单](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)。)
   * 存 `HTMLRenderSpec` 储HTML运行时选项的对象。
   * 指定标题值的字 `HTTP_USER_AGENT` 符串值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。 如果不想设置此值，可以传递空字符串。
   * 存储 `URLSpec` 呈现HTML表单所需的URI值的对象。 (请参 [阅指定URI值](/help/forms/developing/rendering-interactive-pdf-forms.md)。)
   * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。 (请参 [阅将文件附加到表单](/help/forms/developing/rendering-interactive-pdf-forms.md)。)
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空对象。 此参数值存储呈现的表单。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空对象。 此参数将存储输出XML数据。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填充的空对象。 此参数将存储表单中的页数。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空对象。 此参数将存储区域设置值。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空对象。 此参数将存储所使用的HTML呈现值。
   * 将包含 `com.adobe.idp.services.holders.FormsResultHolder` 此操作结果的空对象。
   该方 `(Deprecated) renderHTMLForm` 法使用必 `com.adobe.idp.services.holders.FormsResultHolder` 须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过 `FormResult` 获取对象数据成员的 `com.adobe.idp.services.holders.FormsResultHolder` 值来创建 `value` 对象。
   * 通过调 `BLOB` 用对象的方法创建包含表 `FormsResult` 单数据的对 `getOutputContent` 象。
   * 通过调用对象的方 `BLOB` 法获取对象的内容 `getContentType` 类型。
   * 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `BLOB` 类型。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象通过调用该对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
   * 创建一个字节数组，并通过调用对象的 `BLOB` 方法填充该 `getBinaryData` 数组。 此任务将对象的内 `FormsResult` 容分配给字节数组。
   * 调用对 `javax.servlet.http.HttpServletResponse` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

**另请参阅**

[将表单渲染为HTML](#rendering-forms-as-html)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

