---
title: 移动应用程序的内容页面模板
description: 关注此页面，了解移动应用程序的页面模板。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7f00d426-4d28-41ee-8c54-636349e48669
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2569'
ht-degree: 0%

---

# 移动应用程序的页面模板 {#page-templates-for-mobile-apps}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

## 移动应用程序的页面模板 {#page-templates-for-mobile-apps-1}

您为应用程序创建的页面组件基于/libs/mobileapps/components/angular/ng-page组件([在本地服务器的CRXDE Lite中打开](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page))。 此组件包含组件继承或覆盖的以下JSP脚本：

* ng-page.jsp
* head.jsp
* body.jsp
* angular-app-module.js.jsp
* angular-route-fragment.js.jsp
* angular-app-controllers.js.jsp
* controller.js.jsp
* template.jsp
* angular-module-list.js.jsp
* header.jsp
* footer.jsp
* js_clientlibs.jsp
* css_clientlibs.jsp

### ng-page.jsp {#ng-page-jsp}

使用`applicationName`属性确定应用程序的名称，并通过pageContext公开它。

包括head.jsp和body.jsp。

### head.jsp {#head-jsp}

写出应用程序页面的`<head>`元素。

如果要覆盖应用程序的视区元属性，这是您覆盖的文件。

按照最佳实践，应用程序在标题中包含客户端库的css部分，而JS包含在结束&lt; `body>`元素中。

### body.jsp {#body-jsp}

angular根据是否检测到wcmMode (！= WCMMode.DISABLED)，以确定是打开页面进行创作，还是将其作为已发布的页面。

**创作模式**

在创作模式下，每个页面将单独呈现。 angular不处理页面之间的路由，也不能使用ng-view加载包含页面组件的部分模板。 相反，页面模板(template.jsp)的内容通过`cq:include`标记包含在服务器端。

此策略使作者功能(例如，在段落系统、Sidekick、设计模式等中添加和编辑组件)无需修改即可正常工作。 依赖客户端渲染的页面（例如应用程序的页面）在AEM创作模式下性能不佳。

template.jsp include封装在包含`ng-controller`指令的`div`元素中。 此结构启用DOM内容与控制器的链接。 因此，虽然在客户端呈现自身的页面会失败，但可以正常工作的各个组件（请参阅下面关于组件的部分）。

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Publish模式**

在发布模式下（例如，使用内容同步导出应用程序时），所有页面都会变为单页应用程序(SPA)。 (要了解SPA，请使用Angular教程，特别是[https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07)。)

SPA中只有一个HTML页面（包含`<html>`元素的页面）。 此页面称为“布局模板”。 在Angular术语中，它是“……一种适用于我们应用程序中所有视图的模板”。 将此页面视为“顶级应用程序页面”。 按照惯例，顶级应用程序页面是您应用程序中最接近根的`cq:Page`节点（不是重定向）。

由于应用程序的实际URI在发布模式下不会更改，因此从该页面引用外部资产必须使用相对路径。 因此，提供了一个特殊的图像组件，在渲染要导出的图像时，该组件会考虑此顶级页面。

作为SPA，此布局模板页只生成一个带有ng-view指令的div元素。

```xml
 <div ng-view ng-class="transition"></div>
```

angular路由服务使用此元素来显示应用程序中每个页面的内容，包括当前页面的可创作内容（包含在template.jsp中）。

body.jsp文件包括空的header.jsp和footer.jsp。 如果您要在每个页面上提供静态内容，则可以在应用程序中覆盖这些脚本。

最后，Javascript clientlibs包含在&lt;body>元素的底部，其中包括在服务器上生成的两个特殊JS文件： *&lt;页面名称>*.angular应用程序模块.js和&#x200B;*&lt;页面名称>*.angular应用程序控制器.js。

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

此脚本定义应用程序的Angular模块。 此脚本的输出链接到模板组件的其余部分通过ng-page.jsp中的`html`元素生成的标记，该标记包含以下属性：

```xml
ng-app="<c:out value='${applicationName}'/>"
```

此属性指示Angular此DOM元素的内容应链接到以下模块。 此模块将视图(在AEM中，这些资源将为cq：Page资源)与相应的控制器链接。

此模块还定义了一个名为`AppController`的顶级控制器，该控制器将`wcmMode`变量公开到作用域中，并配置从中获取内容同步更新负载的URI。

最后，本模块循环访问每个下级页面（包括本身）并呈现每个页面的路由片段的内容(通过angular-route-fragment.js选择器和扩展)，包括它作为Angular$routeProvider的配置条目。 换句话说，$routeProvider会告知应用程序在请求给定路径时要呈现的内容。

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

此脚本将生成一个必须采用以下形式的JavaScript片段：

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

此代码向$routeProvider(在angular-app-module.js.jsp中定义)指示“/&lt;path>”将由位于`templateUrl`的资源处理，并由`controller`接线（我们将转到下一个）。

如有必要，您可以覆盖此脚本以处理更复杂的路径，包括那些具有变量的路径。 随AEM一起安装的/apps/weretail-app/components/angular/ng-template-page/angular-route-fragment.js.jsp脚本中提供了这方面的示例：

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

在Angular中，控制器连接$scope中的变量，使其暴露在视图中。 angular-app-controllers.js.jsp脚本遵循angular-app-module.js.jsp所示的模式，即遍历每个下级页面（包括本身），并输出每个页面定义的控制器片段(通过controller.js.jsp)。 它定义的模块名为`cqAppControllers`，必须作为顶级应用模块的依赖项列出，以便可以使用页面控制器。

### controller.js.jsp {#controller-js-jsp}

controller.js.jsp脚本为每个页面生成控制器片段。 此控制器片段采用以下形式：

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

为`data`变量分配了Angular`$http.get`方法返回的承诺。 如果需要，此页面中包含的每个组件都可以提供一些.json内容(通过其angular.json.jsp脚本)，并在解析时对此请求的内容执行操作。 该请求在移动设备上非常快，因为它仅访问文件系统。

为了使组件以这种方式成为控制器的一部分，它应该扩展/libs/mobileapps/components/context/ng-componentangular并包含`frameworkType: angular`属性。

### template.jsp {#template-jsp}

首先在body.jsp部分介绍，template.jsp仅包含页面的parsys。 在发布模式下，此内容被直接引用（位于&lt;page-path>.template.html），并通过在$routeProvider上配置的templateUrl加载到SPA中。

此脚本中的parsys可以配置为接受任何类型的组件。 但是，在处理为传统网站(而不是SPA)构建的组件时，必须谨慎。 例如，基础图像组件仅在顶级应用程序页面上正常工作，因为它并非设计为引用应用程序内的资产。

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

此脚本仅输出顶级Angular应用程序模块的Angular依赖关系。 angular-app-module.js.jsp引用了该函数。

### header.jsp {#header-jsp}

将静态内容放置在应用程序顶部的脚本。 此内容由顶级页面包含，不在ng-view的范围内。

### footer.jsp {#footer-jsp}

将静态内容放置在应用程序底部的脚本。 此内容由顶级页面包含，不在ng-view的范围内。

### js_clientlibs.jsp {#js-clientlibs-jsp}

覆盖此脚本以包含您的JavaScript clientlibs。

### css_clientlibs.jsp {#css-clientlibs-jsp}

覆盖此脚本以包含您的CSS clientlibs。

## 应用程序组件 {#app-components}

应用程序组件不仅必须在AEM实例（发布或创作）上运行，而且还必须在应用程序内容通过“内容同步”导出到文件系统时运行。 因此，该组件必须包括以下特性：

* 必须相对引用PhoneGap应用程序中的所有资产、模板和脚本。
* 如果AEM实例在创作或发布模式下运行，则链接的处理方式会有所不同。

### 相对Assets {#relative-assets}

PhoneGap应用程序中任何给定资产的URI不仅会因平台而异，而且在应用程序的每次安装中都是唯一的。 例如，记下在iOS模拟器中运行的应用程序的以下URI：

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/weretail/apps/ng-we-retail/en/home.html`

请注意路径中的GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39;。

作为PhoneGap开发人员，您关注的内容位于www目录下方。 要访问应用程序资产，请使用相对路径。

为了解决此问题，PhoneGap应用程序使用单页应用程序(SPA)模式，以便基本URI（不包括哈希）永不更改。 因此，您引用的每个资源、模板或脚本**都必须相对于您的顶级页面。 **顶级页面通过`<name>.angular-app-module.js`和`<name>.angular-app-controllers.js`初始化Angular路由和控制器。 此页面应该是距离存储库根目录*不*扩展sling：redirect的最近页面。

有几种辅助方法可用于处理相对路径：

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

要查看其用法的示例，请打开位于/libs/mobileapps/components/angular的mobileapps源。

### 链接 {#links}

链接必须使用`ng-click="go('/path')"`函数来支持所有WCM模式。 此函数依赖范围变量的值以正确确定链接操作：

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

当`$scope.wcmMode == true`时，我们将按常规方式处理每个导航事件，以便结果对URL的路径和/或页面部分进行更改。

或者，如果`$scope.wcmMode == false`，则每个导航事件都会导致URL的哈希部分发生更改，该哈希部分由Angular的ngRoute模块在内部解析。

### 组件脚本详细信息 {#component-script-details}

![chlimage_1-51](assets/chlimage_1-51.png)

### ng-component.jsp {#ng-component-jsp}

此脚本在检测到编辑模式时显示组件内容或合适的占位符。

### template.jsp {#template-jsp-1}

template.jsp脚本呈现组件的标记。 如果相关组件由从AEM提取的JSON数据(例如“ng-text”：/libs/mobileapps/components/angular/ng-text/template.jsp)驱动，则此脚本将负责使用页面的控制器范围公开的数据来连接标记。

但是，性能要求有时要求不执行客户端模板化（也称为数据绑定）。 在这种情况下，只需在服务器端呈现组件的标记，并且该标记包含在页面模板内容中即可。

### overhead.jsp {#overhead-jsp}

angular在由JSON数据驱动的组件（如“ng-text”：/libs/mobileapps/components/template/ng-text）中，overhead.jsp可用于从template.jsp中删除所有Java代码。 然后，它从template.jsp中引用，并且在请求中公开的任何变量都可供使用。 此策略鼓励逻辑与呈现分离，并限制从现有组件派生新组件时必须复制和粘贴的代码量。

### controller.js.jsp {#controller-js-jsp-1}

如[AEM页面模板](/help/mobile/apps-architecture.md)中所述，每个组件都可以输出一个JavaScript片段以使用`data`承诺公开的JSON内容。 按照Angular约定，控制器只应用于将变量分配给范围。

### angular.json.jsp {#angular-json-jsp}

此脚本作为片段包含在全页“&lt;page-name>.page.json”文件中，该文件将针对每个扩展ng-page的页面导出angular。 在此文件中，组件开发人员可以公开组件所需的任何JSON结构。 在“ng-text”示例中，此结构仅包括组件的文本内容，以及一个指示组件是否包含富文本的标记。

We.Retail应用程序产品组件是一个更复杂的示例(/apps/weretail-app/components/angular/ng-product)：

```xml
{
    "content-par/ng-product": {
        "items": [{
            "name": "Cajamara",
            "description": "Bike",
            "summaryHTML": "",
            "price": "$610.00",
            "SKU": "eqsmcj",
            "numberOfLikes": "0",
            "numberOfComments": "0"
        }]
    },
    "content-par/ng-product/ng-image": {
        "items": [{
            "hasContent": true,
            "imgSrc": "home/products/eq/eqsm/eqsmcj/jcr_content/content-par/ng-product/ng-image.img.jpg/1377771306985.jpg",
            "description": "",
            "alt": "Cajamara",
            "title": "Cajamara",
            "hasLink": false,
            "linkPath": "",
            "attributes": [{
                "attributeName": "class",
                "attributeValue": "cq-dd-image"
            }]
        }]
    }
}
```

## CLI Assets下载内容 {#contents-of-the-cli-assets-download}

从“应用程序”控制台下载CLI资产以针对特定平台对其进行优化，然后使用PhoneGap命令行集成(CLI) API构建应用程序。 保存到本地文件系统的ZIP文件的内容具有以下结构：

```xml
.cordova/
  |- hooks/
     |- after_prepare/
     |- before_platform_add/
     |- Other Hooks
plugins/
www/
  |- config.xml
  |- index.html
  |- res/
  |- etc/
  |- apps/
  |- content/
  |- package.json
  |- package-update.json
```

### .cordova {#cordova}

这是一个隐藏目录，根据您当前的操作系统设置，您可能无法看到该目录。 您应该配置操作系统，以便在计划修改它所包含的应用程序挂接时显示此目录。

### .cordova/hooks/ {#cordova-hooks}

此目录包含[CLI挂接](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c)。 Hooks目录中的文件夹包含node.js脚本，这些脚本在构建期间的精确时间点运行。

### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

after-platform_add目录包含`copy_AMS_Conifg.js`文件。 此脚本可复制配置文件以支持AdobeMobile Services分析的收集。

### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

after-prepare目录包含`copy_resource_files.js`文件。 此脚本可将多个图标和启动屏幕图像复制到平台特定的位置。

### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

before_platform_add目录包含`install_plugins.js`文件。 此脚本将遍历一个Cordova插件标识符列表，以安装它所检测到的那些尚不可用。

此策略不要求您每次执行Maven `content-package:install`命令时将插件捆绑并安装到AEM。 将文件签入SCM系统的替代策略需要重复的捆绑和安装活动。

### .cordova/挂钩/其他挂钩 {#cordova-hooks-other-hooks}

根据需要包含其他挂接。 可以使用以下挂接（如Phonegap示例hello world应用程序所提供）：

* after_build
* before_build
* after_compile
* before_compile
* after_docs
* before_docs
* after_emulate
* before_emulate
* after_platform_add
* before_platform_add
* after_platform_ls
* before_platform_ls
* after_platform_rm
* before_platform_rm
* after_plugin_add
* before_plugin_add
* after_plugin_ls
* before_plugin_ls
* after_plugin_rm
* before_plugin_rm
* after_prepare
* before_prepare
* after_run
* before_run

### 平台/ {#platforms}

在您对项目执行`phonegap run *<platform>*`命令之前，此目录为空。 当前，`*<platform>*`可以是`ios`或`android`。

在为特定平台构建应用程序后，将创建相应的目录，并且其中包含特定于平台的应用程序代码。

### 插件/ {#plugins}

执行`phonegap run *<platform>*`命令后，`.cordova/hooks/before_platform_add/install_plugins.js`文件中列出的每个插件均会填充插件目录。 目录最初是空的。

### www/ {#www}

www目录包含实施应用程序外观和行为的所有Web内容(HTML、JS和CSS文件)。 除下述例外情况外，此内容源自AEM，并通过Content Sync导出为其静态形式。

### www/config.xml {#www-config-xml}

PhoneGap文档(`https://docs.phonegap.com`)将此文件称为“全局配置文件”。 config.xml包含许多应用程序属性，例如应用程序名称、应用程序“首选项”(例如，iOS Webview是否允许过度滚动)以及PhoneGap Build仅使用&#x200B;*的*&#x200B;插件依赖项。

config.xml文件是AEM中的静态文件，通过Content Sync按原样导出。

### www/index.html {#www-index-html}

index.html文件将重定向到应用程序的起始页。

config.xml文件包含`content`元素：

`<content src="content/phonegap/weretail/apps/ng-we-retail/en.html" />`

在PhoneGap文档(`https://docs.phonegap.com`)中，此元素描述为“可选的&lt;content>元素在顶级Web资产目录中定义应用程序的起始页面。 默认值为index.html，通常显示在项目的顶级www目录中。”

如果没有index.html文件，则PhoneGap Build失败。 因此，此文件包含在内。

### www/res {#www-res}

res目录包含启动画面图像和图标。 `copy_resource_files.js`脚本在`after_prepare`生成阶段将文件复制到其平台特定的位置。

### www/etc {#www-etc}

按照惯例，在AEM中，/etc节点包含静态clientlib内容。 etc目录包含Topcoat、AngularJS和We.Retail ng-clientlibsall库。

### www/apps {#www-apps}

apps目录包含与启动页面相关的代码。 AEM应用程序启动页的独特之处在于，它可以在不进行用户交互的情况下初始化应用程序。 因此，应用程序的clientlib内容（CSS和JS）最小，从而最大限度地提高了性能。

### www/content {#www-content}

内容目录包含应用程序的其余Web内容。 内容可以包括但不限于以下文件：

* HTML页面内容，直接在AEM中创作
* 与AEM组件关联的图像资源
* 服务器端脚本生成的JavaScript内容
* 描述页面或组件内容的JSON文件

### www/package.json {#www-package-json}

package.json文件是一个清单文件，它列出了&#x200B;**完整**&#x200B;内容同步下载包含的文件。 此文件还包含生成内容同步有效负载的时间戳( `lastModified`)。 在从AEM请求对应用程序进行部分更新时，将使用此属性。

### www/package-update.json {#www-package-update-json}

如果此有效负载是整个应用程序的下载，则此清单包含作为`package.json`的文件的确切列表。

但是，如果此有效负载是部分更新，则`package-update.json`仅包含此特定有效负载中包含的文件。
