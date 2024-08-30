---
title: 将自适应表单嵌入到外部网页中
description: 了解将自适应表单嵌入到外部网页中
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 2a237f74-fdfc-4e28-841c-f69afb7b99cf
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 60cc4096c4fd1b51e1d37b6e6f4cdb8806fd79eb
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 98%

---

# 将自适应表单嵌入到外部网页中{#embed-adaptive-form-in-external-web-page}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/embed-adaptive-form-core-components-external-web-page) |
| AEM 6.5 | 本文 |


<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应Forms的旧方法。</span>

可[将自适应表单嵌入到 AEM Sites 页面](/help/forms/using/embed-adaptive-form-aem-sites.md)或托管在 AEM 之外的网页中。嵌入的自适应表单功能齐全，用户无需离开页面即可填写并提交表单。它帮助用户留在网页上其他元素的上下文中，并同时与该表单交互。

## 前提条件 {#prerequisites}

在将自适应表单嵌入到外部网站之前，请执行以下步骤：

* 发布要嵌入到 AEM Forms 服务器的发布实例的自适应表单。
* 在您的网站上创建或标识一个可托管自适应表单的网页。确保该网页能够[从 CDN 读取 jQuery 文件](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js)或嵌入了 jQuery 的本地副本。渲染自适应表单需要 jQuery。
* 当 AEM 服务器与该网页不在相同域中时，执行在[使 AEM Forms 可将自适应表单提供给跨域站点](#cross-site)部分中列出的步骤。

## 嵌入自适应表单 {#embed-adaptive-form}

通过在网页中插入几行 JavaScript 即可嵌入自适应表单。这段代码中的 API 将一个 HTTP 请求发送到自适应表单资源的 AEM 服务器，然后将该自适应表单注入到指定的表单容器中。

要嵌入自适应表单，请执行以下操作：

1. 用以下代码在您的网站上创建一个网页：

   ```html
   <!doctype html>
   <html>
     <head>
       <title>This is the title of the webpage!</title>
       <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
     </head>
     <body>
     <div class="customafsection"/>
       <p>This section is replaced with the adaptive form.</p>
   
    <script>
    var options = {path:"/content/forms/af/locbasic.html", dataRef:"", themepath:"", CSS_Selector:".customafsection"};
    alert(options.path);
    var loadAdaptiveForm = function(options){
    //alert(options.path);
       if(options.path) {
           // options.path refers to the path of the adaptive form
           // For Example: /content/forms/af/ABC, where ABC is the adaptive form
           // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
           var path = options.path;
           path += "/jcr:content/guideContainer.html";
           $.ajax({
               url  : path ,
               type : "GET",
               data : {
                   // Set the wcmmode to be disabled
                   wcmmode : "disabled"
                   // Set the data reference, if any
                  // "dataRef": options.dataRef
                   // Specify a different theme for the form object
                 //  "themeOverride" : options.themepath
               },
               async: false,
               success: function (data) {
                   // If jquery is loaded, set the inner html of the container
                   // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not evaluate the script tag in HTML as per the HTML5 spec
                   // For example: document.getElementById().innerHTML
                   if(window.$ && options.CSS_Selector){
                       // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the script tag.
                       $(options.CSS_Selector).html(data);
                   }
               },
               error: function (data) {
                   // any error handler
               }
           });
       } else {
           if (typeof(console) !== "undefined") {
               console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
           }
       }
    }(options);
   
    </script>
     </body>
   </html>
   ```

1. 在嵌入的代码中：

   * 将 *options.path* 变量的值更改为该自适应表单的发布 URL 的路径。如果 AEM 服务器在某个上下文路径上运行，请确保该 URL 包含此上下文路径。始终提及该自适应表单的完整名称（包括扩展名）。例如，上述代码和自适应表单驻留在同一 AEM Forms 服务器上，因此，该示例使用自适应表单的上下文路径 `/content/forms/af/locbasic.html`。
   * 将 *options.dataRef* 替换为与 URL 一起传递的属性。您可以使用 dataref 变量来[预填充自适应表单](/help/forms/using/prepopulate-adaptive-form-fields.md)。
   * 将 *options.themePath* 替换为自适应表单中配置的主题之外的主题的路径。或者，您可以使用请求属性指定主题路径。
   * CSS_Selector 是将自适应表单嵌入到其中的表单容器的 CSS 选择器。例如，.customafsection css 类是上面示例中的 CSS 选择器。

自适应表单嵌入到网页中。在嵌入的自适应表单中观察以下各项：

* 嵌入的表单中不包括原始自适应表单中的页眉和页脚。
* 可在 Forms Portal 的“草稿”和“提交”选项卡中找到草稿和提交的表单。
* 在原始自适应表单上配置的提交操作保留在嵌入的表单中。
* 自适应表单规则保留在嵌入的表单中并功能齐全。
* 在原始自适应表单中配置的体验定位和 A/B 测试在嵌入的表单中不起作用。
* 如果在原始表单上配置了 Adobe Analytics，则分析数据将由 Adobe Analytics 服务器捕获。但是，在表单分析报告中找不到这些数据。

## 示例拓扑 {#sample-topology}

嵌入自适应表单的外部网页将请求发送到 AEM 服务器，该服务器通常位于专用网络中的防火墙后面。为了确保将请求安全地定向到 AEM 服务器，建议设置反向代理服务器。

让我们看一个如何无需 Dispatcher 即可设置 Apache 2.4 反向代理服务器的示例。在此示例中，您将使用 `/forms` 上下文路径托管 AEM 服务器，并为该反向代理映射 `/forms`。这样确保将 Apache 服务器上对 `/forms` 的任何请求都定向到 AEM 实例。此拓扑有助于减少 Dispatcher 层的规则数量，因为所有前缀为 `/forms` 的请求都将路由到 AEM 服务器。

1. 打开 `httpd.conf` 配置文件，并将下面几行代码解除注释。或者，还可在该文件中添加这几行代码。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 通过在 `httpd-proxy.conf` 配置文件中添加以下代码行而设置代理规则。

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   将 `[AEM_Instance]` 替换为规则中的 AEM 服务器发布 URL。

如果不将 AEM 服务器挂载到某个上下文路径，则 Apache 层的代理规则将如下所示：

```text
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>如果设置了任何其他拓扑，请确保将提交、预填充和其他 URL 添加到 Dispatcher 层的允许列表。

## 最佳实践 {#best-practices}

将自适应表单嵌入到网页中时，请考虑遵循以下最佳实践：

* 确保在网页 CSS 中定义的样式规则不与表单对象 CSS 发生冲突。要避免发生冲突，可使用 AEM 客户端库在自适应表单主题中重用网页 CSS。有关在自适应表单主题中使用客户端库的信息，请参阅 [AEM Forms 中的主题](../../forms/using/themes.md)。
* 让该网页中的表单容器使用整个窗口宽度。这样确保为移动设备配置的 CSS 规则不作任何更改地正常工作。如果表单容器不占用整个窗口宽度，则必须编写自定义 CSS 以使表单适应不同的移动设备。
* 使用 `[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API 获取客户端中表单数据的 XML 或 JSON 表示形式。
* 使用 `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API 从 HTML DOM 卸载该自适应表单。
* 设置从 AEM 服务器发送响应时的 access-control-origin 标头。

## 使 AEM Forms 能够将自适应表单提供给跨域站点 {#cross-site}

1. 在 AEM 发布实例上，转到 `https://'[server]:[port]'/system/console/configMgr` 上的 AEM Web 控制台配置管理器。
1. 找到并打开 **Apache Sling 反向链接过滤器**&#x200B;配置。
1. 在“允许的主机”字段中，指定该网页所在的域。这样使主机可向 AEM 服务器发出 POST 请求。还可使用正则表达式指定一系列外部应用程序域。
