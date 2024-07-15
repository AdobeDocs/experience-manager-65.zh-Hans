---
title: 单页面应用程序
description: 按照本页了解单页应用程序，即，您可以创建与桌面或移动设备应用程序具有相同性能的应用程序。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 1%

---

# 单页面应用程序{#single-page-applications}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

[单页应用程序](https://en.wikipedia.org/wiki/Single-page_application) (SPA)已达到临界质量，被广泛认为是使用Web技术构建无缝体验的最有效模式。 通过遵循SPA模式，您可以创建一个与桌面或移动应用程序具有相同性能的应用程序，但由于该应用程序在开放Web标准中的基础特性，它可以覆盖多种设备平台和板型。

一般而言，SPA的性能优于传统的基于页面的网站，因为它们通常只加载一次完整的HTML页面&#x200B;****（包括CSS、JS和支持的字体内容），然后每次在应用程序中发生状态更改时只加载所需的内容。 此状态更改所需的内容可能因所选技术集而异，但通常包括单个HTML片段以替换现有“视图”，以及执行JS代码块以连接新视图并执行可能需要的任何客户端模板渲染。 此状态更改的速度可以通过支持模板缓存机制进一步提高，如果使用Adobe PhoneGap，甚至可以离线访问模板内容。

AEM 6.1支持通过AEM应用程序构建和管理SPA。 本文介绍SPA背后的概念，以及这些概念如何使用[AngularJS](https://angularjs.org/)将您的品牌带入App Store和Google Play。

## AEM应用程序中的SPA {#spa-in-aem-apps}

AEM Apps中的单页应用程序框架不仅能够实现AngularJS应用程序的高性能，而且还能让作者（或其他非技术人员）能够通过传统上为管理网站而保留的触控优化拖放编辑器环境来创建和管理应用程序内容。 已使用AEM构建站点？ 您发现，使用AEM应用程序可以轻松重用内容、组件、工作流、资源和权限。

## AngularJS应用程序模块 {#angularjs-application-module}

AEM应用程序可为您处理大多数AngularJS配置，包括汇集您应用程序的顶级模块。 默认情况下，此模块名为“AEMAngularApp”，负责生成该模块的脚本可在/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp上找到（和覆盖）。

应用程序初始化的一部分过程包括指定应用程序依赖的AngularJS模块。 您的应用程序使用的模块列表由位于/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp的脚本指定，并且可以由您自己的应用程序页面组件覆盖，以拉入您的应用程序所需的任何其他AngularJS模块。 例如，将上述脚本与Geometrixx实施(位于/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp)进行比较。

为了支持在应用程序中的不同状态之间进行导航，angular应用程序模块脚本遍历顶级应用程序页面的所有子页面，以生成一组“路由”，并在Angular的$routeProvider服务上配置每个路径。 有关这种做法在实践中的示例，请查看Geometrixx Outdoors应用程序示例生成的angular — 应用程序 — 模块脚本： （链接需要本地实例）[http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

在挖掘生成的AEMAngularApp时，您会找到一系列指定的路由，如下所示：

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

上述示例特别说明了将参数作为路径的一部分进行传递的示例。 在此示例中，它指示在请求满足指定模式(/content/phonegap/geometrixx-outdoors/en/home/products/：id)的路径时，该路径应由home/products.template.html模板处理并使用“contentphonegapgeometrixxoutdoorsenhomeproducts”控制器。

请求此路由时要加载的模板由templateUrl属性指定。 此模板包含已包含在该页上的AEM组件中的HTML，以及连接应用程序客户端所需的任何AngularJS指令。 有关Geometrixx组件中AngularJS指令的示例，请查看swipe-carousel的template.jsp (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp)的第45行。

## 页面控制者 {#page-controllers}

用Angular自己的话说，“控制器是一个JavaScript构造函数，用于扩大Angular范围。” （[源](https://docs.angularjs.org/guide/controller)） AEM App中的每个页面自动连接到一个控制器，该控制器可由任何指定`angular`的`frameworkType`的控制器来增强。 请查看ng-text组件示例(/libs/mobileapps/components/template/ng-text)，包括cq：templateangular，以确保每次将此组件添加到页面时，它都会包含此重要属性。

有关更复杂的控制器示例，请打开ng-template-page controller.jsp脚本(位于/apps/geometrixx-outdoors-app/components/template/ng-template-pageangular)。 特别有趣的是它在运行时生成的JavaScript代码，该代码将呈现如下：

```xml
// Controller for page 'products'
.controller('contentphonegapgeometrixxoutdoorsenhomeproducts', ['$scope', '$http', '$routeParams',
    function($scope, $http, $routeParams) {
        var sku = $routeParams.id;
        var productPath = '/' + sku.substring(0, 2) + '/' + sku.substring(0, 4) + '/' + sku;
        var data = $http.get('home/products' + productPath + '.angular.json' + cacheKiller);

        /* ng-product component controller (path: content-par/ng-product) */
        data.then(function(response) {
            $scope.contentparngproduct = response.data["content-par/ng-product"].items;
        });

        /* ng-image component controller (path: content-par/ng-product/ng-image) */
        data.then(function(response) {
            $scope.contentparngproductngimage = response.data["content-par/ng-product/ng-image"].items;
        });
    }
])
```

在上例中，从`$routeParams`服务中获取参数，然后将参数按摩到存储JSON数据的目录结构中。 通过以这种方式处理SKU `id`，您可以交付单个产品模板，该模板可以呈现可能包含数千种不同产品的产品数据。 这是一种可扩展性更高的模型，它要求在（潜在的）庞大的产品数据库中为每个项目分别设置一条路由。

此处还有两个组件在起作用： ng-product使用它从上述`$http`调用中提取的数据来扩大范围。 此页面上还有一个ng-image，它反过来也通过从响应中检索的值来扩大范围。 利用Angular的`$http`服务，每个组件都会耐心等待，直到请求完成并完成它创建的承诺。

## 后续步骤 {#the-next-steps}

了解单页应用程序后，请参阅[使用PhoneGap CLI开发应用程序](/help/mobile/phonegap-apps-pg-cli.md)。
